
**Basic Statistical Measures**

| Location | Value | Variability | Value |
|----------|-------|-------------|-------|
| Mean | 33.98333 | Std Deviation | 10.16890 |
| Median | 31.50000 | Variance | 103.40650 |
| Mode | 24.00000 | Range | 55.00000 |
| | | Interquartile Range | 13.00000 |

Note: The mode displayed is the smallest of 2 modes with a count of 5.

**Tests for Location: Mu0=0**

| Test | Statistic | p-Value |
|------|----------|---------|
| Student's t | t | Pr > |t| < .0001 |
| Sign | M | Pr >= |M| < .0001 |
| Signed Rank | S | Pr >= |S| < .0001 |

**Quantiles (Definition 5)**

| Quantile | Estimate |
|----------|----------|
| 100% Max | 67.0 |
| 99% | 67.0 |
| 95% | 54.5 |
| 90% | 48.5 |
| 75% Q3 | 40.0 |
| 50% Median | 31.5 |
| 25% Q1 | 27.0 |
| 10% | 24.0 |
| 5% | 23.0 |
| 1% | 12.0 |
| 0% Min | 12.0 |

| Extreme Observations | | | | | |
|---|---|---|---|---|---|
| Lowest | | | Highest | | |
| Value | city | Obs | Value | city | Obs |
| 12 | Minneapolis-St. Paul, MN-WI | 34 | 53 | Los Angeles, Long Beach, CA | 29 |
| 20 | Milwaukee, WI | 33 | 54 | New Orleans, LA | 37 |
| 23 | Utica-Rome, NY | 54 | 55 | Houston, TX | 25 |
| 23 | Albany-Schenectady-Troy, NY | 2 | 55 | San Diego, CA | 47 |
| 24 | Worcester, MA | 58 | 67 | Miami-Hialeah, FL | 32 |

## 3.10.1 PROC MEANS for descriptive statistics

Means and standard deviations are commonly calculated and reported for numeric variables. The MEANS procedure can calculate a variety of numeric summary statistics. In the following code, the default output statistics from PROC MEANS are requested for the total number of young produced in the nitrofen study. An option to limit the output to two decimal places (MAXDEC=2) is set. Furthermore, this analysis is conducted by levels of the concentration variable. The following code produces the output in Display 3.31:

```
proc means data=nitro_tox maxdec=2;
  class conc;
  var total;
run;
```

Display 3.31 Means, standard deviations, and extreme values for the total number of young in nitrofen study

| Analysis Variable: total | | | | | | |
|---|---|---|---|---|---|---|
| conc | N Obs | N | Mean | Std Dev | Minimum | Maximum |
| 0 | 10 | 10 | 31.40 | 3.60 | 24.00 | 36.00 |
| 80 | 10 | 10 | 31.50 | 3.27 | 26.00 | 36.00 |
| 160 | 10 | 10 | 28.30 | 2.36 | 23.00 | 31.00 |
| 235 | 10 | 10 | 17.20 | 5.90 | 7.00 | 27.00 |
| 310 | 10 | 10 | 6.00 | 3.71 | 0.00 | 15.00 |

You can customize statistical summaries in tabular output using PROC TABULATE, which is discussed in detail in Chapter 4.

## 3.11 Selecting a Simple Random Sample

Simple random samples can be selected using survey procedures. Suppose you want to select a sample of N=6 cities (without replacement) from the SMSA data set (which contains N=60 cities). The SURVEYSELECT procedure makes this a simple task. The program is shown in Display 3.32.

### Display 3.32 SAS program to select a simple random sample of N=6 cities selected from a data set containing N=60 cities

```
/*
  60 cities from the SMSA data set are read (cf. Display 2.8)
*/

%let DATA_DIR=C:\Users\baileraj.IT\Desktop;
options nodate nocenter nonumber;
data SMSA_from_txt;
  infile "C:\Users\baileraj\Desktop\SMSA-DASL-2space-sep.txt"
  firstobs=2;
  length city $ 39;
  input city & JanTemp JulyTemp RelHum Rain Mortality Education PopDensity pct_NonWhite pct_WC pop pop_per_house income HCPot NOxPot SO2Pot NOx;
run;

/* DEBUG option - print out N=60 observations in the SMSA data set */
/*
proc print data=SMSA_from_txt;
  var city JanTemp JulyTemp RelHum NOxPot SO2Pot NOx;
run;
*/

proc surveyselect data=SMSA_from_txt
  method=srs n=6 out=sample_SMSA_cities;
run;

ods rtf bodytitle file="&DATA_DIR\Display-3.32.rtf";
proc print data=sample_SMSA_cities;
  var city JanTemp JulyTemp RelHum NOxPot SO2Pot NOx;
run;
ods rtf close;
```

A data set containing the sample frame—a list of all population elements—is passed to PROC SURVEYSELECT as data=SMSA_from_txt. A simple random sample of a specified sample size is specified in method=srs n=6 with the resulting sample stored in the SAS data set specified by out=sample_SMSA_cities. The sample is printed in Display 3.33.

### Display 3.33 Simple random sample of N=6 cities selected from a data set containing N=60 cities

| Obs | city | JanTemp | JulyTemp | RelHum | NOxPot | SO2Pot | NOx |
|---|---|---|---|---|---|---|---|
| 1 | Baltimore, MD | 35 | 77 | 55 | 38 | 206 | 38 |
| 2 | Chattanooga, TN-GA | 42 | 79 | 56 | 8 | 27 | 8 |
| 3 | Miami-Hialeah, FL | 67 | 82 | 60 | 1 | 1 | 1 |
| 4 | Milwaukee, WI | 20 | 69 | 64 | 23 | 125 | 23 |
| 5 | Minneapolis-St. Paul, MN-WI | 12 | 73 | 58 | 11 | 26 | 11 |
| 6 | York, PA | 33 | 76 | 54 | 8 | 49 | 8 |

The SURVEYSELECT procedure can generate bootstrap samples. Cassell (2007) has a nice discussion of using PROC SURVEYSELECT in this way. In his discussion, the sampling with replacement uses the METHOD=URS option with PROC SURVEYSELECT and SAMPRATE=1 to implicitly define the bootstrap sample size to equal the original sample size. In Chapter 8, a percentile bootstrap is implemented using DATA step programming.

## 3.12 Randomly Assigning Treatments to Observations

The random assignment of treatments to experimental units is a fundamental exercise in statistics. So, it should be no surprise that this can be readily accomplished in SAS. Suppose you are conducting an experiment with four treatments. You decide that five replicate observations should be in each treatment. Assume that the four treatments are assigned to a pool of 20 experimental units labeled 1 through 20. The PLAN procedure in Display 3.34 is invoked to create a permutation of the integers 1 through 20—the labels

of the experimental units. Programming in a DATA step is used to assign TRT=1 to the first five labels in the permuted set. TRT=2 to the next five labels, etc. This data set is then transposed before printing the randomization.

### Display 3.34 Creating a randomization of four treatments to 20 experimental units (EUs)

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

### Display 3.35 Randomization of four treatments to 20 experimental units (EUs) using PROC PLAN

generate randomization/allocation
assign: 4 treatments to 20 EUs

| Obs | _NAME_ | C1 | C2 | C3 | C4 | C5 | C6 | C7 | C8 | C9 | C10 | C11 | C12 | C13 | C14 | C15 | C16 | C17 | C18 | C19 | C20 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | EU | 3 | 6 | 12 | 8 | 9 | 7 | 13 | 4 | 18 | 1 | 19 | 17 | 20 | 15 | 10 | 16 | 5 | 14 | 11 | 2 |
| 2 | TRT | 1 | 1 | 1 | 1 | 1 | 2 | 2 | 2 | 2 | 2 | 3 | 3 | 3 | 3 | 3 | 3 | 3 | 3 | 3 | 3 |

## 3.13 Summary

The purpose of this chapter is to help you start working with SAS procedures. The chapter begins with a quick presentation of options that control the display of SAS output. The annotation of output using the TITLE and LABEL statements follows. The use of formats is introduced and illustrated. Data set properties are displayed using PROC CONTENTS. The values of variables in a data set are listed using the PRINT procedure. Basic statistical graphics are introduced (SGPLOT), with statistical summaries of categorical variables (FREQ) and numeric variables (MEANS, UNIVARIATE) following. The selection of a simple random sample (SURVEYSELECT) and the randomization of treatments to experiments units (PLAN) bring this chapter to its close.

## 3.14 References

Agresti, Alan. 2002. Categorical Data Analysis. 2d ed. Hoboken, NJ: Wiley Interscience.

Bailer, A. John, and James T. Oris. 1994. "Assessing toxicity pollutants in aquatic systems." Case Studies in Biometry. N. Lange, L. Ryan, L. Billard, D. Brillinger, L. Conquest, and J. Greenhouse, eds. New York, NY: John Wiley & Sons, Inc.

Cassell, David L. 2007. "Don't Be Loopy: Re-Sampling and Simulation the SAS Way." Proceedings of the SAS Global Forum 2007 Conference. Cary, NC: SAS Institute Inc. Available at http://www2.sas.com/proceedings/forum2007/183-2007.pdf.

Stokes, Maura E., Charles S. Davis, and Gary G. Koch. 2000. Categorical Data Analysis Using the SAS System. 2d ed. Cary, NC: SAS Institute Inc.
