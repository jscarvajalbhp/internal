================================================================================
  README — Interval_T2_BHP.csv
  BHP Drilling-Assays Schema Population
  Project: Tannenberg Copper Project (Tannenberg 2 Area)
  Worksheet: "Interval"
  Date: 2026-07-09
================================================================================

DATASET OVERVIEW
----------------
Name     : Tannenberg 2 Area — Composited Interval Assays
Source   : Assays_HNLUG (Tannenberg 2 Area).xlsx — worksheet "Interval"
Format   : CSV (comma-separated, UTF-8 with BOM)
CRS      : NONE — this worksheet contains no coordinate columns
Country  : Germany (central Hesse — Tannenberg 2 area)
Features : 100 composited assay intervals (drillhole Ro23 and related holes)
Output   : Interval_T2_BHP.csv
Columns  : 394 (COMPLETE BHP Drilling-Assays schema, all fields present in
           schema order; fields with no source data are written empty)

NOTE ON COORDINATES
--------------------
The "Interval" worksheet does NOT contain mid_x / mid_y / mid_z columns, so
WGS84_CALX / WGS84_CALY / WGS84_CALZ are left blank. These are down-hole
composite intervals whose spatial position must be derived by joining to the
collar + downhole-survey data on HOLEID + From/To depths (not available in
this worksheet). CoordSurv is therefore also left blank.

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
    (e.g. Cu_pc=2 -> 20,000 ppm; Cu_pc=0.88 -> 8,800 ppm; Cu_pc=5 -> 50,000 ppm).
  Therefore NO numeric unit conversion was required.

SOURCE FIELDS (ORIGINAL WORKSHEET)
------------------------------------
  HoleID       Drillhole identifier (e.g. Ro23)
  From_m, To_m Interval start / end depth (metres downhole)
  SampleID     Sample identifier (e.g. Ro23-004)
  Cu_ppm ... Ag_ppm   Element assays (see unit table above)
  Fe_pc, Cu_pc       Iron and copper in percent
  Interval_cm  Interval length (centimetres)
  Interval_m   Interval length (metres) — only 6/100 populated in source

BHP SCHEMA FIELDS POPULATED
-----------------------------
  PROJECTCOD   Fixed: "Tannenberg Copper Project"
  HOLEID       From HoleID
  SAMPLEID     From SampleID
  SAMPLETYPE   Fixed: "Core"
  SapSubType   Fixed: "Drill Core"
  Point_Type   Fixed: "Drillhole"
  GEOLFROM/GEOLTO   From From_m/To_m (metres)
  Interval_cm  From Interval_cm (retained)
  Ag/Co/Cu/Ni/Pb/Zn_ppm, Fe_pct   Element results (units matched, see table)
  Cu_pct       Copper percent (retained from Cu_pc)
  WGS84_CALX/Y/Z, CoordSurv   BLANK (no coordinates in this worksheet)

ASSAY POPULATION SUMMARY
--------------------------
  Element     Populated     Coverage
  ------------------------------------
  Cu_ppm      93/100        93%
  Pb_ppm      93/100        93%
  Zn_ppm      93/100        93%
  Cu_pct      100/100       100%
  Ag_ppm      100/100       100%
  Ni_ppm      66/100        66%
  Co_ppm      66/100        66%
  Fe_pct      55/100        55%

COMPLETE SCHEMA OUTPUT
----------------------
The CSV contains ALL 394 Drilling-Assays schema fields, written in schema
order, so the file is a full/complete schema instance. Source data is mapped
into the matching fields (see above); every remaining field is present as a
column header with an empty value.

FIELDS PRESENT BUT LEFT EMPTY (no source data)
-----------------------------------------------
  PNTPROSPC, WGS84_CALX/Y/Z, CoordSurv, SF_Observe, SurvInstr, SampleDate,
  SAMPLEDBY, all lithology / alteration / mineralogy fields, all lab dispatch
  fields, all non-source element results, all _GMD / _LDD / _UDD detection-limit
  and generic-method fields, and all major-oxide fields (SiO2_p ... TOTAL_p).
  These are retained as empty columns for schema completeness.

POPULATION STATISTICS
----------------------
  Total intervals   : 100
  WGS84 conversion  : N/A (no source coordinates)
  Unit conversions  : 0 (all source units already match schema units)

================================================================================
