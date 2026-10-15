confirms that two observations at each of the 10 values of predictor variable X are produced:

```
proc print data=simreg;
title " first 2 experiments from the SIMREG data set";
where iexpt<=2;
run;
```

The ODS OUTPUT selection extracts parameter estimates from the fitting of the 2000 regression data sets using PROC REG. The fits from the first two simulated samples that are output to the PARMEST data set are displayed using the following code:

```
proc print data=ParmEst;
title "first 2 experiments from the PARMEST data set";
where iexpt<=2;
var iexpt Variable Estimate;
run;
```

This code produces the following output:

| Obs | iexpt | Variable | Estimate |
| --- | ----- | -------- | -------- |
| 1 | 1 | Intercept | 3.89332 |
| 2 | 1 | x | 1.33037 |
| 3 | 2 | Intercept | 3.91362 |
| 4 | 2 | x | 1.25442 |

Each simulated sample leads to a model fit based on the two lines of the PARMEST data set that show the estimate associated with VARIABLE='INTERCEPT' as b0, and the estimate associated with VARIABLE=X as b1. This SAS log reports that 4000 lines of output are associated with the 2000 model fits.

```
NOTE: The data set WORK.PARMEST has 4000 observations and 9 variables.
```

DATA step programming is needed to extract the intercept estimate from one line and pair it with the slope estimate from the next line for each model fit. This is accomplished using the following code:

```
data ParmEst2; set ParmEst;
retain b0;
if variable="Intercept" then b0 = estimate;
else do;
b1 = estimate;
keep iexpt b0 b1;
output;
end;
run;
```