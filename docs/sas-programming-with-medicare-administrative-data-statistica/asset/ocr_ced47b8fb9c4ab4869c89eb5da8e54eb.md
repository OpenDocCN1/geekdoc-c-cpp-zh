# 132 SAS Programming with Medicare Administrative Data

In Step 10.8, we add the beneficiary's state to the STAY_UTIL data by merging it with the ENR_CONTENTR_2010 FNL data set. We are presenting a summary of length of stay only for those beneficiaries with at least one inpatient, so we do not retain all beneficiaries in the ENR_CONTENTR_2010 FNL data set (i.e., we use an "in" merge to ensure only the one hospital stay). We call the output of FNL_PRESENT_IPLOS.

```
* 10.8: MERGE INPATIENT LENGTH OF STAY WITH BENEFICIARY SSA STATE INFORMATION */
data fnl.present_iplos(keep=bene_id stay_cnt_top_ip_los state);
	merge enr.contentr_2010 fnl(in=a) stay_util(in=b);
	b bene_id;
	if b;

run;
```

In Step 10.9, we sort the FNL_PRESENT_IPLOS data set in preparation for displaying data by state. Specifically, we sort the fnl.present_iplos by the variable STATE, which will be the 'by' variable in the PROC FREQ required in the next step.

```
* STEP 10.9: SORT BY SSA STATE IN PREPARATION FOR PRESENTATION OF IP LOS BY SSA STATE AND COUNTY */
proc sort data=fnl.present_iplos
	by state;

run;
```

Finally, in Step 10.10, we perform a PROC FREQ to output measurement of the average inpatient length of stay for each beneficiary (IP_LOS) by the name of state (STATE) associated with the beneficiary's SSA state code in the MBSF data. Once again, use ODS to output the PROC FREQ results to the same format where permanent data is stored for our work in this chapter. Note that we limit our frequency to the state of Michigan, and to values of IP_LOS between 1 and 5 days.

```
* STEP 10.10: PRESENT IP LOS INFORMATION BY BENEFICIARY SSA STATE */
ods file="c:\Users\gillingham\Desktop\SAS
book Final_DATA_OUTPUT=Gillingham_fig10_0.html"
image dpl=300 style=CrystalsiclePrinter;
	ods graphics on imagefmt=png;
	title "FREQUENCY OF IP LOS BY SSA STATE";
proc freq data=fnl.present_iplos(where=(state='MI' and 1<==ip_los<=5));
	tables ip_los;
	by state;

run;
ods html close;
```