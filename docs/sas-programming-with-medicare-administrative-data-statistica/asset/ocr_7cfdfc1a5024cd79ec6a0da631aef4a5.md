# Chapter 9: Programming to Identify Chronic Conditions 111

In Step 9.2, we continue the process of identifying the presence of diagnosis codes used to identify diabetes or COPD, this time using our carriers data set. Again, we search each claim for diagnosis codes that indicate the presence of diabetes or COPD code value is found in one of the carrier's 13 line-level diagnosis codes (LINE_IC_DGNS CDI1-LINE_IC_DGNS_CD13), we set the relevant flag (DIA_CARR, COPD_CARR, or both) to 1. We output only those records where the flag variables are equal to 1. In Step 9.3 and 9.4, we will use these records to proof that the beneficiary has diabetes or COPD.

```
* STEP 9.2: SEARCH CARRIER CLAIMS FOR DIABETES AND COPD DIAGNOS CODES
*/
data cc_carr_search(keep=bene_id dia_carr copd_carr);
  set udln_2010 fnl;
  array indgns(13) line_ic_dgns cdl_line_ic_dgns_cd13;
  do i=1 to 3
    /* diabetes *
    if substr(indgns(i),1,4)=3572
    or substr(indgns(i),1,5)
    in('24900','24901','24910','24911','24920','24921','24930','24931',
  '24940','24950','24951','24960','24961','24970','24971',
  '24980','24981','24990','24991',
  '25000','25001','25002','25003','25010','25011','25012','25013',
  '25020','25021','25022','25023',
  '25030','25031','25032','25033','25040','25041','25042','25043',
  '25052','25051','25052','25053',
  '25060','25061','25062','25063','25070','25071','25072','25073',
  '25080','25081','25083',
  '25090','25091','25092','25093','36201','36202',
end dia_carr=1;
  /* copd *
  if substr(indgns(i),1,3)='496'
  or substr(indgns(i),1,4)='4910'
  '4911','4918','4919','4920','4928','4940','4941'
  or substr(indgns(i),1,5) in('49120','49121','49122') then
copd_carr=1;
  end;
  if dia_carr=1 or copd_carr=1;
run;
```

In Step 9.3, we use a macro to loop through all claims processed, summarizing the flags for each beneficiary by claim type, outputting one file for each relevant claim type (CC_NT_IP, CC_NT_SN, CC_NT_OP, CC_NT_HH, and CC_NT_CARR). In so, we create summary variables called DIA_IP_SUM, DIA_SN_SUM, DIA_OP_SUM, DIA_HH_SUM and DIA_CARR_SUM equal to the total number of claims with the presence of a diagnosis code for diabetes in the relevant claims set for each beneficiary. Similarly, we create summary variables called COPD_IP_SUM, COPD_OP_SUM, COPD_HH_SUM and COPD_CARR_SUM equal to the total