================================================================================
  README — Sierra_Madre_interp_pl.shp
  BHP Geological Interpretation Schema — Litho-Magnetic Boundaries
  Date: 2026-07-06
================================================================================

DATASET OVERVIEW
----------------
Name     : Sierra Madre Litho-Magnetic Boundaries Interpretation
Source   : USGS EarthMRI / Wyoming State Geological Survey
Format   : ESRI Shapefile (Polygon) with spatial index (.sbn/.sbx)
CRS      : EPSG:26913 — NAD83 / UTM Zone 13N
Extent   : Sierra Madre Range, Wyoming, USA
Features : 245 polygons
Data Year: 2024

INTERPRETATION CONTEXT
-----------------------
This shapefile represents lithogeological domain boundaries interpreted by
integrating aeromagnetic survey data with existing geological mapping of the
Sierra Madre range. Unlike the "Sierra Madre Mag interp" layer (which reflects
purely magnetic domains), this layer defines Litho-Magnetic Boundaries —
polygons whose edges are constrained by both the magnetic signature and the
mapped geological lithology, producing a higher-fidelity interpretation of
subsurface rock unit extents.

The same 17 geological units are represented as in the magnetic interpretation
layer, but the polygon boundaries reflect the combined lithogeological and
geophysical evidence.

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
  Project      Project                        Fixed: "Sierra Madre Litho-Magnetic Boundaries"
  Area         Area (km²)                     SHAPE_Area ÷ 1,000,000
  InterpFeat   Feature                        Fixed: "Geological Interpretation - Litho-Magnetic Boundaries"
  InterpSour   Interpretation Source          Fixed: "Aeromagnetic Survey / Lithogeological Boundary Interpretation"
  InterpAuth   Interpretation Author          Fixed: "USGS / Wyoming State Geological Survey"
  InterpCof    Interpretation Confidence      Derived from Geophysica:
                                                "Strongly magnetic, defining" or "Strongly magnetic" → High
                                                "Moderately magnetic"                                → Moderate
                                                All others (Non magnetic, Weakly magnetic)           → Low
  RckClas      BHP_Rock Class                 From Unit_Name keyword match (see below)
  RckClasCod   BHP_Rock Class_Code            PLU / MET / SED
  Comp         BHP Composition                From Unit_Name keyword match
  Comp_Code    BHP_Composition_Code           FEL / INT / MAF / ULT
  RckEra       BHP Rock Era                   Derived from age parsing of Unit_Age
  RckEraCod    BHP_Rock Era_Code              AR / PR / PP / MP / NP / CZ
  RckClasTyp   Rock Class/Rock Type           Copied from Geophysica (magnetic character)
  Rock_Name    Rock Name                      Copied from Unit_Name
  Eon          Eon                            Parsed from Unit_Age
  Era          Era                            Parsed from Unit_Age
  Period       Period                         Parsed from Unit_Age where available
  Epoch        Epoch                          Parsed from Unit_Age where available
  StratUnit    Stratigraphic Unit             Copied from Unit_Name (full name)
  Group        Group                          Identified from Unit_Name:
                                                "Libby Creek Group" → Libby Creek Group
                                                "Deep Lake Group"   → Deep Lake Group
  Formation    Formation                      Identified from Unit_Name:
                                                Bottle Creek Formation, Hanna Formation,
                                                Sherman Granite, Spring Lake Granodiorite
  Age_MA       Age (Ma)                       Midpoint of parsed age range
  Age_Min      Age Min (Ma)                   Minimum age boundary (Ma)
  Age_Max      Age Max (Ma)                   Maximum age boundary (Ma)
  MapScale     Map Scale                      Fixed: "1:500000"
  ConfRank     Confidence/Rank                Same as InterpCof (High / Moderate / Low)
  Year         Year                           Fixed: "2024"
  DataSource   Data Source                    Fixed: "USGS EarthMRI / Wyoming State Geological Survey"
  SourceLink   Source Link                    Fixed: "https://ngmdb.usgs.gov/emri/"

ROCK CLASSIFICATION LOGIC  (Unit_Name → RckClas / Comp)
---------------------------------------------------------
  Metamorphic (MET): metasedimentary, metavolcanic, schist, quartzite, marble,
    metaconglomerate, iron-formation, diamictite, amphibolite, hornblende gneiss, gneiss
  Sedimentary (SED): sandstone, shale, conglomerate, coal, formation, claystone
  Plutonic    (PLU): granite, granodiorite, quartz monzonite, quartz diorite,
    granitic, mafic intrusive, gabbro, ultramafic

  Composition:
    Felsic       (FEL): granite, granodiorite, quartz monzonite, granitic
    Intermediate (INT): quartz diorite, diorite
    Mafic        (MAF): mafic, gabbro, amphibolite, basalt
    Ultramafic   (ULT): ultramafic, peridotite

AGE PARSING LOGIC  (Unit_Age → chronostratigraphic fields)
-----------------------------------------------------------
  Handles compound strings: "Archean-Middle Archean-Late", "Proterozoic | Mesoproterozoic (1415-1435 Ma)"
  Explicit Ma ranges extracted where present.
  Age boundaries (Ma):
    Archean:          4000–2500    Paleoproterozoic: 2500–1600
    Mesoproterozoic:  1600–1000    Neoproterozoic:   1000–538
    Cenozoic:         66–0         Paleocene:        66–56

UNIT SUMMARY
-------------
  Unit                                         RckClas      Comp          Era               Group / Formation
  ──────────────────────────────────────────────────────────────────────────────────────────────────────────
  Mafic intrusive rocks                        Plutonic     Mafic         Proterozoic
  Mafic metavolcanic rocks                     Metamorphic  Mafic         Proterozoic
  Metasedimentary and metavolcanic rocks       Metamorphic  —             —
  Metasedimentary rocks - Libby Creek Group    Metamorphic  —             Paleoproterozoic  Libby Creek Group
  Metasedimentary rocks - Deep Lake Group      Metamorphic  —             Paleoproterozoic  Deep Lake Group
  Bottle Creek Formation                       Sedimentary  —             Proterozoic       Bottle Creek Formation
  Granite gneiss                               Metamorphic  Felsic        —
  Spring Lake granodiorite                     Plutonic     Felsic        —                 Spring Lake Granodiorite
  Granitic rocks of 1,700-Ma age group         Plutonic     Felsic        Paleoproterozoic
  Granitic rocks of 2,600-Ma age group         Plutonic     Felsic        —
  Quartz diorite                               Plutonic     Intermediate  Paleoproterozoic
  Sherman Granite                              Plutonic     Felsic        Proterozoic       Sherman Granite
  Hanna Formation                              Sedimentary  —             Cenozoic          Hanna Formation
  Hanna Formation overlaying ...               Sedimentary  varies        —                 Hanna Formation
  Upper Miocene rocks overlaying granite gn.   Metamorphic  Felsic        —

RELATIONSHIP TO SIBLING LAYER
-------------------------------
  Sierra Madre Mag interp.shp  — Pure magnetic domain polygons (magnetic character only)
  Sierra_Madre_interp_pl.shp   — THIS FILE: Litho-Magnetic Boundary polygons (magnetic +
                                  lithogeological constraints combined)
  Both layers share the same 245 features and Unit_Name/Unit_Age/Geophysica values.
  The key difference is the polygon boundary geometry and the InterpFeat/InterpSour
  metadata fields reflecting the litho-magnetic interpretation method.

FIELDS NOT POPULATED
---------------------
  SupGroup — No supergroup-level classification available in source data

POPULATION STATISTICS
----------------------
  Total features     : 245
  BHP fields added   : 31
  Fields populated   : 30 / 31
  Fields left empty  : 1 (SupGroup)
  Unique units       : 17

================================================================================
