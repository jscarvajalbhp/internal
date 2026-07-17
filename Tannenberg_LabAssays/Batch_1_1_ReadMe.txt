================================================================================
  README - Batch 1.1
  Project: Tannenberg Copper Project
  BHP Drilling-Assays Schema
  Date processed: 2026-07-17
================================================================================

BATCH OVERVIEW
--------------
  Batch label    : 1.1
  Lab            : SGS Laboratories
  Samples received at lab : 08-Nov-25
  Results reported        : 14-Nov-25
  Total certificates      : 5
  Total samples           : 698

CERTIFICATES IN THIS BATCH
----------------------------
  Certificate     Samples   ICP Elements   AAS Elements
  TR2502684       133       33 + Cu/Pb/Zn %  Ag, Cu, Pb, Zn (AAS42S)
  TR2502685       136       33 + Cu/Zn %     Ag, Cu, Zn (AAS42S)
  TR2502686       130       33 + Cu %        Ag, Cu (AAS42S)
  TR2502687       131       33 + Cu %        Ag, Cu (AAS42S)
  TR2502688       168       33 + Cu/Zn %     Ag, Cu, Zn (AAS42S)

SOURCE FILE STRUCTURE
---------------------
Each source CSV (TR250268X.CSV) had an 8-row non-standard header before any data:
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
  TR2502684_BHP.csv
  TR2502685_BHP.csv
  TR2502686_BHP.csv
  TR2502687_BHP.csv
  TR2502688_BHP.csv

Each file is a unified CSV with:
  LEFT  - BHP Drilling-Assays schema fields (standardised)
  RIGHT - Original raw columns with combined single-row header:
            Element cols : ElementName_UNIT[METHOD|LDL:x|UDL:y]
            Weight cols  : ColName_UNIT[METHOD]
            Sample col   : SampleID_orig

BHP FIELDS POPULATED (all certificates)
-----------------------------------------
  PROJECTCOD    : Tannenberg
  CertificateNo : TR250268X (per certificate)
  Received      : 08-Nov-25
  Reported      : 14-Nov-25
  SAMPLEID      : Lab sample identifier
  SAMPLETYPE    : Core
  SapSubType    : Drill Core
  Point_Type    : Drillhole
  Dsptch_L_D    : Full batch ID string from Row 1
  SmpDspDate    : 08-Nov-25
  SmpRetDate    : 14-Nov-25
  Lab_L_D       : Certificate number (e.g. TR2502684)
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

  ICP40B suite (all 5 certificates):
    Ag_ppm, Al_pct, As_ppm, Ba_ppm, Be_ppm, Bi_ppm, Ca_pct, Cd_ppm,
    Co_ppm, Cr_ppm, Cu_ppm, Fe_pct, K_pct, La_ppm, Li_ppm, Mg_pct,
    Mn_ppm, Mo_ppm, Na_pct, Ni_ppm, P_pct, Pb_ppm, S_pct, Sb_ppm,
    Sc_ppm, Sn_ppm, Sr_ppm, Ti_pct, V_ppm, W_ppm, Y_ppm, Zn_ppm, Zr_ppm

  High-grade percent results (present in some certificates):
    Cu_pct  - all 5 certificates
    Pb_pct  - TR2502684 only
    Zn_pct  - TR2502684, TR2502685, TR2502688

  AAS42S suite (high-grade atomic absorption confirmation):
    Ag_ppm_AAS42S  - all 5 certificates
    Cu_pct (AAS42S) - all 5 certificates
    Pb_pct (AAS42S) - TR2502684 only
    Zn_pct (AAS42S) - TR2502684, TR2502685, TR2502688

ANALYTICAL METHODS
------------------
  WGH10      Sample weighing
  CRU24      Crushing (24-hour dry)
  CRU-QA/QC  Crushing quality control (sieve fractions)
  PUL-QA/QC  Pulverising quality control (75 um sieve fractions)
  ICP40B     Multi-element ICP-OES (33-element suite)
  AAS42S     Atomic Absorption Spectrometry (high-grade Ag, Cu, Pb, Zn)

NOTES
-----
  - Values of "-" in source (not analysed) stored as empty in BHP fields,
    preserved as "-" in the raw original columns on the right.
  - Values prefixed "<" (below detection) or ">" (above detection) kept as-is.
  - HOLEID is empty: link to drillholes via SAMPLEID in the collars/intervals table.
  - Fields not in source (WGS84, lithology, alteration, etc.) are left empty.

================================================================================
