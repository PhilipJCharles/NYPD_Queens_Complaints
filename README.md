# Queens Reported Crime Analysis

## Project Overview

This project analyzes **reported crime complaints in Queens** from January 2020 through the latest available reporting period in 2026.

The analysis focuses on:

- Changes in complaint volume
- Commonly reported offenses
- Offense severity
- Geographic distribution
- Recorded victim characteristics

> **Note:** Because the 2026 dataset contains only completed reporting quarters, 2026 results are treated as **year-to-date**. They are not directly compared with complete prior years unless the same reporting period is used for every year.

## Project Objectives

The primary questions addressed in this project are:

1. How did the total number of reported complaints change from 2020 through 2026 year-to-date?
2. Which offense descriptions had the highest number of reported complaints each year?
3. How were complaints distributed by recorded victim sex within each offense description?
4. Which Queens precincts recorded the highest number of complaints?
5. What percentage of complaints were classified as felonies, misdemeanors, or violations?

These objectives may be modified as the project develops and additional patterns are identified.

## Data Source

The data was obtained from the **New York City Police Department** through **NYC Open Data**.

The NYPD complaint datasets contain valid felony, misdemeanor, and violation crimes reported to the New York City Police Department.

Two complaint datasets were used:

- **NYPD Complaint Data Historic:** Contains complaint records through the most recent completed calendar year.
- **NYPD Complaint Data Current Year-to-Date:** Contains complaint records through the latest completed quarter of 2026.

The records represent crimes reported to and recorded by the NYPD. They do not necessarily represent every crime that occurred.

## Data Extraction

The original historic dataset contained more than **10 million records**.

The source data was queried and filtered before being exported to Excel using the following criteria:

- **Borough:** Queens
- **Reporting period:** 2020 through the latest available 2026 quarter

After filtering, approximately **677,000 complaint records** were extracted for analysis.

## Data Preparation

The following preparation steps were completed:

- Filtered the dataset to Queens.
- Filtered the reporting period to 2020–2026.
- Selected columns relevant to the project objectives.
- Renamed abbreviated source columns to improve readability.
- Removed columns that were outside the scope of the current analysis.

## Modified Column Names

| Original Column | Modified Column |
|---|---|
| `CMPLNT_NUM` | `Complaint_ID` |
| `CMPLNT_FR_DT` | `Incident_StartDate` |
| `CMPLNT_TO_DT` | `Incident_EndDate` |
| `CMPLNT_FR_TM` | `Incident_StartTime` |
| `CMPLNT_TO_TM` | `Incident_EndTime` |
| `BORO` | `Borough` |
| `RPT_DT` | `Reported_Date` |
| `ADDR_PCT_CD` | `Precinct_Code` |
| `KY_CD` | `Offense_Classification_Code` |
| `OFNS_DESC` | `Offense_Description` |
| `PD_CD` | `Detailed_Offense_Code` |
| `PD_DESC` | `Detailed_Offense_Description` |
| `CRM_ATPT_CPTD_CD` | `Crime_Completion_Status` |
| `LAW_CAT_CD` | `Offense_Severity` |
| `SUSP_AGE_GROUP` | `Suspect_Age_Group` |
| `SUSP_RACE` | `Suspect_Race` |
| `SUSP_SEX` | `Suspect_Sex` |
| `VIC_AGE_GROUP` | `Victim_Age_Group` |
| `VIC_RACE` | `Victim_Race` |
| `VIC_SEX` | `Victim_Sex` |

`LAW_CAT_CD` was renamed `Offense_Severity` because its values identify whether a complaint was classified as a:

- Felony
- Misdemeanor
- Violation

## Removed Columns

The following columns were removed because they were not required for the current project objectives:

- `PREM_TYP_DESC`
- `LOC_OF_OCCUR_DESC`
- `PARKS_NM`
- `HADEVELOPT`
- `STATION_NAME`
- `PATROL_BORO`
- `TRANSIT_DISTRICT`
- `X_COORD_CD`
- `Y_COORD_CD`
- `HOUSING_PSA`
- `Latitude`
- `Longitude`
- `Lat_Lon`

Latitude and longitude were removed because the current analysis uses police precincts rather than individual coordinate-level mapping.

These fields may be restored if geographic mapping is added later.

## Data Cleaning

The following data-cleaning and validation steps were performed on the Queens complaint dataset.

### Data-Type Standardization

- Converted `Incident_StartDate` from General to Date.
- Converted `Incident_EndDate` from General to Date.
- Converted `Incident_StartTime` from General to Time.
- Converted `Precinct_Code` from General to a standardized identifier format.
- Converted `Reported_Date` from General to Date.

### Identifier Standardization

- Removed unwanted punctuation from `Precinct_Code`.
- Removed unwanted punctuation from `Offense_Classification_Code`.
- Removed unwanted punctuation from `Detailed_Offense_Code`.
- Verified that code columns contained consistently formatted values.

### Missing-Value Standardization

Converted literal `(null)` values into blank cells in the following columns:

- `Incident_EndTime`
- `Crime_Completion_Status`
- `Suspect_Age_Group`
- `Suspect_Race`
- `Suspect_Sex`
- `Victim_Sex`

Standardized `UNKNOWN` values in the following columns:

- `Victim_Age_Group`
- `Victim_Race`

### Error Handling

- Identified `#VALUE!` errors in `Incident_StartDate`.
- Replaced invalid date errors with blank values so the column could be converted to a consistent date type.

### Duplicate Validation

- Checked `Complaint_ID` for duplicate values.
- No duplicate complaint IDs were found.

