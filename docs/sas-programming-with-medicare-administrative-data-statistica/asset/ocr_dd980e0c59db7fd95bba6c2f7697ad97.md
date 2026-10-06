# Chapter 5: Request, Receive, Load, and Transform Data 49

```
array xexpnsdt2_(13) xexpnsdt2_1-expnsdt2_13;
array hcpcs_cd(13) hcpcs_cd1-hcpcs_cd13;
array xlinepmt(13) linepmt1-linepmt13;
array xprfnpi(13) prfnnpil1-prfnnpil13;
array xtax_num(13) tax_num1-tax_num13;
if first.clm_id then
    do i=1 to 13
        xline_icd_dgns_cd(clm_ln)='';
        xexpnsdt1_(clm_ln)=.;
        xexpnsdt2_(clm_ln)=.;
        hcpcs_cd(clm_ln)='';
        xlinepmt(clm_ln)=.;
        xprfnpi(clm_ln)='';
        xtax_num(clm_ln)='';
    end;

xline_icd_dgns_cd(clm_ln)=clm_id_dgns_cd;
xexpnsdt1_(clm_ln)=xexpnsdt1;
xexpnsdt2_(clm_ln)=xexpnsdt2;
hcpcs_cd(clm_ln)=hcpcs_cd;
xlinepmt(clm_ln)=linepmt;
xprfnpi(clm_ln)=prfnpi;
xtax_num(clm_ln)=tax_num;

if last.clm_id then output;
run;
```

Figure 5.1 shows the observations for a specific BENE_ID in the CARRIER2010LINE data set. Note how the variables that describe a service, like diagnosis code (LINE_ICD_DGNS_CD) variable, are stored as individual records for line numbers (CLM_LN) of the same claim (CLM_ID).

**Figure 5.1:** Sorted Carrier Line File

# SORTED CARRIER LINE FILE

| Obs | BENE_ID | CLM_ID | CLM_LN | LINE_ICD_DGNS_CD |
|---|---|---|---|---||
| 4 | 00016F745862988F | 887023385728164 | | 1 | 56211 |
| 5 | 00016F745862988F | 887023385728164 | | 2 | 56211 |
| 6 | 00016F745862988F | 887023385728164 | | 3 | 33818 |