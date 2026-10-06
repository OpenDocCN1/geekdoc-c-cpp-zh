# Chapter 5: Request, Receive, Load, and Transform Data 51

In Step 5.4, we merge the CARRIER2010CLAIM and CARRIER2010LINE_WIDE files by the unique beneficiary identifier (**BENE_ID**) and the unique claim identifier (CLM_ID), using an “a and b” merge. We use a SAS data set called ETLARR_2010. This output carrier data set, by **BENE_ID**, will be used for identifying Part B carriers throughout the remainder of this book. Note that we output file called CARR_NOMATCH contains the records that did not match by **BENE_ID** and **CLM_ID** for quality assurance purposes (mismatches indicate a potential issue with the data or your).

```
* STEP 5.4: MERGE BASE CLAIM AND TRANSFORMED LINE FILES *\adata etl.carr_2010 carr_nomatch;
merge carrier2010claim(in=a) carrier2010line_wide(in=b);
  by bene_id clm_id;
  if a and b then output etl_carr_2010;
  else output carr_nomatch;
```

Figure 5.4 is a single record of the outputted ETLARR_2010 data set for the same beneficiary displayed above. We can see that the claim and line files have been merged such that one record per claim exists, whereas variables like procedure code and diagnosis code formerly stored in individual rows in the line file are now arranged in a single row, with the base detail of the dates on the claim (**FROM_DT** and **THRU_DT**).

# Figure 5.4: Merged Transformed Line and Base Claim Files

| Obs | BENE_ID | CLM_ID | hcpcs_cd1 | hcpcs_cd2 | hcpcs_cd3 | line_ic_dgns_cd1 | line_ic_dgns_cd2 | line_ic_dgns_cd3 | FROM_DT | THRU_DT |
|---|---|---|---|---|---|---|---|---|---|--|
| 4 | 0001847456286892 | 88072338578164 | 99223 | 4048 | 56211 | | 33818 | | 20100329 | 20100529 |

# Chapter Summary

In this chapter, we learned how to receive, load, and transform the Administrative claims and enrollment data we use to complete our research programming project. To this end, we discussed the following information:

+   - A request can take a lot of time and cost a lot of money to fulfill, so it is important to plan as much as possible before initiating our data request.
- Depending on the source of funding, there are several routes to procuring Medicare data for research purposes. We discussed CMS’s Integrated Data Repository (IDR), Data Extract System (DESY), and Virtual Research Data Center (VRDC). In addition, we discussed the Research Assistance Center (ResDAC), and CMS’s data distribution contractor.
- ResDAC and CMS’s data distribution contractor are the research community’s gateway to CMS data.