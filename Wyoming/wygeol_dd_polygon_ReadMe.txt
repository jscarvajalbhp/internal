================================================================================
  README — wygeol_dd_polygon.shp  (Wyoming State Geological Map)
  BHP Schema Population Summary
  Date: 2026-07-06
================================================================================

SOURCE DATA
-----------
File      : wygeol_dd_polygon.shp (.dbf .shx .prj)
CRS       : EPSG:4267 — NAD27 (geographic, decimal degrees)
Extent    : -111.06°W to -104.05°W | 41.00°N to 45.01°N  (State of Wyoming, USA)
Features  : 17,346 polygons
DBF size  : 107 MB
Origin    : USGS / Wyoming State Geological Survey (SGMC)

SOURCE FIELDS USED FOR POPULATION
----------------------------------
  ORIG_LABEL  — Original unit label  → copied to ROCK_NAME
  UNIT_AGE    — Geological age text  → parsed for EON/ERA/PERIOD/EPOCH/AGE_MA/MIN/MAX
  ROCKTYPE1   — Primary lithology    → RCKCLAS, COMP, RCKCLASTYP
  ROCKTYPE2   — Secondary lithology  → included in RCKCLASTYP

AGE POPULATION LOGIC  (UNIT_AGE → chronostratigraphic fields)
--------------------------------------------------------------
  Reference: ICS Chronostratigraphic Chart 2024-12
  
  UNIT_AGE is free-text and may contain:
    - Single period:  "Miocene"
    - Range:          "Lower Cretaceous-Upper Cretaceous"
    - Compound range: "Jurassic(?) and Triassic(?) to Lower Cretaceous"
  
  Parsing steps:
    1. Qualifiers (?) removed.
    2. Text split on ' to ', ' and ', '-' to isolate individual period names.
    3. Each part matched against internal age table (oldest period → AGE_MAX,
       youngest period → AGE_MIN; midpoint → AGE_MA).
    4. EON/ERA/PERIOD/EPOCH derived from the oldest period in the range.
    5. RCKERA and RCKERACOD summarised at the Era level (e.g. Cenozoic / CZ).

  Key age boundaries used (Ma):
    Archean:          4000 – 2500   | Paleoproterozoic: 2500 – 1600
    Mesoproterozoic:  1600 – 1000   | Neoproterozoic:   1000 – 538
    Cambrian:          538 – 485    | Ordovician:        485 – 444
    Silurian:          444 – 419    | Devonian:          419 – 359
    Mississippian:     359 – 323    | Pennsylvanian:     323 – 299
    Permian:           299 – 252    | Triassic:          252 – 201
    Jurassic:          201 – 145    | Cretaceous:        145 – 66
    Paleocene:          66 – 56     | Eocene:             56 – 33.9
    Oligocene:        33.9 – 23     | Miocene:            23 – 5.3
    Pliocene:          5.3 – 2.58   | Pleistocene:       2.58 – 0.012
    Quaternary:        2.58 – 0     | Holocene:         0.012 – 0

ROCK CLASSIFICATION LOGIC  (ROCKTYPE1/2 → RCKCLAS/COMP)
---------------------------------------------------------
  RCKCLAS / Code:
    Plutonic  (PLU) — granite, granodiorite, granitoid, gabbroid, anorthosite,
                      alkalic intrusive rock, quartz diorite, quartz monzonite,
                      peridotite, plutonic rock (phaneritic), norite
    Volcanic  (VOL) — andesite, basalt, dacite, rhyolite, alkalic/intermediate/
                      felsic volcanic rock, lava flow, metavolcanic rock
    Sedimentary (SED) — clastic, carbonate, limestone, sandstone, mudstone,
                        claystone, conglomerate, dolostone, alluvium, gravel,
                        dune sand, glacial drift, mixed clastic/carbonate, playa,
                        landslide, colluvium, oil shale, coal, evaporite, loess
    Metamorphic (MET) — granitic gneiss, metasedimentary rock, migmatite,
                        metavolcanic rock

  COMP / Code:
    Felsic       (FEL) — granite, granodiorite, granitoid, rhyolite, dacite,
                         quartz monzonite, felsic/alkalic volcanic/intrusive
    Intermediate (INT) — andesite, intermediate volcanic rock, quartz diorite
    Mafic        (MAF) — basalt, gabbroid, anorthosite, norite
    Ultramafic   (ULT) — peridotite

  RCKCLASTYP — Combined label "Primary / Secondary" from ROCKTYPE1 + ROCKTYPE2

FIXED FIELDS (ALL 17,346 FEATURES)
------------------------------------
  COUNTRY    = USA
  PROJECT    = Wyoming State Map
  FEATURE    = Geology
  MAPSCALE   = 1:500000
  DATASOURCE = USGS / Wyoming State Geological Survey

POPULATION STATISTICS
----------------------
  Total features processed : 17,346
  Age fields populated      : 17,225  (99.3%)
  Rock fields classified    : 17,346  (100%)
  Features with no UNIT_AGE :    121   (0.7%) — mainly water bodies / ice

FIELDS NOT POPULATED (insufficient source data)
------------------------------------------------
  STRATUNIT, SUPGROUP, GROUP, FORMATION — require lithostratigraphic unit lookup
  CONFRANK   — requires qualitative assessment
  YEAR       — not provided in source metadata
  SOURCELINK — no direct URL per polygon in source data

================================================================================
