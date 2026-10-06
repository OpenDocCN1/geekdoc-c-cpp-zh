# SAS Programming with Medicare Administrative Data

In Step 8.2, we summarize the E&M payments and services derived in Step 8.1 by beneficiary.
Specifically, we use PROC SQL to create a data set called CST.EM_COST_BENE to create two summary variables, EM TOTCOST_BENE (which summarizes the total payments for E&M services for each beneficiary) and EM TOTSVC_BENE (which summarizes the total count of E&M services for each beneficiary). This summarization is achieved by grouping the data by Bene ID. Note that both of the variables are created, we format the EM_TOTCOST_BENE variable to look like a dollar figure.

```
/* STEP 8.2; CALCULATE TOTAL E&M COSTS AND TOTAL E&M SERVICES BY
BENEFICIARY */
proc sql;
    create table cst.em_cost as
    select bene_id, sum(em_cost) as em_totcost_bene format=dollar15.2
    label='TOTAL E&M COST FOR THE BENE',
    sum(em_svc) as em_totsvc_bene label='TOTAL E&M SERVICES FOR
quit;
```

Output 8.1 shows the results of Step 8.2, printing just the first 10 observations for display purposes.

# Output 8.1: Total E&M Costs and Total E&M Services

TOTAL E&M COSTS AND SERVICES BY BENEFICIARY FOR BENEFICIARIES WITH AT LEAST ONE E&M SERVICE

| Bene_ID | em_totcost_bene | em_totsvc_bene |
|---|---|--|
| 1 | 00016745B629B9F | $80.00 | 1 |
| 2 | 0001FD7D2223DC | $0.00 | 0 |
| 3 | 0021CA6FF03E67 | $0.00 | 0 |
| 4 | 0002DAE1RC8CC70D | | 2 |
| 5 | 00030843E3ESB76 | $120.00 | 1 |
| 6 | 000497E2AAD63F | $0.00 | 0 |
| 7 | 0004FA0A83D5021D | $780.00 | 5 |
| 8 | 0005270573EA12A8 | $470.00 | 4 |
| 9 | 00070B63B73AE297 | $740.00 | 5 |
| 10 | 0007F12A492FD25D | $870.00 | 14 |

Finally, in Step 8.3, we summarize our E&M payment and service information, but do so only for the population of beneficiaries with at least one E&M service in a physician office setting, outputting a data set called CST.EM_COST to create distinct beneficiaries called EM_TOTBENE, and a summary of total payments called EM_TOTCOST. What's more, we perform a calculation using two of our created variables (EM_TOTBENE and EM_TOTCOST) to arrive at the average E&M payment for our population of beneficiaries with at least one E&M service, called EM_AVGCOST. We use a 'where' clause to ensure our output takes