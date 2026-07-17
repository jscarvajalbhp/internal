================================================================================
  README - Tannenberg Copper Project: Laboratory Assay CSVs (TR2502684-TR2502688)
  BHP Drilling-Assays Schema Population
  Date processed: 2026-07-17
================================================================================

SOURCE FILES
------------
Five laboratory batch CSV files received from the analytical laboratory:
  TR2502684.CSV   TR2502685.CSV   TR2502686.CSV   TR2502687.CSV   TR2502688.CSV

All files share an identical non-standard structure (described below).

--------------------------------------------------------------------------------
ORIGINAL FILE STRUCTURE (8-row metadata header)
--------------------------------------------------------------------------------
  Row 1 : Batch/Job ID and sample count        -> maps to Dsptch_L_D / Labjobno
  Row 2 : "Received DD-Mon-YY"                 -> maps to SmpDspDate
  Row 3 : "Reported DD-Mon-YY"                 -> maps to SmpRetDate
  Row 4 : Column names
            Col A        = Sample ID (BATCH NO / sample label)
            Cols B-M     = Weight QA/QC columns (13 columns)
            Cols N+      = Element analytical results (prefixed with @)
  Row 5 : Analytical METHOD per column (e.g. WGH10, CRU24, CRU-QA/QC, PUL-QA/QC, ICP40B, AAS42S)
  Row 6 : Lower Detection Limit (LDETECTION) per column
  Row 7 : Upper Detection Limit (UDETECTION) per column
  Row 8 : UNITS per column (KG, G, %, PPM)
  Row 9+ : Sample data (Sample ID in Col A, values in subsequent columns)

Rows 1-3 are metadata only (no column data).
Rows 4-8 form a 5-row compound header, collapsed into a single descriptive header row
in the output _CombinedHeaders.csv files.
Row 9 onward contains actual assay results.

--------------------------------------------------------------------------------
OUTPUT FILES (per source file, two outputs)
--------------------------------------------------------------------------------
  *_BHP.csv              - BHP Drilling-Assays schema format
  *_CombinedHeaders.csv  - Raw structure with collapsed single-row header

--------------------------------------------------------------------------------
COMBINED HEADER FORMAT (_CombinedHeaders.csv)
--------------------------------------------------------------------------------
Each column header encodes: ElementName_UNIT[METHOD|LDL:value|UDL:value]
Examples:
  Ag_ppm[ICP40B|LDL:2|UDL:10]       - Silver by ICP40B, 2-10 ppm detection range
  Al_pct[ICP40B|LDL:0.01|UDL:15]    - Aluminium by ICP40B, 0.01-15 % range
  Wtkg_KG[WGH10]                     - Sample weight by weighing method WGH10
  Cu_pct[AAS42S|LDL:0.001|UDL:50]   - Copper by AAS42S (high-grade method)

Weight column headers: ColumnName_UNIT[METHOD]
Sample ID column: retained as-is from source (BATCH NO label)

--------------------------------------------------------------------------------
BHP DRILLING-ASSAYS SCHEMA MAPPING (_BHP.csv)
--------------------------------------------------------------------------------
Field               Source / Logic
-----------         -------------------------------------------------------
PROJECTCOD          Fixed: "Tannenberg Copper Project"
HOLEID              Empty (drillhole ID not present in lab files; link via SAMPLEID)
SAMPLEID            Column A (row 9+) - the laboratory sample identifier
SAMPLETYPE          Fixed: "Core"
SapSubType          Fixed: "Drill Core"
Point_Type          Fixed: "Drillhole"
Dsptch_L_D          Row 1 batch ID string (e.g. "TR2502684     133   392")
SmpDspDate          Row 2 received date (e.g. "08-Nov-25")
SmpRetDate          Row 3 reported date (e.g. "14-Nov-25")
Lab_L_D             Source filename (batch reference)
Labjobno            Row 1 batch ID string
AnalysisLD          Empty (list built from column methods if needed)
SampWt_g_D          Column B (Wtkg) - sample weight as received
Wtkg                Raw sample weight (kg) - WGH10 method
Wtcru_dry_kg        Crushed dry weight (kg) - CRU24 method
Tot_Weight_CRU      Total weight after crushing (g) - CRU QA/QC
Pass_2mm_pct        % passing 2mm sieve - CRU QA/QC
Rmnd_2mm_pct        % retained on 2mm sieve - CRU QA/QC
WT_MinusFrac_CRU_g  Weight of minus fraction (g) - CRU QA/QC
WT_PlusFrac_CRU_g   Weight of plus fraction (g) - CRU QA/QC
Tot_Weight_PUL_g    Total weight after pulverizing (g) - PUL QA/QC
Pass_75um_pct       % passing 75um sieve - PUL QA/QC
Rmnd_75um_pct       % retained on 75um sieve - PUL QA/QC
WT_MinusFrac_PUL_g  Weight of minus fraction (g) - PUL QA/QC
WT_PlusFrac_PUL_g   Weight of plus fraction (g) - PUL QA/QC

ELEMENT FIELDS (per element, 4 fields generated):
  {El}_{unit}         Best assay value (raw, including < and > prefixes for detects)
  {El}_{unit}_GMD     Analytical method (e.g. ICP40B, AAS42S)
  {El}_{unit}_LDD     Lower detection limit
  {El}_{unit}_UDD     Upper detection limit

Unit mapping: PPM -> _ppm suffix | % -> _pct suffix | KG -> _kg | G -> _g

Duplicate element/method columns (e.g. @Ag and @Cu appear in both ICP40B and AAS42S):
  Disambiguated by appending method to field name:
    Ag_ppm          (ICP40B primary)
    Ag_ppm_AAS42S   (AAS42S confirmation)
    Cu_ppm          (ICP40B primary)
    Cu_pct_AAS42S   (AAS42S high-grade)

NOTE: Values of "-" in the source (not analysed) are stored as empty string in output.
      Values of "<X" (below detection) and ">X" (above detection) are preserved as-is.

--------------------------------------------------------------------------------
BATCH SUMMARY
--------------------------------------------------------------------------------
  File          Batch ID      Received     Reported     Samples  Elements
  TR2502684     TR2502684     08-Nov-25    14-Nov-25    133      37
  TR2502685     TR2502685     08-Nov-25    14-Nov-25    136      36
  TR2502686     TR2502686     08-Nov-25    14-Nov-25    130      35
  TR2502687     TR2502687     08-Nov-25    14-Nov-25    131      35
  TR2502688     TR2502688     08-Nov-25    14-Nov-25    168      36
  TOTAL                                                 698

ELEMENTS ANALYSED (all files, ICP40B suite):
  Ag, Al, As, Ba, Be, Bi, Ca, Cd, Co, Cr, Cu, Fe, K, La, Li, Mg, Mn, Mo,
  Na, Ni, P, Pb, S, Sb, Sc, Sn, Sr, Ti, V, W, Y, Zn, Zr
  High-grade AAS42S suite (cols 47-50): Ag_AAS, Cu_AAS, Pb_AAS, Zn_AAS

ANALYTICAL METHODS:
  WGH10      - Sample weighing
  CRU24      - Crushing (24-hour, dry weight)
  CRU-QA/QC  - Crushing quality control (sieve fractions)
  PUL-QA/QC  - Pulverizing quality control (75um sieve fractions)
  ICP40B     - Multi-element ICP-OES (40-element suite)
  AAS42S     - Atomic Absorption Spectrometry (high-grade Ag, Cu, Pb, Zn)

--------------------------------------------------------------------------------
FIELDS LEFT EMPTY (not present in source lab data)
--------------------------------------------------------------------------------
  HOLEID, PNTPROSPC, WGS84_CALX/Y/Z, CoordSurv, SurvInstr, SampleDate,
  SAMPLEDBY, Lith1/2, LT_Color1/2, Lith_Desc, Alt_*, MN_Miner_*, Min_Desc,
  OSDU_Inges, GenerMeth, RecvdWt_g

================================================================================
