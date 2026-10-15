# Display 8.48 (continued)

```
call streaminit(27549);

do i=1 to 4000;
    do ii = 1 to 31;
        ipick = int(31*RAND('uniform')+1);
        bage(ii) = age(ipick);
    end;
    boot_mean = mean(of bage1-bage31);      * calculate the test statistic;
    keep boot_mean;
    output boot_data;
end;

datalines;
44 40 44 42 38 47 40 43 44 38 44 45 45 47 54 49 51 51 48 49 57 54 52 50
51 54 51 57 49 48 52
run;

* select 5th and 95th percentiles from bootstrap distribution of the mean;
proc tabulate data=boot_data;
    var boot_mean;
    table boot_mean, P5 P95;
run;

ods graphics on;
proc sgplot data=boot_data;  * histogram of bootstrap means (not shown);
    histogram boot_mean;
run;
ods graphics off;

ODS RTF close;
```

The 90% t-based CI for the mean response is 46.09 to 49.27. The percentile-based bootstrap CI for the mean response is 46.19 to 49.19. An alternative to using DATA step programming to generate resamples is to use SAS procedures such as SURVEYSELECT (Wicklin 2008).

# 8.10 Throw Out Your Tables of Statistical Distributions

In statistical applications, you might need to look up quantiles from reference distributions to define rejection regions or to determine multipliers of standard errors for constructing CIs. In addition, you might need to look up areas under distributions to construct p-values. Tables of quantiles and probabilities are often in the inside pages and appendices of introductory statistics books. The good news is that these tables can be replaced with functions in SAS, namely CDF and QUANTILE. The CDF function determines Pr(Y≤c), where Y is a random variable in a distribution. Continuous