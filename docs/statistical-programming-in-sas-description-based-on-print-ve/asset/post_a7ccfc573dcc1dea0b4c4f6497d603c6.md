
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

## 8.10 Throw Out Your Tables of Statistical Distributions

In statistical applications, you might need to look up quantiles from reference distributions to define rejection regions or to determine multipliers of standard errors for constructing CIs. In addition, you might need to look up areas under distributions to construct p-values. Tables of quantiles and probabilities are often in the inside pages and appendices of introductory statistics books. The good news is that these tables can be replaced with functions in SAS, namely CDF and QUANTILE. The CDF function determines Pr(Y≤c), where Y is a random variable in a distribution. Continuous

distributions such as uniform, beta, chi-square, F, gamma, normal, t, and log-normal are included. Discrete distributions such as Bernoulli, binomial, Poisson, and negative binomial are also included. Here is the general syntax of the CDF function:

```
CDF('distribution-name', c, parameter-list-sep-commas)
```

where C = the value of the random variable.

The CDF function is a general way of requesting lower-tail probabilities. SAS has a number of different CDF-named functions that still work in SAS 9.2. For example, CDF('NORMAL',C) is equivalent to PROBNORM(C). CDF('T',C) is equivalent to PROBT(C). Display 8.50 shows the use of the CDF function for a variety of calculations. Pr(Z≤-1.645), Pr{ t[df=6] ≤ -1.645), Pr{ t[df=60] ≤ -1.645), and Pr{ t[df=600] ≤ -1.645) are calculated. (Question: Does t→Z as the degrees of freedom increases?) Pr(Y≤m) is calculated for m=0,1,2,3,4 when Y ~ binomial(n=trials=4 and prob of success=0.5). Pr(Y=m) is constructed as Pr(Y≤m)-Pr(Y≤ m-1) for m=1,2,3,4 and Pr(Y=0)=Pr(Y≤0). Try this at home: How would you determine P(0<Z<1.645) with these functions?

## Display 8.49 CDF function in SAS

```
data cdf_examples;

/* Z ~ N(0,1) table values */
 norm_area_left = cdf("Normal",-1.645);

 norm_area_right = 1-cdf("Normal",-1.645);  * area above -1.645 under N(0,1);

/* T ~ t(df) table values */
 t_area_left_06 = cdf("T",-1.645, 6);    * area <= -1.645 for t(df=6);
 t_area_left_60 = cdf("T",-1.645, 60);   * area <= -1.645 for t(df=60);
 t_area_left_600 = cdf("T",-1.645, 600); * area <= -1.645 for t(df=600);

/* Pr(Y<=m) for Y ~ binomial(m=successes, p=prob of success=0.5, n=4 trials) */
 bin_cdf_0 = CDF('binomial', 0, 0.50, 4);
 bin_cdf_1 = CDF('binomial', 1, 0.50, 4);
 bin_cdf_2 = CDF('binomial', 2, 0.50, 4);
 bin_cdf_3 = CDF('binomial', 3, 0.50, 4);
 bin_cdf_4 = CDF('binomial', 4, 0.50, 4);

 p0 = bin_cdf_0;           /* Pr(Y=m) for Y ~ binomial(p=0.5, n=4) */
 p1 = bin_cdf_1 - bin_cdf_0;
 p2 = bin_cdf_2 - bin_cdf_1;
 p3 = bin_cdf_3 - bin_cdf_2;
 p4 = bin_cdf_4 - bin_cdf_3;
 run;
 ods rtf bodytitle file="C:\Users\baileraj.IT\Desktop\Display-8-50.rtf";
 proc print data=cdf_examples;
 run;
 ods rtf close;
```

Probabilities calculated using the CDF function are shown in Display 8.50.

## Display 8.50 Output from PROC PRINT of normal and binomial CDF function

| norm_area_left | norm_area_right | t_area_left_06 | t_area_left_60 | t_area_left_600 |
|---|---|---|---|---|
| 0.049985 | 0.95002 | 0.075536 | 0.052600 | 0.050247 |

| bin_cdf_0 | bin_cdf_1 | bin_cdf_2 | bin_cdf_3 | bin_cdf_4 | p0 | p1 | p2 | p3 | p4 |
|---|---|---|---|---|---|---|---|---|---|
| 0.0625 | 0.3125 | 0.6875 | 0.9375 | 1 | 0.0625 | 0.25 | 0.375 | 0.25 | 0.0625 |

The difference in the values of CDF is used to calculate the probability of the five possible values of a binomial random variable when four trials are conducted. Calculating the probability mass function is unnecessary given other functions available in SAS. In fact, SAS provides a general function for obtaining the value of the probability density function (PDF) of a continuous random variable, or the value of the probability mass function (PMF) of a discrete random variable using the PDF function. Here is the general syntax of this function:

```
PDF('distribution-name', value-of-random-variable, parameter-list-sep-commas)
```

Many distributions can be used here. Display 8.51 shows a program that calculates Pr(Y=m) for m=0,1,2,3,4 for Y~binomial(n=4, π=0.5) and the value of the standard normal density at z=0 using the PDF function.

## Display 8.51 PDF and PMF functions

```
data pdf_examples;

/* Pr(Y=m) for Y ~ binomial(p=prob of success=0.5, n=4 trials) */
bin_0 = PDF('binomial', 0, 0.50, 4);
bin_1 = PDF('binomial', 1, 0.50, 4);
bin_2 = PDF('binomial', 2, 0.50, 4);
bin_3 = PDF('binomial', 3, 0.50, 4);
bin_4 = PDF('binomial', 4, 0.50, 4);

/* Z ~ N(0,1) value of phi(0) */
normal_density_0 = pdf("Normal", 0);
run;
ods rtf bodytitle file="C:\Users\baileraj.IT\Desktop\Display-8-52.rtf";
proc print data=pdf_examples;
run;
ods rtf close;
```

The probabilities and density produced by Display 8.51 are shown in Display 8.52. This display includes the binomial Pr(Y=m) and the standard normal density evaluated at z=0, normal_density_0 = 0.399 (= 1/√2π =0.399).

## Display 8.52 Output from PROC PRINT of normal and binomial PDF function

| bin_0 | bin_1 | bin_2 | bin_3 | bin_4 | normal_density_0 |
| 0.0625 | 0.25 | 0.375 | 0.25 | 0.0625 | 0.39894 |

Suppose you want to generate a graphical comparison of t(df=4) with a standard normal density. The following program might be useful.

## Display 8.53 Comparing a standard normal density to t₄

```
data t_vs_z;
 do x= -3.5 to 3.5 by .001;
  t4 = x;
  t_density = PDF('t', x, 4);
  z = x;
  z_density = PDF('Normal', x);
  output;
 end;
run;

ods rtf bodytitle file="C:\Users\baileraj.IT\Desktop\Display-8-54.rtf";

ods graphics on;
proc sgplot data=t_vs_z;
 label t_density="t[df=4] density";
 label z_density="N(0,1) density";
 series x=t4 y=t_density / curvelabel;
 series x=z y=z_density / curvelabel;
 xaxis label="value";
 yaxis label="density";
run;
ods graphics off;
ods rtf close;
```

Comparing the standard normal density to t₄ is shown in Display 8.54.

## Display 8.54 Plot comparing standard normal density to t₄

![](img/26474180ee55914c13fb9156a7678157_331_0.png)

The distributional QUANTILE function shouldn’t go unnoticed. This function returns the value of a random variable associated with a lower-tail probability. In other words, given a cumulative distribution function F(), its associated parameters, and a lower-tail probability, this function returns the value of x such that F(x) probability. Here is the syntax of this function:

```
QUANTILE('distribution-name', prob, parameter-list-sep-commas)
```

The parameter list varies with the distribution. The program in Display 8.55 determines quantiles from a continuous random variable (normal) and from a discrete random variable (binomial).

This output reinforces that zero can be written in ways that you do not expect. (Here, the numerical calculation of 0 was written as -1.15194E-17). Because the CDF of a discrete random variable is a step function, the quantiles do not necessarily change as the probability argument changes.

In this second program, quantiles for a t distribution with four degrees of freedom and for a z distribution are calculated for probabilities from 0.01 to 0.99 by 0.01. These quantiles are displayed in a series plot in Display 8.57.

## Display 8.57 Producing a Q-Q plot of t4 versus standard normal

```
data t vs z quant;
do prob = .01 to .99 by .01;
	t_quantile = QUANTILE('t', prob, 4);
	z_quantile = QUANTILE('Normal', prob);
	output;
end;
run;
```

```
ods rtf bodytitle file="C:\Users\bailera j.IT\Desktop\Display-8-58.rtf";
ods graphics on;
proc sgplot data=t_vs_z_quant;
	series x=z quantile y=t quantile;
	yaxis label="t[df=4] density";
	xaxis label ="N(0,1) density";
run;
ods graphics off;
ods rtf close;
```
