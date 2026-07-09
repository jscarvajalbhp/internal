================================================================================
  README — Collars_T2_BHP.csv
  BHP Drilling-Collar Schema Population
  Date: 2026-07-09
================================================================================

DATASET OVERVIEW
----------------
Name     : Drillhole Collar Dataset (T2)
Source   : Project internal CSV — Collars (T2).csv
Format   : CSV (comma-separated, UTF-8 with BOM)
CRS      : DHDN / Gauss-Krüger Zone 4 (EPSG:31468)
Country  : Germany (central region — Eschwege / Hesse area)
Features : 67 drillhole collars
Output   : Collars_T2_BHP.csv

COORDINATE SYSTEM IDENTIFICATION
----------------------------------
Source coordinates have Easting ~4.33–4.37 M and Northing ~5.64–5.68 M.
The leading digit "4" in the Easting encodes Gauss-Krüger Zone 4 (false easting
= 4,500,000 m). German terminology "nicht eingestuft" (= "unclassified") in
StratAtEOH and place names (Eschwege, Herlefeld) confirm central Germany.

Confirmed EPSG:31468 (DHDN/GK Zone 4) via test transformation:
  TH_740081  → lon=10.008°E, lat=51.221°N  ✓ (Eschwege region, Hesse)

WGS84 conversion performed using GDAL/OGR (OAMS_TRADITIONAL_GIS_ORDER).

SOURCE FIELDS (ORIGINAL CSV)
------------------------------
  HoleID       Drillhole identifier
  Easting      Easting coordinate (DHDN/GK Zone 4, metres)
  Northing     Northing coordinate (DHDN/GK Zone 4, metres)
  Elevation    Ground elevation (m above sea level)
  z_on_terra   Terrain surface elevation from DEM (m asl)
  MaxDepth     Total hole depth (metres)
  StratAtEOH   Stratigraphy at End of Hole ("nicht eingestuft" = unclassified)
  Class        Hole classification code (see mapping below)
  In_Licence   Whether within licence area (Yes / No / original)
  Dip          Hole dip angle (all 90° = vertical)
  DipDir       Dip direction azimuth (all 0° = vertical)

BHP SCHEMA FIELDS ADDED AND POPULATED
--------------------------------------
  Field        Alias                    Source / Logic
  ───────────────────────────────────────────────────────────────────────────
  HOLEID       HOLEID                   Copied from HoleID
  PROJECTCOD   PROJECTCODE              Fixed: "DESERTEX-DE"
  HOLETYPE     HOLETYPE                 Fixed: "DRILLHOLE"
  EASTING      X                        Copied from Easting (GK4 metres)
  NORTHING     Y                        Copied from Northing (GK4 metres)
  ELEVATION    Z                        Copied from Elevation (m asl)
  CORD_SYST    COORDINATE SYSTEM        Fixed: "DHDN / Gauss-Kruger Zone 4 (EPSG:31468)"
  WGS84_CALX   LL_WGS84_CALC_X          Longitude (°E) — transformed via GDAL EPSG:31468→4326
  WGS84_CALY   LL_WGS84_CALC_Y          Latitude (°N)  — transformed via GDAL EPSG:31468→4326
  WGS84_CALZ   LL_WGS84_CALC_Z          Copied from Elevation (elevation unchanged by transform)
  Depth_m_D    DEPTH_M                  Copied from MaxDepth (metres)
  PROSPECT     PROSPECT                 Empty — no prospect codes in source
  ColSurvMet   Collar_SurveyMeth        Fixed: "GPS" (assumed; no survey method in source)
  STARTDATE    STARTDATE                Empty — not available in source
  ENDDATE      ENDDATE                  Empty — not available in source
  DrillType    Drill_Type               Fixed: "DDH" (all holes vertical, presumed diamond)
  HoleStatus   Hole_Status              Mapped from Class field (see table below)
  HL_Comp      Company                  Empty — not available in source
  Col_Comm     Collar_Comments          Copied from StratAtEOH

CLASS → HOLESTATUS MAPPING
----------------------------
  Class value    HoleStatus
  ─────────────────────────
  Dead           Abandoned
  WS             Finished
  Mx at EOS      Finished
  Mx at SOS      Finished
  NA             Unknown
  ND             Unknown

WGS84 COORDINATE SAMPLE (first 5 holes)
-----------------------------------------
  HoleID          Longitude (°E)   Latitude (°N)
  ─────────────────────────────────────────────
  TH_740081       10.0080646       51.2210414
  Eschwege 2       9.9318561       51.2118040
  Herlefeld        9.7566783       51.0794774

FIELDS LEFT EMPTY
-----------------
  PROSPECT    — no prospect/target codes in source
  STARTDATE   — drilling dates not recorded in source
  ENDDATE     — drilling dates not recorded in source
  HL_Comp     — drilling company not recorded in source

POPULATION STATISTICS
----------------------
  Total collars       : 67
  BHP fields added    : 19
  Fields populated    : 15 / 19
  Fields empty        : 4  (PROSPECT, STARTDATE, ENDDATE, HL_Comp)
  WGS84 conversion    : 67/67 (100%)

================================================================================
