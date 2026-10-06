# 126 SAS Programming with Medicare Administrative Data

as the STUDY_AGE and AGE_CATS variables (kept from the ENR_CONTENT_2010_FNL file) and the TOT_AMB_SVC variable (kept from the ambulance utilization analytic file).

```
/ STEP 10.1: MERGE CONTINUOUSLY ENROLLED BENEFICIARIES WITH AMBULANCE
UTILIZATION DATA * */
proc format;
    value age_cats_fnt
    0='AGE LESS THAN 65'
    1='AGE BETWEEN 65 AND 74, INCLUSIVE'
    2='AGE BETWEEN 75 AND 84, INCLUSIVE'
    3='AGE BETWEEN 85 AND 94, INCLUSIVE'
    4='AGE GREATER THAN EQUAL TO 95';
run;

data fnl.present_amb(keep=bene_id tot_amb_svc study_age age_cats);
    merge enr.contentr_2010_fnl(in=a) utl.amb_util(in=b);
    by bene_id;
    if b;
n
run;
```

Next, in Step 10.2, we use ODS to present PROC SUMMARY of the beneficiaries with at least one claim for an ambulance service (using a 'where' clause that the value of TOT_AMB_SVC is not null), along with the number of ambulance services (the value of TOT_AMB_SVC variable) and the beneficiary's age category (the value of AGE_CATS). Note that we must first sort the file by AGE_CATS, and we utilize the formatting of the AGE_CATS variable in our presentation of the output.

```
* STEP 10.2: PRESENT MEASUREMENT OF AMBULANCE UTILIZATION */
proc sort data=fnl.present_amb;
    by age_cats;
run;

ods html file="C:\Users\mgillingham\Desktop\SAS
Book\FINAL_DATA_OUTPUT\Gillingham_fig10_2.html"
image_dpi=300 style=GrayscalePrinter;
ods graphics on / imagefmt=png;
title="LISTING OF BENEFICIARIES WITH AMBULANCE UTILIZATION GROUPED BY
AGE_CATS";

proc summary data=fnl.present_amb(where=(tot_amb_svc ne .)) print;
    var tot_amb_svc;
    by age_cats;
    format age_cats age_cats_fnt.;
run;
ods html close;
```