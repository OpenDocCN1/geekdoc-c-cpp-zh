You can customize statistical summaries in tabular output using PROC TABULATE, which is discussed in detail in Chapter 4.

# 3.11 Selecting a Simple Random Sample

Simple random samples can be selected using survey procedures. Suppose you want to select a sample of N=6 cities (without replacement) from the SMSA data set (which contains N=60 cities). The SURVEYSELECT procedure makes this a simple task. The program is shown in Display 3.32.

# Display 3.32 SAS program to select a simple random sample of N=6 cities selected from a data set containing N=60 cities

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