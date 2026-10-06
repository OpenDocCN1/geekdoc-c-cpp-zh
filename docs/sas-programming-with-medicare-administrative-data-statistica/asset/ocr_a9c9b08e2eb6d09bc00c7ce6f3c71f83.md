Output 9.2: Frequency of EM Services

# FREQ OF EM SERVICES FOR BENEFICIARIES WITH DIABETES OR COPD

The FREQ Procedure

| Frequency | Table 1 of dia_flag by copd_flag | |
|---|---||
| Percent | Controlling for em_svc=1 | |
| Row Pct | copd_flag | |
| Col Pct | dia_flag | 0 | 1 | Total |
| | | 0 | 2113 | 2113 |
| | | 0.00 | 7.24 | 7.24 |
| | | 0.00 | 100.00 | |
| | | 0.00 | 37.46 | |
| | 1 | 23548 | 3528 | 27076 |
| | | 80.67 | 12.09 | 92.76 |
| | | 86.97 | 13.03 | |
| | | 100.00 | 62.54 | |
| Total | | 23548 | 5641 | 29189 |
| | | 80.67 | 19.33 | 100.00 |

# Algorithms: Diabetic Eye Exams for Beneficiaries with Diabetes

Now that we have a taste of using claims data to analyze services for beneficiaries with chronic conditions, let's search for evidence of eye exam services for the beneficiaries we identified as having diabetes. We will keep our example sample and use a small set of procedure codes to identify retinal eye exams (presented in the code below). However, it is possible to use additional codes, like ICD-9CM surgical codes. If we are calculating an official quality measure (e.g., an NCQA HEDIS measure), we must perform exclusions on our population of beneficiaries. However, for our purposes, a simple check of the carrier file will suffice; although it would be easy enough to apply this algorithm to other settings, using algorithms developed in this chapter.

In Step 9.6, we create a data set CND_EYE_DIA that contains the beneficiary identifier (BENE_ID) and a flag variable EYE_SYNC indicating whether we found evidence of an eye exam for this beneficiary in the carrier claims. First, we merge the data set created in Step 9.4 that identifies beneficiaries with diabetes or COPD (CND_DIA_COPD_COND) with the carrier claims data set (UTL_CARR_2010_FNL). Because we are interested in eye exams for beneficiaries identified as having diabetes, we subset the CND_DIA_COPD_COND data set with a 'where' clause specifying that we retain records where DIA_FLAG is equal to 1. From this point forward, it is a matter of executing code