of the experimental units. Programming in a DATA step is used to assign TRT=1 to the first five labels in the permuted set. TRT=2 to the next five labels, etc. This data set is then transposed before printing the randomization.

# Display 3.34 Creating a randomization of four treatments to 20 experimental units (EUs)

```
%let DATA_DIR = C:\Users\baileraj.IT\Desktop;
proc plan seed=776655;
title "generate randomization/allocation";
title2 "assign: 4 treatments to 20 EUs";
factors EU=20;
output out=design_crd;
run;

data design_crd;
set design_crd;
if _n_ <= 5 then TRT=1;      * assign first 5 observations to trt 1;
else if _n_ <= 10 then TRT=2;  * assign next 5 obs. to trt 2;
else if _n_ <= 20 then TRT=3;  * assign next 5 obs. to trt 3;
else TRT=4;                   * assign last 5 obs. to trt 4;
run;

proc transpose data=design_crd out=t_design_crd prefix=C;
run;                          * transpose the data for printing;

ods rtf bodytitle file="&DATA_DIR\Display-3.34.rtf";
proc print data=t_design_crd;
run;
ods rtf close;
```

In Display 3.35, treatment 1 is assigned to experimental units with labels 3, 6, 12, 8, and 9. Treatment 2 is assigned to experimental units with labels 7, 13, 4, 18, and 1, and so on. While this randomization could have been implemented using DATA step programming, PROC PLAN can construct other more complicated experimental designs (e.g., randomized block designs, Latin squares, factorial experiments, etc.). Other SAS procedures for constructing experimental designs include FACTEX and OPTEX. Both of these procedures are part of SAS/QC software and can be used to construct a broader range of experimental designs (e.g., fractional factorial and optimal designs).