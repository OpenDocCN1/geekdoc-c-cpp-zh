# Display 3.15 Producing a horizontal bar chart using PROC SGPLOT

```
%let DATA_DIR = C:\Users\baileraj.IT\Desktop;
%let OLD_DIR = M:\public.www\classes\sta402\SAS-programs;

data nitro_tox;
    infile "&DATA_DIR\ch2-dat.txt"
          firstobs=16 expandtabs missover pad ;
    input @9 animal 2. @17 conc 3. @25 brood1 2.
          @33 brood2 2. @41 brood3 2. @49 total 2.;
run;

* ods rtf bodytitle file="&DATA_DIR\Display-3.15.rtf";
ods listing image dpi=300;
ods graphics / width=4.5in;
proc sgplot data=nitro_tox;  * Display 3.16;
    hbar conc / response=total stat=mean limits=both limitstat=stddev
                numstd=2;
run;

proc sgplot data=nitro_tox; * Display 3.17;
    dot animal / response=total group=conc;
run;

ods graphics off;
* ods rtf close;
```

The bar lengths in Display 3.16 correspond to the mean number of young produced (stat=mean) for each concentration (hbar conc). The limits extend to reflect a multiple of the standard deviation from the mean in each concentration (limitstat=stddev numstd=2). The limits could be modified to reflect a confidence interval for each unknown mean (limitstat=clm) if you wanted that information. So, when would you prefer which display? Hint: Do you want to describe the distribution of responses in a sample? Or. do you want to reflect the uncertainty when estimating an unknown population parameter?