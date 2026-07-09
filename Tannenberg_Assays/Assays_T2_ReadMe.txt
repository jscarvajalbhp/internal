================================================================================
  README — Assays_T2_BHP.csv
  BHP Drilling-Assays Schema Population
  Project: Tannenberg Copper Project
  Date: 2026-07-09
================================================================================

DATASET OVERVIEW
----------------
Name     : Tannenberg Copper Project — Drillhole Assay Dataset (T2)
Source   : Project internal CSV — Assays (T2).csv
Format   : CSV (comma-separated, UTF-8 with BOM)
CRS      : DHDN / Gauss-Krüger Zone 4 (EPSG:31468) — mid_x/mid_y coordinates
Country  : Germany (central Hesse — Bad Hersfeld / Rotenburg an der Fulda area)
Features : 833 assay intervals across 35 drillholes
Output   : Assays_T2_BHP.csv

COORDINATE SYSTEM
------------------
Source coordinates (mid_x, mid_y) are interval midpoints in DHDN/GK Zone 4
(EPSG:31468). These represent the 3D midpoint of each downhole sample interval.
  mid_x range: 4,336,189 – 4,358,153 m (Easting, GK4)
  mid_y range: 5,643,832 – 5,676,848 m (Northing, GK4)
  WGS84 extent: ~9.62–10.12°E, ~50.87–51.22°N

WGS84 conversion performed using GDAL/OGR (EPSG:31468 → EPSG:4326).

SOURCE FIELDS (ORIGINAL CSV)
------------------------------
  fid          Sequential feature ID
  HoleID       Drillhole identifier (35 unique holes, e.g. Ro15–Ro45, Kuechen, Quentel, Rohrbach)
  From         Interval start depth (metres downhole)
  To           Interval end depth (metres downhole)
  SampleID     Sample identifier
  Length_mm    Core sample length (millimetres)
  Cu_ppm       Copper assay result (ppm)
  Pb_ppm       Lead assay result (ppm)
  Zn_ppm       Zinc assay result (ppm)
  Ni_ppm       Nickel assay result (ppm) — partial population
  Co_ppm       Cobalt assay result (ppm) — partial population
  Ag_ppm       Silver assay result (ppm) — partial population
  Fe_pc        Iron assay result (percent)
  Cu_pc        Copper assay result (percent)
  mid_x        GK4 Easting of interval midpoint (metres)
  mid_y        GK4 Northing of interval midpoint (metres)
  mid_z        Elevation of interval midpoint (metres asl; negative = below surface)

BHP SCHEMA FIELDS ADDED AND POPULATED
--------------------------------------
  Field        Alias                      Source / Logic
  ───────────────────────────────────────────────────────────────────────────
  PROJECTCOD   ProjectCode                Fixed: "Tannenberg Copper Project"
  HOLEID       CAMPAIGNID                 Copied from HoleID
  SAMPLEID     SampleID                   Copied from SampleID
  SAMPLETYPE   SampleType                 Fixed: "Core"
  SapSubType   SampleSubType              Fixed: "Drill Core"
  Point_Type   Type of site               Fixed: "Drillhole"
  WGS84_CALX   LL_WGS84_X                 Longitude (°E) — GDAL EPSG:31468 → 4326
  WGS84_CALY   LL_WGS84_Y                 Latitude (°N)  — GDAL EPSG:31468 → 4326
  WGS84_CALZ   Elevation_masl             Copied from mid_z
  CoordSurv    Point_SurveyMethod         Fixed: "Downhole Survey"
  Cu_ppm       Cu_ppm_BESTEL              Copied from Cu_ppm (833/833 populated)
  Pb_ppm       Pb_ppm_BESTEL              Copied from Pb_ppm (833/833 populated)
  Zn_ppm       Zn_ppm_BESTEL              Copied from Zn_ppm (833/833 populated)
  Ni_ppm       Ni_ppm_BESTEL              Copied from Ni_ppm (158/833 populated)
  Co_ppm       Co_ppm_BESTEL              Copied from Co_ppm (158/833 populated)
  Ag_ppm       Ag_ppm_BESTEL              Copied from Ag_ppm (764/833 populated)
  Fe_pct       Fe_pct_BESTEL              Copied from Fe_pc (117/833 populated)

FIELDS LEFT EMPTY
-----------------
  PNTPROSPC    — no prospect codes in source
  SF_Observe, SurvInstr, SampleDate, SAMPLEDBY — not in source
  Lith1/2, LT_Color1/2, Lith_Desc — no lithology logged in source
  Alt_Assbl1, Alt1/2/3, Alt_Desc — no alteration data in source
  MN_Miner_1/2/3, Min_Desc — no mineralogy description in source
  Lab_L_D, Dsptch_L_D, SmpDspDate, Labjobno, SmpRetDate — lab dispatch not in source
  AnalysisLD, GenerMeth, SampWt_g_D, RecvdWt_g — not in source
  All _GMD, _LDD, _UDD detection limit fields — not available in source

ASSAY POPULATION SUMMARY
--------------------------
  Element     Intervals populated   Coverage
  ──────────────────────────────────────────
  Cu_ppm      833 / 833             100%
  Pb_ppm      833 / 833             100%
  Zn_ppm      833 / 833             100%
  Cu_pc       833 / 833             100%  (retained as source field)
  Ag_ppm      764 / 833              92%
  Ni_ppm      158 / 833              19%
  Co_ppm      158 / 833              19%
  Fe_pct      117 / 833              14%

DRILLHOLE SUMMARY
------------------
  35 unique drillholes: Ro15–Ro45 series, Kuechen, Quentel, Rohrbach, RO30
  All holes located in central Hesse, Germany (~9.62–10.12°E, ~50.87–51.22°N)
  Depth intervals range from surface to >470 m downhole

POPULATION STATISTICS
----------------------
  Total intervals     : 833
  BHP fields added    : ~60 (schema columns)
  Fields populated    : 17 with data
  WGS84 conversion    : 833/833 (100%)

================================================================================
