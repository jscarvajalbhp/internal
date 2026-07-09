================================================================================
  README — Litho_Tannenberg_BHP.csv
  BHP Drilling-Litho Schema Population
  Project: Tannenberg Copper Project
  Date: 2026-07-09
================================================================================

DATASET OVERVIEW
----------------
Name     : Tannenberg Copper Project — Core & Cuttings Lithostratigraphy
Source   : Tannenbergfield_Cores & cuttings in core storage HLNUG.xlsx (Sheet: Tabelle1)
Format   : CSV (comma-separated, UTF-8 with BOM)
CRS      : DHDN / Gauss-Krüger Zone 3 (EPSG:31467) — X/Y coordinates
Country  : Germany (central Hesse / Werra-Meissner region, ~9.6–10.1°E, 50.9–51.2°N)
Features : 58 drillhole/borehole records
Output   : Litho_Tannenberg_BHP.csv
Source   : HLNUG (Hessisches Landesamt für Naturschutz, Umwelt und Geologie)

COORDINATE SYSTEM
------------------
Source X/Y coordinates use DHDN/GK Zone 3 (EPSG:31467).
Leading digit "3" in Easting (~3,548,000–3,578,000 m) confirms Zone 3.
Confirmed by test transform: X=3,548,010 / Y=5,651,830 → lon=9.683°E, lat=50.999°N ✓
WGS84 conversion performed with GDAL/OGR (EPSG:31467 → EPSG:4326).

SOURCE FIELDS (ORIGINAL EXCEL)
--------------------------------
  SheetNo          Map sheet number (TK25 grid cell, e.g. 4924, 4925, 5024, 5025)
  Directory        HLNUG archive directory number
  SampleName_Orig  Full original borehole/core name including year and locality
  X_GK3            Easting (DHDN/GK Zone 3, metres)
  Y_GK3            Northing (DHDN/GK Zone 3, metres)
  TotalDepth_m     Total drilled depth (metres)
  Strat_DE         Original German stratigraphy description (retained unchanged)
  SampleType_DE    Original German sample type label
  CoreFrom_m       Core interval start depth (metres)
  CoreTo_m         Core interval end depth (metres)
  CuttingsFrom_m   Cuttings interval start depth (metres)
  CuttingsTo_m     Cuttings interval end depth (metres)

LEGEND (from source file, rows 66-71)
---------------------------------------
  KE  = Kern             → Core
  KEA = Kernauswahl      → Core (partial)
  SP  = Spülbohrung      → Cuttings
  SPA = Auswahlspülbohrung → Cuttings (partial)
  ME  = Meißelbohrung    → Cuttings rotary

BHP SCHEMA FIELDS ADDED
------------------------
  Field              Source / Logic
  ─────────────────────────────────────────────────────────────────────────
  HOLEID             Extracted from SampleName_Orig (text before first "(" or ",")
  PROJECTCOD         Fixed: "Tannenberg Copper Project"
  GEOLFROM           Core From depth if available, else Cuttings From
  GEOLTO             Core To depth if available, else Cuttings To
  PROSPECT           Empty — not specified in source
  PRIORITY           Fixed: 1 (primary log)
  Lith1              English translation of Strat_DE (see translation table below)
  Lith_Desc          Original German stratigraphy text (Strat_DE) — retained as-is
  HL_MesUnit         Fixed: "metres"
  GEOLFROM_Original  Same as GEOLFROM (original unit = metres)
  GEOLTO_Original    Same as GEOLTO
  WGS84_CALX         Longitude (°E) — transformed from X_GK3 via GDAL
  WGS84_CALY         Latitude (°N)  — transformed from Y_GK3 via GDAL
  COORD_SYST         Fixed: "DHDN / Gauss-Kruger Zone 3 (EPSG:31467)"
  SampleType_EN      English translation of SampleType_DE

FIELDS LEFT EMPTY
-----------------
  LT_Color1/2, Lith2, LT_GrnSize, LT_Texture — not in source
  LT_LogDate, LT_LogBy — not in source
  OSDU_Inges — not applicable

STRATIGRAPHIC TRANSLATION TABLE (German → English)
----------------------------------------------------
  Permian abbreviations:
    z   = Zechstein          r  = Roet (Upper Permian)
    z1  = Zechstein-1(Werra) z2 = Zechstein-2    z3 = Zechstein-3(Leine)
    z4  = Zechstein-4(Aller) z5 = Zechstein-5    z6 = Zechstein-6(Ohre)
    ro  = Roet(Perm-Trias transition)
    Werra-Sulfat = Werra Sulfate    Werra-Karbonat = Werra Carbonate
    Werra-Anhydrit = Werra Anhydrite   Werra-Tonstein = Werra Mudstone
    Leine-Karbonat = Leine Carbonate
    Weißliegend = Weissliegend    Rotliegend = Rotliegend
    Kupferschiefer/Kupfersfr = Kupferschiefer(Cu-shale)

  Triassic abbreviations:
    s   = Buntsandstein      su = Lower-Buntsandstein   suB = Lower-Buntsandstein(Broeckelschiefer)
    m   = Muschelkalk        mu = Lower-Muschelkalk      mm = Mid-Muschelkalk     mo = Upper-Muschelkalk
    so  = Upper-Muschelkalk(Lettenkeuper)     k = Keuper
    sm  = Mid-Muschelkalk    smV = Volpriehausen-Beds    smH = Heilbronn-Beds
    smD = Diemel-Beds        smS = Salinar-Mid-Muschelkalk
    soRö = Roet-Upper-Muschelkalk
    muOr = Orbicularis-Beds  muW3 = Wellenkalk-W3  muT = Trochitenkalk
    muW2 = Wellenkalk-W2     muOo = Oolithzone     muW1 = Wellenkalk-W1

  Zechstein cycles:
    zWAW = Werra-Anhydrite(z1)   zWCA = Werra-Carbonate(z1)
    zwT  = Werra-Clay(z1)        roW  = Roet-Werra-transition
    ZLTo = Leine-Clay(z3)        ZLCA = Leine-Carbonate(z3)
    zA   = Aller-cycle(z4)

  General:
    Quartär = Quaternary         Q  = Quaternary
    Trias   = Triassic           Perm = Permian
    Devon   = Devonian           Oberdevon = Upper Devonian
    Unterkarbon = Lower Carboniferous    Paläozoikum = Palaeozoic
    Kristallin = Crystalline basement   Schiefer = Schist/Slate
    Phyllit = Phyllite           Grauwacke = Greywacke
    Brekzie = Breccia            Konglomerat = Conglomerate
    Verwerfung = Fault zone      ET gekernt = cored by ET program

POPULATION STATISTICS
----------------------
  Total records       : 58
  BHP fields added    : 20+
  WGS84 conversion    : 58/58 (100%)
  Lith1 (EN trans.)   : 56/58 (2 have no stratigraphy in source)
  Fields left empty   : PROSPECT, LT_Color1/2, Lith2, LT_GrnSize,
                        LT_Texture, LT_LogDate, LT_LogBy, OSDU_Inges

================================================================================
