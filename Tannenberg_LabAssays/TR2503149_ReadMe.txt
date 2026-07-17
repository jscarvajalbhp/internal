================================================================================
  README - Certificate TR2503149
  Project: Tannenberg Copper Project
  BHP Drilling-Assays Schema | Batch 1.2
  Date processed: 2026-07-17
================================================================================

CERTIFICATE DETAILS
-------------------
  Certificate No : TR2503149
  Batch          : 1.2
  Samples received at lab : 23-Dec-25
  Results reported        : 06-Feb-26
  Total samples           : 148
  Output file             : TR2503149_BHP.csv

SOURCE FILE STRUCTURE
---------------------
The original TR2503149.CSV had an 8-row non-standard header before any data:
  Row 1 : Certificate ID + sample count  (-> CertificateNo, Dsptch_L_D, Labjobno)
  Row 2 : "Received DD-Mon-YY"           (-> Received, SmpDspDate)
  Row 3 : "Reported DD-Mon-YY"           (-> Reported, SmpRetDate)
  Row 4 : Column names  (Col A = Sample ID; Cols B-M = QC weights; Cols N+ = @Elements)
  Row 5 : Analytical METHOD per column
  Row 6 : Lower Detection Limit (LDETECTION) per column
  Row 7 : Upper Detection Limit (UDETECTION) per column
  Row 8 : Units per column (KG, G, %, PPM)
  Row 9+: Sample assay data

Rows 1-3 were removed and captured as fields.
Rows 4-8 (5-row compound header) were collapsed into a single descriptive label
appended as raw original columns on the right side of the output file.

OUTPUT FILE STRUCTURE (TR2503149_BHP.csv)
---------------------------------------
LEFT  - BHP Drilling-Assays schema fields (standardised)
RIGHT - Original raw columns with combined single-row header:
          Format: ElementName_UNIT[METHOD|LDL:x|UDL:y]  e.g. Ag_ppm[ICP40B|LDL:2|UDL:10]
          Weight cols: ColName_UNIT[METHOD]              e.g. Wtkg_KG[WGH10]
          Col 0: SampleID_orig

BHP FIELDS POPULATED
---------------------
  PROJECTCOD    : Tannenberg
  CertificateNo : TR2503149
  Received      : 23-Dec-25
  Reported      : 06-Feb-26
  SAMPLEID      : Lab sample identifier (e.g. PAL00841)
  SAMPLETYPE    : Core
  SapSubType    : Drill Core
  Point_Type    : Drillhole
  Dsptch_L_D    : Full batch ID string from Row 1
  SmpDspDate    : 23-Dec-25
  SmpRetDate    : 06-Feb-26
  Lab_L_D       : TR2503149
  Labjobno      : Full batch ID string from Row 1
  SampWt_g_D    : Sample weight (kg) from Col B

WEIGHT QC FIELDS (BHP)
-----------------------
  Wtkg              Sample weight as received (kg)          WGH10
  Wtcru_dry_kg      Crushed dry weight (kg)                 CRU24
  Tot_Weight_CRU    Total weight after crushing (g)         CRU QA/QC
  Pass_2mm_pct      % passing 2 mm sieve                    CRU QA/QC
  Rmnd_2mm_pct      % retained on 2 mm sieve                CRU QA/QC
  WT_MinusFrac_CRU_g  Weight minus fraction after crush (g) CRU QA/QC
  WT_PlusFrac_CRU_g   Weight plus fraction after crush (g)  CRU QA/QC
  Tot_Weight_PUL_g  Total weight after pulverising (g)      PUL QA/QC
  Pass_75um_pct     % passing 75 um sieve                   PUL QA/QC
  Rmnd_75um_pct     % retained on 75 um sieve               PUL QA/QC
  WT_MinusFrac_PUL_g  Weight minus fraction after pul. (g)  PUL QA/QC
  WT_PlusFrac_PUL_g   Weight plus fraction after pul. (g)   PUL QA/QC

ANALYTICAL ELEMENT FIELDS (BHP)
--------------------------------
Each element generates 4 fields: value | _GMD (method) | _LDD (lower det.) | _UDD (upper det.)

  ICP40B suite (multi-element ICP-OES):
    Ag_ppm                         (method field: Ag_ppm_GMD | limits: Ag_ppm_LDD / Ag_ppm_UDD)
    Al_pct                         (method field: Al_pct_GMD | limits: Al_pct_LDD / Al_pct_UDD)
    As_ppm                         (method field: As_ppm_GMD | limits: As_ppm_LDD / As_ppm_UDD)
    Ba_ppm                         (method field: Ba_ppm_GMD | limits: Ba_ppm_LDD / Ba_ppm_UDD)
    Be_ppm                         (method field: Be_ppm_GMD | limits: Be_ppm_LDD / Be_ppm_UDD)
    Bi_ppm                         (method field: Bi_ppm_GMD | limits: Bi_ppm_LDD / Bi_ppm_UDD)
    Ca_pct                         (method field: Ca_pct_GMD | limits: Ca_pct_LDD / Ca_pct_UDD)
    Cd_ppm                         (method field: Cd_ppm_GMD | limits: Cd_ppm_LDD / Cd_ppm_UDD)
    Co_ppm                         (method field: Co_ppm_GMD | limits: Co_ppm_LDD / Co_ppm_UDD)
    Cr_ppm                         (method field: Cr_ppm_GMD | limits: Cr_ppm_LDD / Cr_ppm_UDD)
    Cu_ppm                         (method field: Cu_ppm_GMD | limits: Cu_ppm_LDD / Cu_ppm_UDD)
    Fe_pct                         (method field: Fe_pct_GMD | limits: Fe_pct_LDD / Fe_pct_UDD)
    K_pct                          (method field: K_pct_GMD | limits: K_pct_LDD / K_pct_UDD)
    La_ppm                         (method field: La_ppm_GMD | limits: La_ppm_LDD / La_ppm_UDD)
    Li_ppm                         (method field: Li_ppm_GMD | limits: Li_ppm_LDD / Li_ppm_UDD)
    Mg_pct                         (method field: Mg_pct_GMD | limits: Mg_pct_LDD / Mg_pct_UDD)
    Mn_ppm                         (method field: Mn_ppm_GMD | limits: Mn_ppm_LDD / Mn_ppm_UDD)
    Mo_ppm                         (method field: Mo_ppm_GMD | limits: Mo_ppm_LDD / Mo_ppm_UDD)
    Na_pct                         (method field: Na_pct_GMD | limits: Na_pct_LDD / Na_pct_UDD)
    Ni_ppm                         (method field: Ni_ppm_GMD | limits: Ni_ppm_LDD / Ni_ppm_UDD)
    P_pct                          (method field: P_pct_GMD | limits: P_pct_LDD / P_pct_UDD)
    Pb_ppm                         (method field: Pb_ppm_GMD | limits: Pb_ppm_LDD / Pb_ppm_UDD)
    S_pct                          (method field: S_pct_GMD | limits: S_pct_LDD / S_pct_UDD)
    Sb_ppm                         (method field: Sb_ppm_GMD | limits: Sb_ppm_LDD / Sb_ppm_UDD)
    Sc_ppm                         (method field: Sc_ppm_GMD | limits: Sc_ppm_LDD / Sc_ppm_UDD)
    Sn_ppm                         (method field: Sn_ppm_GMD | limits: Sn_ppm_LDD / Sn_ppm_UDD)
    Sr_ppm                         (method field: Sr_ppm_GMD | limits: Sr_ppm_LDD / Sr_ppm_UDD)
    Ti_pct                         (method field: Ti_pct_GMD | limits: Ti_pct_LDD / Ti_pct_UDD)
    V_ppm                          (method field: V_ppm_GMD | limits: V_ppm_LDD / V_ppm_UDD)
    W_ppm                          (method field: W_ppm_GMD | limits: W_ppm_LDD / W_ppm_UDD)
    Y_ppm                          (method field: Y_ppm_GMD | limits: Y_ppm_LDD / Y_ppm_UDD)
    Zn_ppm                         (method field: Zn_ppm_GMD | limits: Zn_ppm_LDD / Zn_ppm_UDD)
    Zr_ppm                         (method field: Zr_ppm_GMD | limits: Zr_ppm_LDD / Zr_ppm_UDD)
    Cu_pct                         (method field: Cu_pct_GMD | limits: Cu_pct_LDD / Cu_pct_UDD)
  AAS42S suite (high-grade AAS confirmation):
    Ag_ppm_AAS42S                  (method field: Ag_ppm_AAS42S_GMD | limits: Ag_ppm_AAS42S_LDD / Ag_ppm_AAS42S_UDD)
NOTES
-----
  - Values of "-" in source (not analysed) are stored as empty string in BHP fields
    but preserved as "-" in the raw original columns on the right.
  - Values prefixed with "<" (below detection) or ">" (above detection) are kept as-is.
  - HOLEID is empty: link samples to drillholes via SAMPLEID in the collars/intervals table.
  - Fields not present in source (WGS84_CALX/Y/Z, Lith, Alt, Min, etc.) are left empty.

================================================================================
