# Display 4.6 (continued)

```
retain P_25 P_75;      * keep values of Q1 and Q3 around to be assigned;
if _n =1 then set cstats;  * read and process CSTATS data set first;
  set cstats;
  set country;
run;

* you need to be somewhat careful in defining categories if any missing;
*   values are present (see Section 8.3) - not a problem in this example;
data country; set country;    * define density categorical var;
if density <= P_25 then density_cat=1;      * [min, Q1];
else if density <= P_75 then density_cat=2;      * [Q1, Q3];
else density_cat=3;                         * (Q3, max];
run;
* aside: could hard code Q1/Q3 but the solution above is a bit slicker and
        avoids the possibility of transcription error, is robust to
        underlying data changes when program is rerun;

proc freq data=country;  * check construction of density category variable;
table density_cat;
run;

* additional check suggested by Kathy Roggenkamp;
proc means data=country n nmiss min max;
class density_cat / missing;
var density;
run;

ods rtf BODYTITLE file="&topdir\Display-4.6.rtf";
proc tabulate data=country;
class density_cat;
var lifemen lifewom liter loggnp;
table (lifemen lifewom liter loggnp)*(n nmiss mean median stddev), density_cat;
run;
ods rtf close;
```

The program first reads the country data set, and then defines additional variables including LOGGNP and population density. The quartiles of DENSITY are determined using PROC UNIVARIATE, and then a categorical variable is created that indicates whether a country falls in the lowest 25%, middle 50%, or upper 25% of population density in this collection of countries. The assignment of these categories is checked using PROC FREQ. (Here, one fourth of the countries should be in the first category, and one fourth should be in the third category. One half should be in the middle category). A (not very attractive) table is produced and shown in Display 4.7.