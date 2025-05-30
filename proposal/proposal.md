Geographic Disparities in Access to Telemedicine Services
================
Shirisha Biyyala
2024-12-18

### Project Overview

#### Introduction and Background

The COVID-19 pandemic prompted an unprecedented surge in telemedicine
usage, transforming healthcare delivery across the United States.
However, access to telemedicine services has not been uniform across all
regions, creating potential disparities. This project aims to examine
these disparities using the Medicare Fee-For-Service Public Provider
Enrollment data, which contains detailed information on
Medicare-enrolled providers, their practice locations, and the
reassignment of benefits. The goal is to identify geographic patterns in
access to telemedicine services and highlight regions that may have been
underserved during the pandemic.

### Problem Statement

#### Define the Problem

Access to telemedicine services varies significantly across geographic
areas, leading to disparities that affect healthcare delivery and
outcomes. Factors contributing to these disparities may include the
distribution of telemedicine-capable providers, demographic
characteristics of the population, and provider enrollment
characteristics. Understanding these factors is crucial for addressing
inequities in healthcare access.

#### Project Objectives

- **Analyze Provider Distribution**: Examine the distribution of
  telemedicine-capable providers across different geographic regions
  (e.g., states, cities, zip codes).
- **Identify Disparities**: Investigate disparities in access to
  telemedicine services based on geographic, demographic, and
  provider-level variables.
- **Explore Provider Enrollment Characteristics**: Assess how provider
  type, specialty, and reassignment of benefits impact access to
  telemedicine.
- **Provide Policy Recommendations**: Offer actionable recommendations
  for healthcare policy that can improve telemedicine access in
  underserved areas.

### Data Source

This project will utilize several datasets to analyze geographic
disparities in access to telemedicine services. Each dataset provides
critical information necessary for understanding the landscape of
telemedicine providers and their service availability.

- **Source**: Provider Enrollment, Chain, and Ownership System (PECOS).
- **Link**: [Medicare Fee-For-Service Public Provider Enrollment
  Data](https://www.nber.org/research/data/medicare-fee-service-public-provider-enrollment-data)

#### Enrollment Data

**Description**: Contains comprehensive details about healthcare
practitioners enrolled in Medicare, including identification, names, and
provider types.

**File**: `/data/PPEF_Enrollment_Extract_2024.10.07.csv`

    ## Rows: 2,907,050
    ## Columns: 11
    ## $ NPI                <dbl> 1003879883, 1003976986, 1407802119, 1831165075, 185…
    ## $ PECOS_ASCT_CNTL_ID <chr> "8022920719", "7113839812", "8022920727", "51936378…
    ## $ ENRLMT_ID          <chr> "I20031103000001", "I20031103000005", "I20031103000…
    ## $ PROVIDER_TYPE_CD   <chr> "14-16", "14-68", "14-93", "14-16", "14-30", "14-35…
    ## $ PROVIDER_TYPE_DESC <chr> "PRACTITIONER - OBSTETRICS/GYNECOLOGY", "PRACTITION…
    ## $ STATE_CD           <chr> "PR", "PA", "PA", "PR", "KY", "NJ", "NJ", "NJ", "PR…
    ## $ FIRST_NAME         <chr> "ANTONIO", "CHRISTOPHER", "KADISHA", "JORGE", "RHON…
    ## $ MDL_NAME           <chr> NA, "J", "B", "A", "G", "J", NA, "D", NA, NA, NA, N…
    ## $ LAST_NAME          <chr> "ALVAREZ RODRIGUEZ", "ZIEGLER", "RAPP", "OSTOLAZA B…
    ## $ ORG_NAME           <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ GNDR_SW            <chr> "M", "M", "F", "M", "F", "M", "F", "M", "F", "M", "…

|                                                  |            |
|:-------------------------------------------------|:-----------|
| Name                                             | enrollment |
| Number of rows                                   | 2907050    |
| Number of columns                                | 11         |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |            |
| Column type frequency:                           |            |
| character                                        | 10         |
| numeric                                          | 1          |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |            |
| Group variables                                  | None       |

Data summary

**Variable type: character**

| skim_variable      | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:-------------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| PECOS_ASCT_CNTL_ID |         0 |          1.00 |  10 |  10 |     0 |  2431835 |          0 |
| ENRLMT_ID          |         0 |          1.00 |  15 |  15 |     0 |  2907050 |          0 |
| PROVIDER_TYPE_CD   |         0 |          1.00 |   5 |   5 |     0 |      319 |          0 |
| PROVIDER_TYPE_DESC |         0 |          1.00 |  20 |  92 |     0 |      319 |          0 |
| STATE_CD           |         0 |          1.00 |   2 |   2 |     0 |       56 |          0 |
| FIRST_NAME         |    442267 |          0.85 |   1 |  25 |     0 |   132941 |          0 |
| MDL_NAME           |   1304034 |          0.55 |   1 |  25 |     0 |    64218 |          0 |
| LAST_NAME          |    442275 |          0.85 |   1 |  35 |     0 |   403036 |          0 |
| ORG_NAME           |   2464811 |          0.15 |   3 |  70 |     0 |   300419 |          0 |
| GNDR_SW            |    884784 |          0.70 |   1 |   1 |     0 |        3 |          0 |

**Variable type: numeric**

| skim_variable | n_missing | complete_rate |       mean |        sd |        p0 |        p25 |        p50 |        p75 |      p100 | hist  |
|:--------------|----------:|--------------:|-----------:|----------:|----------:|-----------:|-----------:|-----------:|----------:|:------|
| NPI           |         0 |             1 | 1499801324 | 287973464 | 1.003e+09 | 1245943172 | 1497977718 | 1740984694 | 1.993e+09 | ▇▇▇▇▇ |

#### Practice Location Data

**Description**: Includes information about the locations where
practitioners operate, detailing the specific city, state, and ZIP code
of each practice.

**File**: `/data/PPEF_Practice_Location_Extract_2024.10.07.csv`

    ## Rows: 1,073,700
    ## Columns: 4
    ## $ ENRLMT_ID <chr> "I20031103000005", "I20031103000013", "I20031103000015", "I2…
    ## $ CITY_NAME <chr> "MECHANICSBURG", "SAN JUAN", "TOMS RIVER", "JERSEY CITY", "A…
    ## $ STATE_CD  <chr> "PA", "PR", "NJ", "NJ", "PR", "MI", "PR", "PR", "PR", "PR", …
    ## $ ZIP_CD    <chr> "170501925", "009175030", "08757", "073062305", "006055256",…

|                                                  |          |
|:-------------------------------------------------|:---------|
| Name                                             | location |
| Number of rows                                   | 1073700  |
| Number of columns                                | 4        |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |          |
| Column type frequency:                           |          |
| character                                        | 4        |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |          |
| Group variables                                  | None     |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| ENRLMT_ID     |         0 |             1 |  15 |  15 |     0 |   534477 |          0 |
| CITY_NAME     |         0 |             1 |   2 |  30 |     0 |    16187 |          0 |
| STATE_CD      |         0 |             1 |   2 |   2 |     0 |       57 |          0 |
| ZIP_CD        |         0 |             1 |   5 |   9 |     0 |   508857 |          0 |

#### Reassignment Data

**Description**: Provides details regarding the reassignment of benefits
for certain healthcare practitioners, highlighting their relationships
with other providers or entities.

**File**: `/data/PPEF_Reassignment_Extract_2024.10.07.csv`

    ## Rows: 3,301,706
    ## Columns: 2
    ## $ REASGN_BNFT_ENRLMT_ID <chr> "I20031103000001", "I20031103000001", "I20031103…
    ## $ RCV_BNFT_ENRLMT_ID    <chr> "O20031216000213", "O20111004000177", "O20040308…

|                                                  |              |
|:-------------------------------------------------|:-------------|
| Name                                             | reassignment |
| Number of rows                                   | 3301706      |
| Number of columns                                | 2            |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |              |
| Column type frequency:                           |              |
| character                                        | 2            |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |              |
| Group variables                                  | None         |

Data summary

**Variable type: character**

| skim_variable         | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:----------------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| REASGN_BNFT_ENRLMT_ID |         0 |             1 |  15 |  15 |     0 |  1976960 |          0 |
| RCV_BNFT_ENRLMT_ID    |         0 |             1 |  15 |  15 |     0 |   257695 |          0 |

#### Secondary Specialty Data

**Description**: Lists additional specialties that practitioners may
possess, expanding the understanding of the services they can provide.

**File**: `/data/PPEF_Secondary_Specialty_Extract_2024.10.07.csv`

    ## Rows: 507,127
    ## Columns: 3
    ## $ ENRLMT_ID          <chr> "I20031103000037", "I20031103000037", "I20031103000…
    ## $ PROVIDER_TYPE_CD   <chr> "14-11", "14-81", "14-19", "14-09", "14-30", "14-11…
    ## $ PROVIDER_TYPE_DESC <chr> "PRACTITIONER - INTERNAL MEDICINE", "PRACTITIONER -…

|                                                  |           |
|:-------------------------------------------------|:----------|
| Name                                             | secondary |
| Number of rows                                   | 507127    |
| Number of columns                                | 3         |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |           |
| Column type frequency:                           |           |
| character                                        | 3         |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |           |
| Group variables                                  | None      |

Data summary

**Variable type: character**

| skim_variable      | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:-------------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| ENRLMT_ID          |         0 |             1 |  15 |  15 |     0 |   451450 |          0 |
| PROVIDER_TYPE_CD   |         0 |             1 |   5 |   5 |     0 |      161 |          0 |
| PROVIDER_TYPE_DESC |         0 |             1 |  20 |  70 |     0 |      161 |          0 |

### Methodology

#### Data Preprocessing

- **Data Cleaning**: Conduct thorough cleaning of the dataset to
  eliminate inconsistencies or missing values, particularly in
  geographic identifiers (state, city, ZIP code).
- **Data Linking**: Link relevant fields such as Enrollment IDs,
  Provider Type Codes, and Practice Location information to create a
  cohesive dataset for analysis.

#### Exploratory Data Analysis (EDA)

- **Provider Distribution Analysis**: Analyze the number of
  telemedicine-capable providers across different geographic levels
  (state, city, ZIP code).
- **Providing Service Analysis**: Flag providers based on the presence
  of associated location and benefit reassignment data to categorize
  them into those providing telemedicine services and those not
  providing such services.

#### Geospatial Analysis

- **Mapping Provider Distribution**: Utilize GIS tools or mapping
  software (e.g., R libraries like `leaflet`, `arcgisbinding`, and
  `arcgisgeocoder`) to visually represent the distribution of
  telemedicine-capable providers.
- **Hotspot Analysis**: Identify geographic regions with high or low
  access to telemedicine services based on provider density.

#### Statistical Analysis

- **Regression Models**: Analyze relationships between provider
  characteristics (e.g., provider type, reassignment of benefits) and
  geographic disparities in access to telemedicine services.
- **Cluster Analysis**: Group regions based on similarities in provider
  availability to identify underserved areas.

### Anticipated Outcomes

- A detailed report highlighting geographic disparities in access to
  telemedicine services across the United States.
- Identification of specific regions and populations that face
  challenges in accessing telemedicine.
- Recommendations for policy interventions aimed at improving
  telemedicine access, ultimately contributing to enhanced healthcare
  equity.
