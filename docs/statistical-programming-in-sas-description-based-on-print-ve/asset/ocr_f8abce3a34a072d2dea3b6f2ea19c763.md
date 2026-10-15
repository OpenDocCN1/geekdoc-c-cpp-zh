# Display 2.26 *(continued)*

```
data SMSA_subset_pollution;
    length city $ 27;
    input city & HCpot NOxPot SO2Pot NOx;
datalines;
Akron, OH  21 15 59 15
Albany-Schenectady-Troy, NY  8 10 39 10
Baltimore, MD  43 38 206 38
Allentown, Bethlehem, PA-NJ  6 6 33 6
Atlanta, GA  18 8 24 8
;
run;

proc sort data=SMSA_subset_weather;
    by city;
run;
proc sort data=SMSA_subset_demog;
    by city;
run;
proc sort data=SMSA_subset_pollution;
    by city;
run;

data all_subset;
    merge SMSA_subset_weather SMSA_subset_demog SMSA_subset_pollution;
    by city;
run;

ods rtf bodytitle file='C:\Users\baileraj.TT\Desktop\ch2-fig2.26.rtf';
proc print data=all_subset;
    var city JanTemp mortality NOx;
run;
ods rtf close;
```

Each data set must be sorted by CITY—the common key for the later merge—before merging is done using the MERGE statement.

```
data all_subset;
    merge SMSA_subset_weather SMSA_subset_demog SMSA_subset_pollution;
    by city;
```

The SAS log confirms that the five observations in the three SMSA subset data sets are merged into a single data set—all_subset—containing five observations:

```
NOTE: There were 5 observations read from the data set WORK.SMSA_SUBSET_WEATHER.
NOTE: There were 5 observations read from the data set WORK.SMSA_SUBSET_DEMOG.
NOTE: There were 5 observations read from the data set WORK.SMSA_SUBSET_POLLUTION.
NOTE: The data set WORK.ALL_SUBSET has 5 observations and 17 variables.
```