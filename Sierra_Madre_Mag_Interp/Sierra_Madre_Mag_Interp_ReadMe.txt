================================================================================
  README — Sierra Madre Mag interp.shp
  BHP Geological Interpretation Schema Population Summary
  Date: 2026-07-06
================================================================================

DATASET OVERVIEW
----------------
Name     : Sierra Madre Magnetic Interpretation
Source   : USGS EarthMRI / Wyoming State Geological Survey
Format   : ESRI Shapefile (Polygon)
CRS      : EPSG:26913 — NAD83 / UTM Zone 13N
Extent   : Sierra Madre Range, Wyoming, USA
Features : 245 polygons
Data Year: 2024

INTERPRETATION CONTEXT
-----------------------
This shapefile represents geological units interpreted from aeromagnetic survey
data over the Sierra Madre range, Wyoming. Polygons delineate crustal domains
identified through magnetic signature analysis. The Geophysica field records the
magnetic response characteristic of each unit (e.g. "Strongly magnetic, defining
the unit"), which was used to drive the InterpCof (confidence) field.

SOURCE FIELDS (ORIGINAL SHAPEFILE)
------------------------------------
  OBJECTID      Unique feature identifier
  Symbol_Ori    Original map symbol (may include overlay notation e.g. "Tha//Wg")
  Unit_Name     Name of the geological unit
  Unit_Descr    Detailed lithological description (truncated at 254 chars in DBF)
  Unit_Age      Age string (e.g. "Proterozoic | Mesoproterozoic (1415-1435 Ma)")
  Symbol        Simplified map symbol
  RuleID_1      Symbology rule ID
  SHAPE_Leng    Polygon perimeter (metres)
  SHAPE_Area    Polygon area (square metres)
  Geophysica    Magnetic character description

BHP SCHEMA FIELDS ADDED AND POPULATED
--------------------------------------
  Field        Alias                          Source / Logic
  ────────────────────────────────────────────────────────────────────────────
  Country      Country                        Fixed: "USA"
  Project      Project                        Fixed: "Sierra Madre Magnetic Interpretation"
  Area         Area                           SHAPE_Area converted to km²
  InterpFeat   Feature                        Fixed: "Geological Interpretation - Magnetics"
  InterpSour   Interpretation Source          Fixed: "Aeromagnetic Survey Interpretation"
  InterpAuth   Interpretation Author          Fixed: "USGS / Wyoming State Geological Survey"
  InterpCof    Interpretation Confidence      Derived from Geophysica field:
                                                "Strongly magnetic, defining" → High
                                                "Moderately magnetic"        → Moderate
                                                All others                   → Low
  RckClas      BHP_Rock Class                 Derived from Unit_Name (see logic below)
  RckClasCod   BHP_Rock Class_Code            PLU / MET / SED
  Comp         BHP Composition                Derived from Unit_Name
  Comp_Code    BHP_Composition_Code           FEL / INT / MAF / ULT
  RckEra       BHP Rock Era                   From age parsing of Unit_Age
  RckEraCod    BHP_Rock Era_Code              AR / PR / PP / MP / NP / CZ
  RckClasTyp   Rock Class/Rock Type           Copied from Geophysica (magnetic signature)
  Rock_Name    Rock Name                      Copied from Unit_Name
  Eon          Eon                            Parsed from Unit_Age
  Era          Era                            Parsed from Unit_Age
  Period       Period                         Parsed from Unit_Age where available
  Epoch        Epoch                          Parsed from Unit_Age where available
  Formation    Formation                      Copied from Unit_Name
  Age_MA       Age (Ma)                       Midpoint of age range
  Age_Min      Age Min (Ma)                   Minimum age boundary (Ma)
  Age_Max      Age Max (Ma)                   Maximum age boundary (Ma)
  MapScale     Map Scale                      Fixed: "1:500000"
  ConfRank     Confidence/Rank                Same as InterpCof (High/Moderate/Low)
  Year         Year                           Fixed: "2024"
  DataSource   Data Source                    Fixed: "USGS EarthMRI / Wyoming State Geological Survey"
  SourceLink   Source Link                    Fixed: "https://ngmdb.usgs.gov/emri/"

ROCK CLASSIFICATION LOGIC  (Unit_Name → RckClas / Comp)
---------------------------------------------------------
  Metamorphic (MET):
    metasedimentary, metavolcanic, schist, quartzite, marble, metaconglomerate,
    iron-formation, diamictite, amphibolite, hornblende gneiss, gneiss

  Sedimentary (SED):
    sandstone, shale, conglomerate, coal, arkosic, formation, claystone

  Plutonic (PLU):
    granite, granodiorite, quartz monzonite, quartz diorite, granitic,
    mafic intrusive, gabbro, diabase, ultramafic

  Composition:
    Felsic       — granite, granodiorite, quartz monzonite, granitic
    Intermediate — quartz diorite, diorite
    Mafic        — mafic, gabbro, amphibolite, basalt
    Ultramafic   — peridotite, dunite

AGE PARSING LOGIC  (Unit_Age → Eon/Era/Period/Epoch/Age_MA/Min/Max)
--------------------------------------------------------------------
  Unit_Age may be:
    - Simple term:         "Archean"
    - Compound:            "Archean-Late Proterozoic"
    - Pipe-delimited:      "Proterozoic | Mesoproterozoic (1415-1435 Ma)"
    - Explicit Ma range:   extracted directly where present (e.g. 1415-1435 Ma)

  Age boundaries used:
    Archean Early/Middle/Late : 4000–2500 Ma
    Paleoproterozoic          : 2500–1600 Ma
    Mesoproterozoic           : 1600–1000 Ma  (explicit if given)
    Neoproterozoic            : 1000–538 Ma
    Cenozoic / Paleocene      :   66–56 Ma
    Cenozoic / Eocene/Miocene :   56–5.3 Ma

UNIT CLASSIFICATION SUMMARY
-----------------------------
  Unit Name                                    RckClas      Comp          Era
  ──────────────────────────────────────────────────────────────────────────────
  Mafic intrusive rocks                        Plutonic     Mafic         Proterozoic
  Mafic metavolcanic rocks                     Metamorphic  Mafic         Proterozoic
  Metasedimentary and metavolcanic rocks       Metamorphic  —             —
  Metasedimentary rocks - Libby Creek Group    Metamorphic  —             Paleoproterozoic
  Metasedimentary rocks - Deep Lake Group      Metamorphic  —             Paleoproterozoic
  Bottle Creek Formation                       Sedimentary  —             Proterozoic
  Granite gneiss                               Metamorphic  Felsic        —
  Spring Lake granodiorite                     Plutonic     Felsic        —
  Granitic rocks of 1,700-Ma age group         Plutonic     Felsic        Paleoproterozoic
  Granitic rocks of 2,600-Ma age group         Plutonic     Felsic        —
  Quartz diorite                               Plutonic     Intermediate  Paleoproterozoic
  Sherman Granite                              Plutonic     Felsic        Proterozoic
  Hanna Formation                              Sedimentary  —             Cenozoic
  Hanna Formation overlaying ...               Sedimentary  varies        —
  Upper Miocene rocks overlaying granite gn.   Metamorphic  Felsic        —

FIELDS NOT POPULATED (no structured source data)
-------------------------------------------------
  StratUnit   — Stratigraphic unit; Unit_Name used as proxy in Formation
  SupGroup    — Supergroup; not available per polygon
  Group       — Group; not available per polygon

POPULATION STATISTICS
----------------------
  Total features     : 245
  BHP fields added   : 31
  Fields populated   : 28 / 31
  Fields left empty  : 3 (StratUnit, SupGroup, Group)
  Unique units       : 17

================================================================================
