# Display 6.22 (continued)

```
if &M_Jmin < JanTemp <= &M_JQ1 then JanTemp_quart=1;
else if JanTemp <= &M_JQ2 then JanTemp_quart=2;
else if JanTemp <= &M_JQ3 then JanTemp_quart=3;
else if JanTemp <= &M_Jmax then JanTemp_quart=4;

label JanTemp_quart="Interval:";
format JanTemp_quart JTemp.;
run;

/* debugging check to see if variables correctly defined */
proc print data=SMSA_from_txt;
    var JanTemp JanTemp_quart freezing;
run;

/* define set of graphics */
ods rtf bodytitle file="C:\Users\baileraj.IT\Desktop\SMSA-plots.rtf";

* Display 6.23: HISTOGRAM of Jan. Temp.;
proc sgplot data=SMSA_from_txt;
    histogram JanTemp;
    density JanTemp / type=kernel;
run;

* Display 6.24: Scatter plot of Mortality vs. Education;
proc sgplot data=SMSA_from_txt;
    scatter x=Education y=Mortality;
run;

* Display 6.25: Scatter plots with shared y-axis for comparison;
proc sgscatter data=SMSA_from_txt;
    compare y=Mortality x=(Education income JanTemp) / loess;
run;

* Display 6.26: Scatter plot matrix;
proc sgscatter data=SMSA_from_txt;
    matrix Mortality Education income JanTemp / diagonal=(histogram);
run;

* Display 6.27: Separate scatter plots for levels of other variables;
proc sgpanel data=SMSA_from_txt noautolegend;  * to suppress legend;
    panelby freezing;
    loess x=Education y=Mortality;
run;

* Display 6.28: Same plot with diff. symbols and line types for diff var levels;
proc sgplot data=SMSA_from_txt;
    loess x=Education y=Mortality / group=freezing;
run;
```