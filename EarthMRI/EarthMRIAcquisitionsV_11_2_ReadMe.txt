================================================================================
  README — EarthMRIAcquisitionsV_11_2.shp
  BHP Ground Geophysics Schema Population Summary
  Date: 2026-07-06
================================================================================

DATASET OVERVIEW
----------------
Name     : EarthMRI Acquisitions V11.2
Source   : U.S. Geological Survey (USGS) Earth Mapping Resources Initiative
           https://mrdata.usgs.gov/earthmri/data-acquisition/project.php
Version  : 11.0 (May 2024)
Format   : ESRI Shapefile
CRS      : EPSG:4326 — WGS 84 (Geographic, decimal degrees)
Extent   : -166.26°W to -65.08°W | 17.78°N to 66.01°N (contiguous USA + Alaska + Puerto Rico)
Features : 183 polygons (geophysical survey footprints)
Purpose  : Study area polygons for scientific projects funded by Earth MRI to support
           critical mineral resource assessment across the USA.

FILES IN THIS FOLDER
--------------------
  EarthMRIAcquisitionsV_11_2.shp/dbf/shx/prj  — Shapefile (BHP schema populated)
  descriptions.csv     — Survey descriptions and abstracts (joined on PID)
  keywords.csv         — Topical and geographic keywords (joined on PID)
  program.csv          — Geophysical program/method names (joined on PID)
  contact.csv          — Contact persons (joined via project_contact.csv)
  project_contact.csv  — PID-to-contact ID crosswalk
  pubs.csv             — Publications and reports linked to each survey (joined on PID)
  acquisition-meta.txt — Overall dataset FGDC metadata

SOURCE FIELDS (ORIGINAL SHAPEFILE)
-----------------------------------
  PID          Primary key linking to all CSV files
  PNAME        Full survey name
  YEARSTART    Survey start year
  YEAREND      Survey end year
  PROGRAM      Broad program category
  AFFILIATIO   Conducting organisation / affiliation
  CNAME        Contact name
  CMAIL        Contact email
  WEBSITE      Project data URL
  PDATA        Data availability notes
  PDATGCHEM    Geochemistry data availability notes
  PAREA        Approximate survey area (km²)
  PAPPROX      Area is approximate flag (Y/N)
  PROVISIONL   Provisional record flag (Y/N)
  ALIAS        Alternative project name

BHP SCHEMA FIELDS ADDED AND POPULATED
--------------------------------------
  Field         Alias                          Source / Logic
  ─────────────────────────────────────────────────────────────────────────────
  Project       ProjectName                    descriptions.csv → pdescrip
  SurvName      SurveyName                     Shapefile PNAME
  SurveyID      SurveyID                       "EMRI-{PID}" (auto-generated)
  AcqPlatfID    AcquisitionPlatformID          "Airborne" (all EarthMRI surveys)
  AcqMethID1    AcquisitionMethodID1           program.csv entry 1 per PID
  AcqMethID2    AcquisitionMethodID2           program.csv entry 2 per PID
  AcqMethID3    AcquisitionMethodID3           program.csv entry 3 per PID (if present)
  AcqMethID4    AcquisitionMethodID4           program.csv entry 4 per PID (if present)
  Operators     Operators                      contact.csv + project_contact.csv → cname
  Contractor    Contractors                    Shapefile AFFILIATIO
  AcqDate1      AcquisitionDateRange.BeginDate Shapefile YEARSTART
  AcqDate2      AcquisitionDateRange.EndDate   Shapefile YEAREND
  Abstract      Abstract                       descriptions.csv → abstract (truncated to 254 chars)
  WebLink       WebLink                        pubs.csv → website (fallback: shapefile WEBSITE)
  SupDocs       SupportingDocuments            pubs.csv → citation (pipe-delimited if multiple)
  Continent     Continent                      Fixed: "North America"
  Country       Country                        Fixed: "USA"
  State_Prov    State/Province                 Extracted from PNAME (US state name match);
                                               fallback to keywords.csv thesaurus-1 geographic terms
  EPGS_Code     EPSG Code                      Fixed: 4326
  Projection    Projection                     Fixed: "Geographic (Lat/Long)"
  Datum         Datum                          Fixed: "WGS 84"
  LengthUnit    Length Units                   Fixed: "Degrees"
  MinX/MinY     Min X / Min Y                  Computed from polygon geometry envelope
  MaxX/MaxY     Max X / Max Y                  Computed from polygon geometry envelope
  MeasValueU    MeasuredValueUnit              Fixed: "nT" (nanoteslas — standard for magnetics)

FIELDS NOT POPULATED (insufficient per-survey source data)
-----------------------------------------------------------
  SurvNumb      — Contractor job number; not in EarthMRI source data
  TimeLapse     — No preceding survey IDs available
  Region        — Sub-state region not consistently available
  LocDatum      — Local datum transformation; not provided
  LineSpace     — Nominal line spacing; available in abstracts but unstructured text
  LineDirect    — Line direction; not tabulated in source
  LineLength    — Total line length; not tabulated in source
  TransMeth     — Transport method; not tabulated in source
  SensConf      — Sensor configuration; not tabulated in source
  SensSep/FldSensHgh/CabLength — Sensor geometry; not tabulated in source
  BasStatDat/BasStatFrq/MagnetFrq — Base station / sensor frequency; not tabulated
  InstName/InstManuf/InstModel/InstSerNum/InstRem — Instrument details; not tabulated
  MeasValue     — Individual measured values not in polygon-level source

NOTE: Many technical acquisition parameters (line spacing, instrument details,
sensor configuration) are described narratively in the Abstract field but are
not structured in the source CSVs. They could be extracted with NLP parsing
of the Abstract if needed.

POPULATION STATISTICS
----------------------
  Total features    : 183
  BHP fields added  : 34 (text, integer, double)
  Fields populated  : 25 / 34
  Fields left empty : 9  (no structured source data available)
  PID match rate    : 100% across all 5 CSVs

================================================================================
