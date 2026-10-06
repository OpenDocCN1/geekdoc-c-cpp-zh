# Chapter 6: Working with Enrollment Data 65

In Step 6.10, we proceed to merge the county and state names onto our enrollment data. First, we sort the ENR.CONTENTR_2010 FNL set by SSA, and then we perform a partial merge of the ENR.CONTENTR_2010 FNL and the SRC.MSABEA_SSA data sets by SSA, keeping all of the data in our enrollment data set. In this way, we have assigned a state and county name to each beneficiary in our file of beneficiaries who were continuously enrolled in Medicare FFS throughout twelve months of 2010.

```
/* STEP 6.10: SORT CONTINUOUS ENROLLMENT DATA AND MERGE WITH MSABEA FILE */
proc sort data=enr.contentr_2010_fnl; by ssa; run;

data enr.contentr_2010_fnl;
  merge enr.contentr_2010_fnl(in=a) src.msabea_ssa(in=b);
  if a;
run;
```

Finally, in Step 6.11, we perform a simple print of the newly added state and county name variables in the ENR.CONTENTR_2010_FNL data set (displaying the first 10 records).

```
/* STEP 6.11: DISPLAY SSA STATE AND COUNTY NAMES IN 2010 ENROLLMENT DATA */
ods html file="C:\Users\mgillingham\Desktop\SASBook\FINAL_DATAVOD_OUTPUT\mgillingham_fig6_11.html"
image_dpi=300 style=GrayscalePrinter;
ods graphics on / imagefmt=png;
title "SSA STATE AND COUNTY NAMES IN 2010 DATA";
proc print data=enr.contentr_2010_fnl(obs=10);
  var bene_id ssa state county;
run;
ods html close;
```