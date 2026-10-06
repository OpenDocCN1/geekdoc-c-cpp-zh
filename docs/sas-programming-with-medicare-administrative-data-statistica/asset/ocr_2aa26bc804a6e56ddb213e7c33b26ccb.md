# Chapter 7: Measuring Utilization of Services 73

loaded in Chapter 5 (except we do not use for our example research programming project) and the relevant enrollment data (ENR_CONTENT_2010_FNL) created in Chapter 6. Because we wish to eliminate all claims for beneficiaries who are not in our population, we must merge the data sets by the beneficiary identifier variable, BENE_ID. In order to make our algorithm run as quickly as possible, we want to be explicit about using the BENE_ID into memory when using our beneficiary data set. We can use the same code to limit each of our seven claims data set, we create a simple macro CLM LOOP that us delimiting. Using this macro allows us to avoid coding the merging algorithms all six times. Reducing the total lines of code we have to write saves development time and reduces the potential for coding errors. Note that we perform an “if a” merge, keeping only the records in a given data set that match the BENE_ID in our enrollment data.

```
* STEP 7: DELIMIT CLAIMS DATA BY BENEFICIARY POPULATION */
* CREATE MACRO LOOP TO PROCESS ALL SEVEN CLAIM TYPES */
%macro clm_loop(clmtyp=)
data data.util&clmtyp._2010_fnl;
merge enr.conterz_2010_fnl(keep=bene_id in=a)
etl.&clmtyp._2010(in=b)
  by bene_id;
  if a;
  run;
%end clm_loop
%clm_loop(clmtyp=c);
%clm_loop(clmtyp=dm);
%clm_loop(clmtyp=op);
%clm_loop(clmtyp=ip);
%clm_loop(clmtyp=sn);
%clm_loop(clmtyp=hh);
%clm_loop(clmtyp=hs)
```

# Algorithms: Measuring Evaluation and Management (E&M) Utilization

Let’s start our investigation of utilization characteristics for our population of continuously enrolled beneficiaries by measuring the number of E&M services in a physician office setting in 2010. In Step 7.2, we create a macro variable that identifies the E&M services we are measuring by looking for procedure code values beginning with “99” (indicating the “E&M” part of the criteria). We include the following procedure codes in the macro variable encodes: 99201, 99202, 99203, 99204, 99205, 99211, 99213, 99214, and 99215. You can learn more about the definitions of these procedure code values online, or by purchasing a procedure code terminology manual. Note that