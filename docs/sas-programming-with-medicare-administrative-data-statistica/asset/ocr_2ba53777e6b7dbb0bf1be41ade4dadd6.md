# 50 SAS Programming with Medicare Administrative Data

Figure 5.2 is a single observation taken from the CARRIER2010LINE_WIDE data set for the same beneficiary displayed above. You can see that the procedure code and diagnosis code variables formerly stored in individual rows are now arrayed in a single row.

Figure 5.2: Transformed Carrier Line File

| Obs | BENE_ID | CLM_ID | hcps_cd1 | hcps_cd2 | hcps_cd3 | line_ic_dgns | line_ic_dgns_cd2 | line_ic_dgns_cd3 |
|---|---|---|---|---|---|---|---||}{
| 4 | 00016F745862898F | 88702338528164 | 99223 | 4048F | | 56211 | 56211 | 33818 |

In Step 5.3, we sort the base claim data set (SRC.CARRIER2010CLAIM) and the transformed claim line data set (CARRIER2010LINE_WIDE) by BENE_ID and CLM_ID in preparation for merging the two files to create a SAS data set that contains one record per base claim file, with all associated claim lines. We save the output of the sort of the carrier base claim file, named CARRIER2010CLAIM, to our work directory.

```
/* STEP 5.3: SORT BASE CLAIM AND TRANSFORMED LINE FILES IN PREPARATION
FOR MERGE */
proc sort data=src.carrier2010claim out=carrier2010claim;
  by bene_id clm_id;
run;

proc sort data=carrier2010line_wide;
  by bene_id clm_id;
run;
```

Figure 5.3 is a single observation taken from the CARRIER2010CLAIM data set for the same beneficiary displayed for Step 5.3 above.

Figure 5.3: Sorted Carrier Base Claim File

TRANSFORMED CARRIER BASE CLAIM FILE

| BENE_ID | CLM_ID | FROM_DT | THRU_DT |
|---|---|---|{}|
| 4 | 00016F745862898F | 88702338528164 | 20100529 | 20100529 |