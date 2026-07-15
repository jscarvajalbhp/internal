================================================================================
  README — Assays_HNLUG_T2_BHP.csv
  BHP Drilling-Assays Schema Population
  Project: Tannenberg Copper Project (Tannenberg 2 Area)
  Worksheet: "Assays_HNLUG"
  Date: 2026-07-09
================================================================================

DATASET OVERVIEW
----------------
Name     : Tannenberg 2 Area — Downhole Assay Dataset (HLNUG)
Source   : Assays_HNLUG (Tannenberg 2 Area).xlsx — worksheet "Assays_HNLUG"
Format   : CSV (comma-separated, UTF-8 with BOM)
CRS      : DHDN / Gauss-Krüger Zone 4 (EPSG:31468) — mid_x/mid_y coordinates
Country  : Germany (central Hesse — Tannenberg 2 area)
Features : 833 assay intervals
Output   : Assays_HNLUG_T2_BHP.csv

COORDINATE SYSTEM
------------------
Source (mid_x, mid_y) are interval-midpoint coordinates in DHDN/GK Zone 4
(EPSG:31468). Leading digit "4" in the Easting (~4,348,000 m) confirms Zone 4.
  Test transform: mid_x=4,348,217.87 / mid_y=5,675,025.55
                  -> lon=9.82729°E, lat=51.19001°N  (central Hesse, Germany) OK
WGS84 conversion performed with GDAL/OGR (EPSG:31468 -> EPSG:4326).

UNIT MATCHING (source vs schema)  -- KEY CHECK
------------------------------------------------
  Source column   Unit      Schema field         Schema unit    Action
  ----------------------------------------------------------------------------
  Cu_ppm          ppm       Cu_ppm_BESTEL        ppm            Direct copy (match)
  Pb_ppm          ppm       Pb_ppm_BESTEL        ppm            Direct copy (match)
  Zn_ppm          ppm       Zn_ppm_BESTEL        ppm            Direct copy (match)
  Ni_ppm          ppm       Ni_ppm_BESTEL        ppm            Direct copy (match)
  Co_ppm          ppm       Co_ppm_BESTEL        ppm            Direct copy (match)
  Ag_ppm          ppm       Ag_ppm_BESTEL        ppm            Direct copy (match)
  Fe_pc           percent   Fe_pct_BESTEL        percent        Name map only (match)
  Cu_pc           percent   (no schema element)  percent        Retained as Cu_pct

  CONSISTENCY CHECK: Cu_ppm == Cu_pc x 10,000 verified across all rows
    (e.g. Cu_pc=0.532 -> 5,320 ppm vs Cu_ppm=5,315; Cu_pc=2 -> 20,000 ppm).
  Therefore NO numeric unit conversion was required. Cu is provided in BOTH
  ppm (schema field Cu_ppm) and percent (retained as Cu_pct for reference).

SOURCE FIELDS (ORIGINAL WORKSHEET)
------------------------------------
  HoleID       Drillhole identifier
  From, To     Interval start / end depth (metres downhole)
  Interval_cm  Sample interval length (centimetres)
  SampleID     Sample identifier (676/833 populated)
  Cu_ppm ... Ag_ppm   Element assays (see unit table above)
  Fe_pc, Cu_pc       Iron and copper in percent
  mid_x, mid_y, mid_z  Interval-midpoint GK4 Easting/Northing and elevation (m asl)

BHP SCHEMA FIELDS POPULATED
-----------------------------
  PROJECTCOD   Fixed: "Tannenberg Copper Project"
  HOLEID       From HoleID
  SAMPLEID     From SampleID
  SAMPLETYPE   Fixed: "Core"
  SapSubType   Fixed: "Drill Core"
  Point_Type   Fixed: "Drillhole"
  WGS84_CALX   Longitude (deg E) - transformed from mid_x
  WGS84_CALY   Latitude  (deg N) - transformed from mid_y
  WGS84_CALZ   From mid_z (m asl)
  CoordSurv    Fixed: "Downhole Survey"
  GEOLFROM/GEOLTO   From From/To (metres)
  Interval_cm  From Interval_cm (retained)
  Ag/Co/Cu/Ni/Pb/Zn_ppm, Fe_pct   Element results (units matched, see table)
  Cu_pct       Copper percent (retained from Cu_pc)

ASSAY POPULATION SUMMARY
--------------------------
  Element     Populated     Coverage
  ------------------------------------
  Cu_ppm      833/833       100%
  Pb_ppm      833/833       100%
  Zn_ppm      833/833       100%
  Cu_pct      833/833       100%
  Ag_ppm      764/833        92%
  Ni_ppm      158/833        19%
  Co_ppm      158/833        19%
  Fe_pct      117/833        14%

FIELDS LEFT EMPTY (not present in source)
-------------------------------------------
  PNTPROSPC, SF_Observe, SurvInstr, SampleDate, SAMPLEDBY,
  all lithology / alteration / mineralogy fields,
  all lab dispatch fields, all _GMD / _LDD / _UDD detection-limit fields.

POPULATION STATISTICS
----------------------
  Total intervals   : 833
  WGS84 conversion  : 833/833 (100%)
  Unit conversions  : 0 (all source units already match schema units)

================================================================================
