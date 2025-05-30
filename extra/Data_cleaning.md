Geographic Disparities in Access to Telemedicine Services in the
Post-COVID-19 Era
================
Shirisha Biyyala
2024-12-18

## 1. Libraries

All the required libraries are loaded for subsequent operations.

## 2. Datasets

    ## # A tibble: 6 × 11
    ##          NPI PECOS_ASCT_CNTL_ID ENRLMT_ID    PROVIDER_TYPE_CD PROVIDER_TYPE_DESC
    ##        <dbl> <chr>              <chr>        <chr>            <chr>             
    ## 1 1003879883 8022920719         I2003110300… 14-16            PRACTITIONER - OB…
    ## 2 1003976986 7113839812         I2003110300… 14-68            PRACTITIONER - CL…
    ## 3 1407802119 8022920727         I2003110300… 14-93            PRACTITIONER - EM…
    ## 4 1831165075 5193637890         I2003110300… 14-16            PRACTITIONER - OB…
    ## 5 1851357214 2466364161         I2003110300… 14-30            PRACTITIONER - DI…
    ## 6 1083766935 5092627794         I2003110300… 14-35            PRACTITIONER - CH…
    ## # ℹ 6 more variables: STATE_CD <chr>, FIRST_NAME <chr>, MDL_NAME <chr>,
    ## #   LAST_NAME <chr>, ORG_NAME <chr>, GNDR_SW <chr>

    ## # A tibble: 6 × 4
    ##   ENRLMT_ID       CITY_NAME     STATE_CD ZIP_CD   
    ##   <chr>           <chr>         <chr>    <chr>    
    ## 1 I20031103000005 MECHANICSBURG PA       170501925
    ## 2 I20031103000013 SAN JUAN      PR       009175030
    ## 3 I20031103000015 TOMS RIVER    NJ       08757    
    ## 4 I20031103000028 JERSEY CITY   NJ       073062305
    ## 5 I20031103000030 AGUADILLA     PR       006055256
    ## 6 I20031103000032 BINGHAM FARMS MI       480255810

    ## # A tibble: 6 × 2
    ##   REASGN_BNFT_ENRLMT_ID RCV_BNFT_ENRLMT_ID
    ##   <chr>                 <chr>             
    ## 1 I20031103000001       O20031216000213   
    ## 2 I20031103000001       O20111004000177   
    ## 3 I20031103000007       O20040308000883   
    ## 4 I20031103000007       O20051206000046   
    ## 5 I20031103000014       O20070303000050   
    ## 6 I20031103000014       O20221026001638

    ## # A tibble: 6 × 3
    ##   ENRLMT_ID       PROVIDER_TYPE_CD PROVIDER_TYPE_DESC                           
    ##   <chr>           <chr>            <chr>                                        
    ## 1 I20031103000037 14-11            PRACTITIONER - INTERNAL MEDICINE             
    ## 2 I20031103000037 14-81            PRACTITIONER - CRITICAL CARE (INTENSIVISTS)  
    ## 3 I20031103000039 14-19            PRACTITIONER - ORAL SURGERY                  
    ## 4 I20031103000089 14-09            PRACTITIONER - INTERVENTIONAL PAIN MANAGEMENT
    ## 5 I20031103000123 14-30            PRACTITIONER - DIAGNOSTIC RADIOLOGY          
    ## 6 I20031103000159 14-11            PRACTITIONER - INTERNAL MEDICINE

These datasets are now loaded into R from the `data` folder in the
repository. We can use them for exploration and further analysis.

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

    ## Rows: 1,073,700
    ## Columns: 4
    ## $ ENRLMT_ID <chr> "I20031103000005", "I20031103000013", "I20031103000015", "I2…
    ## $ CITY_NAME <chr> "MECHANICSBURG", "SAN JUAN", "TOMS RIVER", "JERSEY CITY", "A…
    ## $ STATE_CD  <chr> "PA", "PR", "NJ", "NJ", "PR", "MI", "PR", "PR", "PR", "PR", …
    ## $ ZIP_CD    <chr> "170501925", "009175030", "08757", "073062305", "006055256",…

    ## Rows: 3,301,706
    ## Columns: 2
    ## $ REASGN_BNFT_ENRLMT_ID <chr> "I20031103000001", "I20031103000001", "I20031103…
    ## $ RCV_BNFT_ENRLMT_ID    <chr> "O20031216000213", "O20111004000177", "O20040308…

    ## Rows: 507,127
    ## Columns: 3
    ## $ ENRLMT_ID          <chr> "I20031103000037", "I20031103000037", "I20031103000…
    ## $ PROVIDER_TYPE_CD   <chr> "14-11", "14-81", "14-19", "14-09", "14-30", "14-11…
    ## $ PROVIDER_TYPE_DESC <chr> "PRACTITIONER - INTERNAL MEDICINE", "PRACTITIONER -…

## 3. Data Cleaning

The column names of the `enrollment`, `location`, `reassignment`, and
`secondary` datasets were standardized using `clean_names()` to ensure
consistent formatting.

#### Enrollment Dataset:

- Duplicate rows were removed.
- The `org_name` column was dropped as it contained missing values and
  was deemed unnecessary for the analysis.
- Remaining rows with missing values were removed using `drop_na()`.

#### Location, Reassignment, and Secondary Datasets:

- Duplicates were removed.
- Rows with missing values were dropped.

<!-- -->

    ##  [1] "npi"                "pecos_asct_cntl_id" "enrlmt_id"         
    ##  [4] "provider_type_cd"   "provider_type_desc" "state_cd"          
    ##  [7] "first_name"         "mdl_name"           "last_name"         
    ## [10] "gndr_sw"

    ## [1] "enrlmt_id" "city_name" "state_cd"  "zip_cd"

    ## [1] "reasgn_bnft_enrlmt_id" "rcv_bnft_enrlmt_id"

    ## [1] "enrlmt_id"          "provider_type_cd"   "provider_type_desc"

#### Enrollment Dataset:

- `npi` was converted to a character type for consistency as it contains
  numerical IDs that should not be treated mathematically.
- `provider_type_cd` and `provider_type_desc` were converted to factors
  to represent categorical data.
- `state_cd` was converted to a factor for consistency in state
  representations.
- `gndr_sw` was recoded as a factor with labeled levels (“Female”,
  “Male”, “Unknown”).

#### Location Dataset:

- `state_cd` was converted to a factor for consistency.
- `zip_code` was extracted as the first five digits of the `zip_cd`
  column to standardize the format.

#### Reassignment Dataset:

- The column `reasgn_bnft_enrlmt_id` was renamed to `enrlmt_id` for
  consistency across datasets.

#### Secondary Dataset:

- `provider_type_cd` and `provider_type_desc` were converted to factors.

## 4. Data Preprocessing

    ##      npi            pecos_asct_cntl_id  enrlmt_id         provider_type_cd
    ##  Length:1377687     Length:1377687     Length:1377687     14-50  :207795  
    ##  Class :character   Class :character   Class :character   14-97  :109642  
    ##  Mode  :character   Mode  :character   Mode  :character   14-08  : 81232  
    ##                                                           14-11  : 75378  
    ##                                                           14-65  : 65223  
    ##                                                           14-80  : 53074  
    ##                                                           (Other):785343  
    ##                                              provider_type_desc
    ##  PRACTITIONER - NURSE PRACTITIONER                    :207795  
    ##  PRACTITIONER - PHYSICIAN ASSISTANT                   :109642  
    ##  PRACTITIONER - FAMILY PRACTICE                       : 81232  
    ##  PRACTITIONER - INTERNAL MEDICINE                     : 75378  
    ##  PRACTITIONER - PHYSICAL THERAPIST IN PRIVATE PRACTICE: 65223  
    ##  PRACTITIONER - CLINICAL SOCIAL WORKER                : 53074  
    ##  (Other)                                              :785343  
    ##     state_cd       first_name          mdl_name          last_name        
    ##  CA     :119789   Length:1377687     Length:1377687     Length:1377687    
    ##  TX     : 91813   Class :character   Class :character   Class :character  
    ##  NY     : 82485   Mode  :character   Mode  :character   Mode  :character  
    ##  FL     : 74224                                                           
    ##  PA     : 61323                                                           
    ##  NC     : 53531                                                           
    ##  (Other):894522                                                           
    ##     gndr_sw      
    ##  Female :714826  
    ##  Male   :660513  
    ##  Unknown:  2348  
    ##                  
    ##                  
    ##                  
    ## 

    ##   enrlmt_id          city_name            state_cd         zip_cd         
    ##  Length:1073700     Length:1073700     CA     : 98721   Length:1073700    
    ##  Class :character   Class :character   TX     : 92850   Class :character  
    ##  Mode  :character   Mode  :character   FL     : 89157   Mode  :character  
    ##                                        NY     : 75659                     
    ##                                        IL     : 47136                     
    ##                                        OH     : 40952                     
    ##                                        (Other):629225                     
    ##    zip_code        
    ##  Length:1073700    
    ##  Class :character  
    ##  Mode  :character  
    ##                    
    ##                    
    ##                    
    ## 

    ##   enrlmt_id         rcv_bnft_enrlmt_id
    ##  Length:3301706     Length:3301706    
    ##  Class :character   Class :character  
    ##  Mode  :character   Mode  :character

    ##   enrlmt_id         provider_type_cd                         provider_type_desc
    ##  Length:507127      14-11  :125117   PRACTITIONER - INTERNAL MEDICINE :125117  
    ##  Class :character   14-C5  : 40464   PRACTITIONER - DENTIST           : 40464  
    ##  Mode  :character   14-37  : 30329   PRACTITIONER - PEDIATRIC MEDICINE: 30329  
    ##                     14-08  : 27649   PRACTITIONER - FAMILY PRACTICE   : 27649  
    ##                     14-02  : 17892   PRACTITIONER - GENERAL SURGERY   : 17892  
    ##                     14-93  : 17838   PRACTITIONER - EMERGENCY MEDICINE: 17838  
    ##                     (Other):247838   (Other)                          :247838

    ##         enrlmt_id        npi pecos_asct_cntl_id provider_type_cd.x
    ## 1 I20031103000394 1790853083         1254243868              14-08
    ## 2 I20031104000436 1356302715         6507778826              14-08
    ## 3 I20031104000436 1356302715         6507778826              14-08
    ## 4 I20031105000008 1356436786         9537071832              14-01
    ## 5 I20031105000008 1356436786         9537071832              14-01
    ## 6 I20031105000008 1356436786         9537071832              14-01
    ##              provider_type_desc.x state_cd.x first_name mdl_name      last_name
    ## 1  PRACTITIONER - FAMILY PRACTICE         CA    CORINNE   VIVIAN          BASCH
    ## 2  PRACTITIONER - FAMILY PRACTICE         PA    PATRICK        T         WATERS
    ## 3  PRACTITIONER - FAMILY PRACTICE         PA    PATRICK        T         WATERS
    ## 4 PRACTITIONER - GENERAL PRACTICE         FL   HUMBERTO        R FERNANDEZ MIRO
    ## 5 PRACTITIONER - GENERAL PRACTICE         FL   HUMBERTO        R FERNANDEZ MIRO
    ## 6 PRACTITIONER - GENERAL PRACTICE         FL   HUMBERTO        R FERNANDEZ MIRO
    ##   gndr_sw         city_name state_cd.y    zip_cd zip_code rcv_bnft_enrlmt_id
    ## 1  Female            ARCATA         CA 955217474    95521    O20040121001146
    ## 2    Male HUNTINGDON VALLEY         PA 190067982    19006    O20050419000796
    ## 3    Male HUNTINGDON VALLEY         PA 190067982    19006    O20180308000694
    ## 4    Male             MIAMI         FL 331361115    33136    O20191111000864
    ## 5    Male           HIALEAH         FL 330133814    33013    O20200108000625
    ## 6    Male           HIALEAH         FL 330123113    33012    O20200108000625
    ##   provider_type_cd.y              provider_type_desc.y
    ## 1              14-01   PRACTITIONER - GENERAL PRACTICE
    ## 2              14-38 PRACTITIONER - GERIATRIC MEDICINE
    ## 3              14-38 PRACTITIONER - GERIATRIC MEDICINE
    ## 4              14-08    PRACTITIONER - FAMILY PRACTICE
    ## 5              14-08    PRACTITIONER - FAMILY PRACTICE
    ## 6              14-08    PRACTITIONER - FAMILY PRACTICE

    ## Rows: 11,932
    ## Columns: 17
    ## $ enrlmt_id            <chr> "I20031103000394", "I20031104000436", "I200311040…
    ## $ npi                  <chr> "1790853083", "1356302715", "1356302715", "135643…
    ## $ pecos_asct_cntl_id   <chr> "1254243868", "6507778826", "6507778826", "953707…
    ## $ provider_type_cd.x   <fct> 14-08, 14-08, 14-08, 14-01, 14-01, 14-01, 14-01, …
    ## $ provider_type_desc.x <fct> PRACTITIONER - FAMILY PRACTICE, PRACTITIONER - FA…
    ## $ state_cd.x           <fct> CA, PA, PA, FL, FL, FL, FL, FL, FL, FL, FL, FL, F…
    ## $ first_name           <chr> "CORINNE", "PATRICK", "PATRICK", "HUMBERTO", "HUM…
    ## $ mdl_name             <chr> "VIVIAN", "T", "T", "R", "R", "R", "R", "R", "R",…
    ## $ last_name            <chr> "BASCH", "WATERS", "WATERS", "FERNANDEZ MIRO", "F…
    ## $ gndr_sw              <fct> Female, Male, Male, Male, Male, Male, Male, Male,…
    ## $ city_name            <chr> "ARCATA", "HUNTINGDON VALLEY", "HUNTINGDON VALLEY…
    ## $ state_cd.y           <fct> CA, PA, PA, FL, FL, FL, FL, FL, FL, FL, FL, FL, F…
    ## $ zip_cd               <chr> "955217474", "190067982", "190067982", "331361115…
    ## $ zip_code             <chr> "95521", "19006", "19006", "33136", "33013", "330…
    ## $ rcv_bnft_enrlmt_id   <chr> "O20040121001146", "O20050419000796", "O201803080…
    ## $ provider_type_cd.y   <fct> 14-01, 14-38, 14-38, 14-08, 14-08, 14-08, 14-08, …
    ## $ provider_type_desc.y <fct> PRACTITIONER - GENERAL PRACTICE, PRACTITIONER - G…

    ##   enrlmt_id             npi            pecos_asct_cntl_id provider_type_cd.x
    ##  Length:11932       Length:11932       Length:11932       14-11  :1927      
    ##  Class :character   Class :character   Class :character   14-08  :1361      
    ##  Mode  :character   Mode  :character   Mode  :character   14-26  : 713      
    ##                                                           14-29  : 629      
    ##                                                           14-C6  : 559      
    ##                                                           14-06  : 555      
    ##                                                           (Other):6188      
    ##                                          provider_type_desc.x   state_cd.x  
    ##  PRACTITIONER - INTERNAL MEDICINE                  :1927      CA     :2806  
    ##  PRACTITIONER - FAMILY PRACTICE                    :1361      NY     :1593  
    ##  PRACTITIONER - PSYCHIATRY                         : 713      TX     :1229  
    ##  PRACTITIONER - PULMONARY DISEASE                  : 629      PR     : 655  
    ##  PRACTITIONER - HOSPITALIST                        : 559      FL     : 524  
    ##  PRACTITIONER - CARDIOVASCULAR DISEASE (CARDIOLOGY): 555      IL     : 512  
    ##  (Other)                                           :6188      (Other):4613  
    ##   first_name          mdl_name          last_name            gndr_sw    
    ##  Length:11932       Length:11932       Length:11932       Female :2005  
    ##  Class :character   Class :character   Class :character   Male   :9924  
    ##  Mode  :character   Mode  :character   Mode  :character   Unknown:   3  
    ##                                                                         
    ##                                                                         
    ##                                                                         
    ##                                                                         
    ##   city_name           state_cd.y      zip_cd            zip_code        
    ##  Length:11932       CA     :2806   Length:11932       Length:11932      
    ##  Class :character   NY     :1593   Class :character   Class :character  
    ##  Mode  :character   TX     :1229   Mode  :character   Mode  :character  
    ##                     PR     : 655                                        
    ##                     FL     : 524                                        
    ##                     IL     : 512                                        
    ##                     (Other):4613                                        
    ##  rcv_bnft_enrlmt_id provider_type_cd.y
    ##  Length:11932       14-11  :2646      
    ##  Class :character   14-08  : 683      
    ##  Mode  :character   14-93  : 680      
    ##                     14-01  : 636      
    ##                     14-38  : 479      
    ##                     14-81  : 438      
    ##                     (Other):6370      
    ##                                   provider_type_desc.y
    ##  PRACTITIONER - INTERNAL MEDICINE           :2646     
    ##  PRACTITIONER - FAMILY PRACTICE             : 683     
    ##  PRACTITIONER - EMERGENCY MEDICINE          : 680     
    ##  PRACTITIONER - GENERAL PRACTICE            : 636     
    ##  PRACTITIONER - GERIATRIC MEDICINE          : 479     
    ##  PRACTITIONER - CRITICAL CARE (INTENSIVISTS): 438     
    ##  (Other)                                    :6370

#### Enrollment and Location:

- Merged on the common key `enrlmt_id`.

#### Adding Reassignment Data:

- Merged the resulting dataset with the reassignment data using
  `enrlmt_id`.

#### Adding Secondary Specialty Data:

- Finally, merged the previous dataset with the secondary dataset using
  `enrlmt_id`.

<!-- -->

    ##         enrlmt_id        npi pecos_asct_cntl_id       provider_type_desc.before
    ## 1 I20031103000394 1790853083         1254243868  PRACTITIONER - FAMILY PRACTICE
    ## 2 I20031104000436 1356302715         6507778826  PRACTITIONER - FAMILY PRACTICE
    ## 3 I20031104000436 1356302715         6507778826  PRACTITIONER - FAMILY PRACTICE
    ## 4 I20031105000008 1356436786         9537071832 PRACTITIONER - GENERAL PRACTICE
    ## 5 I20031105000008 1356436786         9537071832 PRACTITIONER - GENERAL PRACTICE
    ## 6 I20031105000008 1356436786         9537071832 PRACTITIONER - GENERAL PRACTICE
    ##   state_cd.before first_name mdl_name      last_name gndr_sw         city_name
    ## 1              CA    CORINNE   VIVIAN          BASCH  Female            ARCATA
    ## 2              PA    PATRICK        T         WATERS    Male HUNTINGDON VALLEY
    ## 3              PA    PATRICK        T         WATERS    Male HUNTINGDON VALLEY
    ## 4              FL   HUMBERTO        R FERNANDEZ MIRO    Male             MIAMI
    ## 5              FL   HUMBERTO        R FERNANDEZ MIRO    Male           HIALEAH
    ## 6              FL   HUMBERTO        R FERNANDEZ MIRO    Male           HIALEAH
    ##   zip_code rcv_bnft_enrlmt_id          provider_type_desc.after state_cd.after
    ## 1    95521    O20040121001146   PRACTITIONER - GENERAL PRACTICE             CA
    ## 2    19006    O20050419000796 PRACTITIONER - GERIATRIC MEDICINE             PA
    ## 3    19006    O20180308000694 PRACTITIONER - GERIATRIC MEDICINE             PA
    ## 4    33136    O20191111000864    PRACTITIONER - FAMILY PRACTICE             FL
    ## 5    33013    O20200108000625    PRACTITIONER - FAMILY PRACTICE             FL
    ## 6    33012    O20200108000625    PRACTITIONER - FAMILY PRACTICE             FL

    ## Rows: 11,932
    ## Columns: 14
    ## $ enrlmt_id                 <chr> "I20031103000394", "I20031104000436", "I2003…
    ## $ npi                       <chr> "1790853083", "1356302715", "1356302715", "1…
    ## $ pecos_asct_cntl_id        <chr> "1254243868", "6507778826", "6507778826", "9…
    ## $ provider_type_desc.before <fct> PRACTITIONER - FAMILY PRACTICE, PRACTITIONER…
    ## $ state_cd.before           <fct> CA, PA, PA, FL, FL, FL, FL, FL, FL, FL, FL, …
    ## $ first_name                <chr> "CORINNE", "PATRICK", "PATRICK", "HUMBERTO",…
    ## $ mdl_name                  <chr> "VIVIAN", "T", "T", "R", "R", "R", "R", "R",…
    ## $ last_name                 <chr> "BASCH", "WATERS", "WATERS", "FERNANDEZ MIRO…
    ## $ gndr_sw                   <fct> Female, Male, Male, Male, Male, Male, Male, …
    ## $ city_name                 <chr> "ARCATA", "HUNTINGDON VALLEY", "HUNTINGDON V…
    ## $ zip_code                  <chr> "95521", "19006", "19006", "33136", "33013",…
    ## $ rcv_bnft_enrlmt_id        <chr> "O20040121001146", "O20050419000796", "O2018…
    ## $ provider_type_desc.after  <fct> PRACTITIONER - GENERAL PRACTICE, PRACTITIONE…
    ## $ state_cd.after            <fct> CA, PA, PA, FL, FL, FL, FL, FL, FL, FL, FL, …

## Summary of Resulting Dataset

The merged dataset contains 14 columns with cleaned and transformed
data. Key columns include:

- `provider_type_cd.before`, `provider_type_desc.before`, and
  `state_cd.before` (from the enrollment data).
- `city_name`, `zip_code`, and `state_cd.after` (from the location
  data).
- `rcv_bnft_enrlmt_id` (from the reassignment data).
- `provider_type_cd.after` and `provider_type_desc.after` (from the
  secondary data).

Rows with inconsistent or missing data were removed to ensure
high-quality and complete information.
