================================================================================
  README — mrds-trim-WY.shp
  BHP Mineral Occurrences Schema Population Summary
  Date: 2026-07-06
================================================================================

DATASET OVERVIEW
----------------
Name     : MRDS Wyoming Mineral Occurrences (trimmed)
Source   : USGS Mineral Resources Data System (MRDS)
           https://mrdata.usgs.gov/mrds/
Format   : ESRI Shapefile (Multi Point)
CRS      : EPSG:32613 — WGS 84 / UTM Zone 13N
Extent   : Wyoming, USA
Features : 5,189 mineral occurrence points

SOURCE FIELDS (ORIGINAL SHAPEFILE)
------------------------------------
  DEP_ID      Unique MRDS deposit identifier
  SITE_NAME   Name of the mineral occurrence / deposit / mine
  DEV_STAT    Development status (Occurrence, Prospect, Past Producer, Producer, Plant, Unknown)
  URL         USGS MRDS web link for the record
  CODE_LIST   Space-separated commodity codes (e.g. "AU CU MO")

BHP SCHEMA FIELDS ADDED AND POPULATED
--------------------------------------
  Field        Alias                    Source / Logic
  ────────────────────────────────────────────────────────────────────────────
  Country      Country                  Fixed: "USA"
  Project      Project                  Fixed: "Wyoming MRDS"
  Feature      Feature                  Fixed: "Mineral Occurrence"
  Area         Area                     Fixed: 0.0 (point dataset, no polygon area)
  RckClas      BHP_Rock Class           Derived from primary commodity code in CODE_LIST
  RckClasCod   BHP_Rock Class_Code      Plutonic=PLU, Volcanic=VOL, Sedimentary=SED,
                                        Metamorphic=MET, Hydrothermal=HYD, Unknown=UNK
  Comp         BHP Composition          Derived from primary commodity (Felsic/Intermediate/
                                        Mafic/Ultramafic where applicable)
  Comp_Code    BHP_Composition_Code     FEL / INT / MAF / ULT
  RckEra       BHP Rock Era             Era implied by deposit type / primary commodity
  RckEraCod    BHP_Rock Era_Code        AR=Archean, PR=Proterozoic, PH=Phanerozoic
  MnOccType    MineralOccType           Fixed: "Point" (MRDS is a point dataset)
  StrucName    StructureName            Copied from SITE_NAME
  MinOccStat   MineralOccStatus         Mapped from DEV_STAT:
                                          Occurrence → Occurrence
                                          Prospect   → Prospect
                                          Past Producer → Past Producer
                                          Producer   → Producer
                                          Plant      → Plant
                                          Unknown    → Unknown
  RckClasTyp   Rock Class/Rock Type     Combined deposit type label from top 2 commodities
  NameMinOcc   MineralOccurrence        Copied from SITE_NAME
  MnOccRock    Mineral_Occ_Rock_Type    Same as RckClas
  MnOccRockN   Mineral_Occ_RockName     Deposit type label derived from CODE_LIST
  DepType      DepositType              Deposit type from primary commodity code
  Eon          Eon                      Inferred from deposit/commodity era assignment
  Era          Era                      Inferred from deposit/commodity era assignment
  Period       Period                   Left blank (insufficient per-point data)
  Epoch        Epoch                    Left blank (insufficient per-point data)
  MapScale     Map Scale                Fixed: "1:500000"
  ConfRank     Confidence/Rank          Fixed: "Low" (point-level commodity info only)
  DataYear     Year                     Fixed: "2020" (MRDS last updated)
  DataSource   Data Source              Fixed: "USGS MRDS"
  SourceLink   Source Link              URL field if present; otherwise auto-built as:
                                        https://mrdata.usgs.gov/mrds/show-mrds.php?dep_id={DEP_ID}

COMMODITY CODE → BHP FIELD MAPPING LOGIC
-----------------------------------------
  The primary (first) commodity code in CODE_LIST drives the classification.
  Key mappings used:

  Code(s)          DepType                      RckClas      Comp         Era
  ───────────────────────────────────────────────────────────────────────────────
  AU               Lode Gold / Orogenic Au      Plutonic     Felsic       Cenozoic
  AG               Epithermal Ag-Au             Volcanic     Intermediate Mesozoic
  CU               Porphyry Cu / VMS            Plutonic     Intermediate Paleozoic
  MO               Porphyry Mo                  Plutonic     Felsic       Mesozoic
  FE               Iron Oxide                   Metamorphic  —            Archean
  TI / TI_M        Fe-Ti Oxide                  Plutonic     Mafic        Archean
  W                Skarn W                      Plutonic     Felsic       Mesozoic
  U                Sandstone-hosted U           Sedimentary  —            Cenozoic
  V                Sedimentary V                Sedimentary  —            Paleozoic
  P                Sedimentary Phosphate        Sedimentary  —            Mesozoic
  PB / ZN          MVT Pb-Zn                    Sedimentary  —            Paleozoic
  NI / CO          Magmatic Ni-Cu-PGE           Plutonic     Mafic        Archean
  PGE / PGE_PT/PD  Magmatic PGE                 Plutonic     Ultramafic   Archean
  REE / NB         Carbonatite REE              Plutonic     Ultramafic   Proterozoic
  CR               Chromite                     Plutonic     Ultramafic   Archean
  ABR_C / ABR_G    Industrial Abrasives         Metamorphic  —            Archean
  GEM / GEM_SP     Gemstone                     Metamorphic  —            Proterozoic
  SIL / CA         Silica / Carbonate           Sedimentary  —            Paleozoic
  LI               Pegmatite Li                 Plutonic     Felsic       Proterozoic
  (50+ codes total mapped)

FIELDS NOT POPULATED (insufficient per-point source data)
----------------------------------------------------------
  StrucLeng   — Line length; not applicable for point features
  StratUnit   — Stratigraphic unit; not in MRDS source
  SupGroup    — Supergroup; not in MRDS source
  GeoGroup    — Group; not in MRDS source
  Formation   — Formation; not in MRDS source
  Age_MA      — Geochronological age; not tabulated per point in MRDS
  Age_Min     — Minimum age; not tabulated per point in MRDS
  Age_Max     — Maximum age; not tabulated per point in MRDS

NOTE: Age and stratigraphic unit data could be cross-referenced with the
Wyoming State Geological Map (wygeol_dd_polygon.shp) by spatial join if needed.

POPULATION STATISTICS
----------------------
  Total features         : 5,189
  Commodity mapped       : 5,189  (100%)
  BHP schema fields added: 35
  Fields populated       : 27 / 35
  Fields left empty      : 8  (no structured per-point source data)

DEV_STAT BREAKDOWN
------------------
  Occurrence    : 2,201  (42.4%)
  Past Producer : 1,125  (21.7%)
  Unknown       :   800  (15.4%)
  Prospect      :   685  (13.2%)
  Producer      :   375   (7.2%)
  Plant         :     3   (0.1%)

================================================================================
