
# Algorithms: Measuring Evaluation and Management Payments

We identified evaluation and management services in Chapter 7, but we did not retain the payment variables in our output. What's more, we searched our carrier claims for evidence of a single E&M service in a physician office setting for each beneficiary. Now, we want to identify payments for E&M services in a physician office setting for each beneficiary with at least one E&M service in a physician office setting as a whole. For the population of beneficiaries. The code we write will be straightforward. We will start by adding payments to our E&M algorithm that we developed in Chapter 7. Then, we will use PROC SQL to sum payments, and a DATA step to calculate payments per beneficiary.

In Step 8.1

```sas
* STEP 8.1: DEFINE EM CODES */
%let emcodes='99201','99202','99203','99204','99205','99211',
'99212','99213','99214','99215';
data em_cost (keep=bene_id expnsdt; prvnpi; linepmt; hcpcs_cd; em_svc em_cost);
  set util.carr_2010_fnl;
  array hcpcscd(13) hcpcs_cd-hcpcs_cd13;
  array prvpmt(13) linepmt1-linepmt3;
  retain em_svc em_cost;
  em_svc=0;
  em_cost=0;
  do i=1 to 13;
    if substr(hcpcscd(i),1,5) in (&emcodes) then do;
      em_svc=em_svc+1;
      em_cost=em_cost+prvpmt(i);
    end;
  end;
run;
```

# SAS Programming with Medicare Administrative Data

In Step 8.2, we summarize the E&M payments and services derived in Step 8.1 by beneficiary. Specifically, we use PROC SQL to create a data set called CST.EM_COST_BENE to create two summary variables, EM_TOTCOST_BENE (which summarizes the total payments for E&M services for each beneficiary) and EM_TOTVC_BENE (which summarizes the total count of E&M services for each beneficiary). This summarization is achieved by grouping the data by Bene ID. Note that both of the variables are created, we format the EM_TOTCOST_BENE variable to look like a dollar figure.

```sas
/* STEP 8.2; CALCULATE TOTAL E&M COSTS AND TOTAL E&M SERVICES BY
BENEFICIARY */
proc sql;
    create table cst.em_cost as
    select bene_id, sum(em_cost) as em_totcost_bene format=dollar15.2
    label='TOTAL E&M COST FOR THE BENE',
    sum(em_svc) as em_totsvc_bene label='TOTAL E&M SERVICES FOR';
quit;
```

Output 8.1 shows the results of Step 8.2, printing just the first 10 observations for display purposes.

# Output 8.1: Total E&M Costs and Total E&M Services

TOTAL E&M COSTS AND SERVICES BY BENEFICIARY FOR BENEFICIARIES WITH AT LEAST ONE E&M SERVICE

| Bene_ID | em_totcost_bene | em_totsvc_bene |
|---|---|---|
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

Finally, in Step 8.3, we summarize our E&M payment and service information, but do so only for the population of beneficiaries with at least one E&M service in a physician office setting, outputting a data set called CST.EM_COST to create distinct beneficiaries called EM_TOTBENE, and a summary of total payments called EM_TOTCOST. What's more, we perform a calculation using two of our created variables (EM_TOTBENE and EM_TOTCOST) to arrive at the average E&M payment for our population of beneficiaries with at least one E&M service, called EM_AVGCOST. We use a 'where' clause to ensure our output takes into account those beneficiaries with at least one E&M service in a physician office setting. We also label the variables we created, and format the payment and average payment calculations to look like dollars.

```sas
* STEP 8.3: CALCULATE TOTAL AND AVERAGE E&M COSTS FOR ALL BENEFICIARIES WITH AT LEAST ONE E&M SERVICE */
proc sql;
    create table cst.em_cost_all as
    select count(distinct bene_id) as em_totbene,
    sum(em_totcost_bene) as em_totcost format=dollar15.2 label='TOTAL E&M COST',
    (em_totcost/em_totbene) as em_avgcost format=dollar10.2 label='AVG E&M COST'
    from cst.em_cost_bene
    where em_totbene > 0;
quit;
```

Output 8.2 shows the result of Step 8.3.

# Output 8.2: Calculate Total and Average E&M Costs

CALCULATE TOTAL AND AVERAGE E&M COSTS FOR THE TOTAL POPULATION OF BENEFICIARIES WITH AT LEAST ONE E&M SERVICE

| em_totbene | em_totcost | em_avgcost |
|---|---|---|
| 1 | 47959 | $14,618,500.00 | $293.79 |

While Step 8.1 and Step 8.2 provide us with total E&M payments for each beneficiary, we can take this opportunity to arrive at the same information differently. In Chapter 7, we created claim files that contained the claim header-level and line-level information in a single record. We can use the line file to search for E&M codes and summarize them by beneficiary. Sure! In Step 8.4, we simply search the carrier data for evidence of E&M procedure codes. Then, we summarize the payment on each line using the LINEPMT variable. Note that we could easily limit our computation by using HPCS codes that represent an E&M service.

```sas
* STEP 8.4: CALCULATE TOTAL E&M COSTS BY BENEFICIARY USING THE CLAIM FILE */
proc sql;
    create table cst.em_cost_bene_line as
    select bene_id, sum(linepmt) as em_totcost_bene format=dollar15.2
    label='TOTAL E&M COST FOR THE BENE'
    from src.carrier_cd2010
    where hcpcs_cd in (&emcodes)
    group by bene_id
    order by bene_id;
quit;
```

Output 8.3 shows the results of Step 8.4, printing just the first 10 observations for display purposes. Note that the output of Step 8.4 is different from the output of Step 8.2. In the Exercises below, we ask why.

# Output 8.3: Total E&M Costs by Beneficiary Using the Claim Line File

TOTAL E&M COSTS BY BENEFICIARY USING THE CLAIM LINE FILE

| Obs | BENE_ID | em_totcost_bene |
|---|---|---|
| 1 | 00016F745862988 | $80.00 |
| 2 | 0002DAE1C8CC70D | $30.00 |
| 3 | 0002F8CE057345B | $910.00 |
| 4 | 000308435E3EB76 | $120.00 |
| 5 | 0005345A39D41C9 | $150.00 |
| 6 | 00048EF14791C68 | $160.00 |
| 7 | 0004F0ABD505251D | $780.00 |
| 8 | 000527052433A128 | $470.00 |
| 9 | 00070B63745BE497 | $740.00 |
| 10 | 0007F12A492FD25D | $870.00 |

# Algorithms: Measuring Inpatient Hospital Payments

In Chapter 7, we decided to treat the claims in inpatient claims data as stays, and for short-acute care hospitals. We will mine-level summary statistics, like average length of stay (ALOS), we use the total amount paid at the header of the claim to calculate the total amount paid by Medicare for a stay at an acute care facility or critical hospital. This is accomplished with slight modifications to the code we used to calculate E&M payments in Step 8.2 and Step 8.3.

In Step 8.5, we summarize total inpatient payments using the PMT_AMT variable in the inpatient claims data set for each beneficiary, outputting a variable called IP_TOTCOST_BENE (similar to the way we calculated total E&M payments for each beneficiary in Step 8.2). We output a data set CST_IP_COST_BENE. Note that this PMT_AMT variable is the amount paid by Medicare to the provider.

# Chapter 8: Measuring Costs

Occasionally, the reader may note the presence of negative payments in the inpatient claims. Recall that our work in Step 7.5 excluded negative amounts from the inpatient data set.

```sas
* STEP 8.5: CALCULATE TOTAL INPATIENT COSTS BY BENEFICIARY FOR
BENEFICIARIES AT LEAST ONE INPATIENT CLAIM */
proc sql;
    create table cst_ip_cost_bene_as
    select bene_id, sum(pmt_amt) as ip_tocost_bene format=dollar15.2
    label='TOTAL COST FOR THE BENE'
    from util.ip_2010_fnl
    group by bene_id;
quit;
```

Output 8.4 shows the results of Step 8.5, printing just the first 10 observations for display purposes.

# Output 8.4: Inpatient Costs by Beneficiary

TOTAL INPATIENT COSTS BY BENEFICIARIES WITH AT LEAST ONE INPATIENT CLAIM

| Obs | BENE_ID | ip_tocost_bene |
|---|---|---|
| 1 | 00016F74586298F | $16,000.00 |
| 2 | 0007F12A49FD25D | $43,000.00 |
| 3 | 00013E191IF37264 | $3,000.00 |
| 4 | 00196F0702489342 | $15,000.00 |
| 5 | 002353398A00234E | $10,000.00 |
| 6 | 00271F7D9C2B88A | $28,000.00 |
| 7 | 0028A2F2EC0CA0802 | $59,000.00 |
| 8 | 0029D3DBB23CE44 | $3,000.00 |
| 9 | 002B6020FF086ABA | $12,000.00 |
| 10 | 0049CB2A111F2225 | $6,000.00 |
