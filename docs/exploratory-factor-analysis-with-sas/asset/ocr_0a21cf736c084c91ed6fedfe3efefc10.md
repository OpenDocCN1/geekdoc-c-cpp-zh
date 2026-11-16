```
solve;
ods output Eigenvalues=boot_eigen
    OutlierRotFactPat=boot_loadings;
proc factor data=bootout_eqd nfactors=3 method=ml ULTRAHEYWOOD
    rotate=OLSIMIN ;
    by replicate;
    var Math: Par: Eng:;
run;
ods output close;run;
*Estimate CI for Eigenvalues and Corresponding Variance;
proc sort data=boot_eigen nodupkey;
    by Number Replicate;
run;
proc univariate data=boot_eigen;
    by Number;
    var Eigenvalue Proportion;
    Histogram;
    output out=ci_eigen pctlpts=2.5, 97.5 mean=Eigenvalue_mean
    Proportion_mean std=Eigenvalue_std Proportion_std
    pctlpre=Eigenvalue_ci Proportion_ci;
run;
```

Table 7.4 on page 134 shows the results for the eigenvalue estimates after changing our extraction method to ULS, and Table 7.5 on page 135 shows the results after using the ULTRAHEYWOOD option. Please note, the estimates that are produced by ML extraction are larger because a weighting process is used in ML. Thus, the relative difference in eigenvalue magnitude should be ignored when comparing these tables.

# Table 7.4 Results for the first four eigenvalues using ULS extraction

| Factor | Original Sample eigenvalue | Reduced Sample eigenvalue | 95% CI | Original Sample variance | Reduced Sample variance | 95% CI |
|---|---|---|---|---|---|---|
| 1 | 3.62 | 3.68 | (3.31,4.21) | 52.1% | 50.0% | (43.9%,54.6%) |
| 2 | 2.16 | 2.47 | (2.11,2.86) | 31.0% | 33.6% | (27.9%,37.2%) |
| 3 | 1.73 | 1.53 | (1.23,1.88) | 24.9% | 20.8% | (16.1%,24.3%) |
| 4 | 0.36 | 0.43 | (0.26,0.72) | 5.2% | 5.9% | (3.4%,9.5%) |