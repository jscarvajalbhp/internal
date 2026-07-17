================================================================================
  README - Batch 1.3
  Project: Tannenberg Copper Project
  BHP Drilling-Assays Schema
  Date processed: 2026-07-17
================================================================================

BATCH OVERVIEW
--------------
  Batch label    : 1.3
  Lab            : SGS Laboratories
  Samples received at lab : 09-Feb-26 to 10-Feb-26 (varies by certificate)
  Results reported        : 23-Feb-26 (all certificates)
  Total certificates      : 6
  Total samples           : 717

CERTIFICATES IN THIS BATCH
----------------------------
  Certificate     Received     Samples   ICP Elements    AAS Elements
  TR2600298       09-Feb-26    150       33 + Cu %       Ag (AAS42S)
  TR2600299       09-Feb-26    150       33 + Cu %       Ag (AAS42S)
  TR2600300       09-Feb-26    150       33 + Cu %       Ag (AAS42S)
  TR2600301       09-Feb-26    150       33 + Cu %       Ag (AAS42S)
  TR2600302       10-Feb-26     67       33 + Cu %       Ag (AAS42S)
  TR2600303       10-Feb-26     50       33              Ag (AAS42S)

SOURCE FILE STRUCTURE
---------------------
Each source CSV (TR260030X.CSV) had an 8-row non-standard header before any data:
  Row 1 : Certificate ID + sample count  -> CertificateNo, Dsptch_L_D, Labjobno
  Row 2 : "Received DD-Mon-YY"           -> Received, SmpDspDate
  Row 3 : "Reported DD-Mon-YY"           -> Reported, SmpRetDate
  Row 4 : Column names
            Col A   = Sample ID
            Cols B-M = Weight QA/QC columns (12 columns)
            Cols N+ = Element results (@ prefix)
  Row 5 : Analytical METHOD per column
  Row 6 : Lower Detection Limit (LDETECTION) per column
  Row 7 : Upper Detection Limit (UDETECTION) per column
  Row 8 : Units per column (KG, G, %, PPM)
  Row 9+: Sample assay data

Rows 1-3 removed from data and captured as individual fields.
Rows 4-8 (5-row compound header) collapsed into a single descriptive label per column,
appended as raw original columns on the right side of each output file.

OUTPUT FILES
------------
  TR2600298_BHP.csv   TR2600299_BHP.csv   TR2600300_BHP.csv
  TR2600301_BHP.csv   TR2600302_BHP.csv   TR2600303_BHP.csv

Each file is a unified CSV with:
  LEFT  - BHP Drilling-Assays schema fields (standardised)
  RIGHT - Original raw columns with combined single-row header:
            Element cols : ElementName_UNIT[METHOD|LDL:x|UDL:y]
            Weight cols  : ColName_UNIT[METHOD]
            Sample col   : SampleID_orig

BHP FIELDS POPULATED (all certificates)
-----------------------------------------
  PROJECTCOD    : Tannenberg
  CertificateNo : TR260030X (per certificate)
  Received      : Per certificate (09-Feb-26 or 10-Feb-26)
  Reported      : 23-Feb-26
  SAMPLEID      : Lab sample identifier
  SAMPLETYPE    : Core
  SapSubType    : Drill Core
  Point_Type    : Drillhole
  Dsptch_L_D    : Full batch ID string from Row 1
  SmpDspDate    : Per certificate received date
  SmpRetDate    : 23-Feb-26
  Lab_L_D       : Certificate number (e.g. TR2600298)
  Labjobno      : Full batch ID string from Row 1
  SampWt_g_D    : Sample weight (kg) from Col B

WEIGHT QC FIELDS
-----------------
  Wtkg               Sample weight as received (kg)           WGH10
  Wtcru_dry_kg       Crushed dry weight (kg)                  CRU24
  Tot_Weight_CRU     Total weight after crushing (g)          CRU QA/QC
  Pass_2mm_pct       % passing 2 mm sieve                     CRU QA/QC
  Rmnd_2mm_pct       % retained on 2 mm sieve                 CRU QA/QC
  WT_MinusFrac_CRU_g Weight of minus fraction after crush (g) CRU QA/QC
  WT_PlusFrac_CRU_g  Weight of plus fraction after crush (g)  CRU QA/QC
  Tot_Weight_PUL_g   Total weight after pulverising (g)       PUL QA/QC
  Pass_75um_pct      % passing 75 um sieve                    PUL QA/QC
  Rmnd_75um_pct      % retained on 75 um sieve                PUL QA/QC
  WT_MinusFrac_PUL_g Weight of minus fraction after pul. (g)  PUL QA/QC
  WT_PlusFrac_PUL_g  Weight of plus fraction after pul. (g)   PUL QA/QC

ANALYTICAL ELEMENT FIELDS
--------------------------
Each element generates 4 BHP fields: value | _GMD (method) | _LDD (lower det.) | _UDD (upper det.)

  ICP40B suite (all 6 certificates):
    Ag_ppm, Al_pct, As_ppm, Ba_ppm, Be_ppm, Bi_ppm, Ca_pct, Cd_ppm,
    Co_ppm, Cr_ppm, Cu_ppm, Fe_pct, K_pct, La_ppm, Li_ppm, Mg_pct,
    Mn_ppm, Mo_ppm, Na_pct, Ni_ppm, P_pct, Pb_ppm, S_pct, Sb_ppm,
    Sc_ppm, Sn_ppm, Sr_ppm, Ti_pct, V_ppm, W_ppm, Y_ppm, Zn_ppm, Zr_ppm

  High-grade percent results:
    Cu_pct  - TR2600298, TR2600299, TR2600300, TR2600301, TR2600302
              (not present in TR2600303)

  AAS42S suite (high-grade atomic absorption confirmation):
    Ag_ppm_AAS42S  - all 6 certificates

ANALYTICAL METHODS
------------------
  WGH10      Sample weighing
  CRU24      Crushing (24-hour dry)
  CRU-QA/QC  Crushing quality control (sieve fractions)
  PUL-QA/QC  Pulverising quality control (75 um sieve fractions)
  ICP40B     Multi-element ICP-OES (33-element suite)
  AAS42S     Atomic Absorption Spectrometry (high-grade Ag)

NOTES
-----
  - Values of "-" in source (not analysed) stored as empty in BHP fields,
    preserved as "-" in the raw original columns on the right.
  - Values prefixed "<" (below detection) or ">" (above detection) kept as-is.
  - HOLEID is empty: link to drillholes via SAMPLEID in the collars/intervals table.
  - Fields not in source (WGS84, lithology, alteration, etc.) are left empty.
  - TR2600303 has a reduced suite: no Cu_pct and no Pb/Zn AAS confirmation.
  - Compared to batches 1.1 and 1.2, Pb_pct and Zn_pct AAS confirmation
    are absent across all certificates in this batch.

================================================================================
