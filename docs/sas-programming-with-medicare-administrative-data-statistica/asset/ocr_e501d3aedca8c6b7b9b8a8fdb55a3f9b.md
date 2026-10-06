Output 9.3 shows the first 10 observations of the output of Step 9.7.

**Output 9.3: Print of Beneficiaries Who Received Diabetic Eye Exams**

# ### PRINT OF BENEFICIARIES WHO RECEIVED DIABETIC EYE EXAMS**

| Obs | BENE_ID | eye_svc |
|---|---|--|
| 1 | 0004F0ABD505251D | 1 |
| 2 | 00052705243EA128 | 1 |
| 3 | 00070B63745BE497 | 1 |
| 4 | 0007F12A492FD25D | 1 |
| 5 | 0013E139F137264 | 1 |
| 6 | 00157F1570C74E09 | 1 |
| 7 | 001876C5D3F3F6A-A | 1 |
| 8 | 0018BD6F2F493452 | 1 |
| 9 | 00196F07022489342 | 1 |
| 10 | 001B371802E7EF58 | 1 |

# ## Algorithms: Hospital Readmissions for Beneficiaries with COPD**

Let's look for readmissions within 30 days of discharge for a hospitalization for any reason. As you advance your skills, you will be asked to program more complicated algorithms. For example, you may be asked to calculate readmission after a specific event, like a hospitalization for COPD or Acute Myocardial Infarction (AMI). In our case, we are simply looking for readmission within 30 days of any hospitalization for our population of beneficiaries identified as having COPD, so we do not need to worry about identifying any diagnosis codes. In some cases, the reader may wish to use both prior and subsequent years of data in order to identify admissions and subsequent readmissions that occurred later in the study year, well as early in the study year as a result of an admission in the year preceding the study year (in our case, calendar year 2010). For our simple instructional example, this will not be necessary.