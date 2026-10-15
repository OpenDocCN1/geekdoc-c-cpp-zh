```
run;

proc print data=m12;
    title "First Merge data example";
run;

/* suppose you have common variables in the data sets that are merged? */

options formdlim="-";

data m1b;
    input ID v1 v2;
    datalines;
1 2 3
2 5 6
4 7 8
;
run;

data m2b;
    input ID v1 v2 var3;
    datalines;
1 11 12 13
2 14 15 16
3 17 18 19
;
data M12b;
    merge m1b m2b;
    by ID;
run;

proc print data=m12b;
    title "Second Merge data example - common variables in 2 data sets";
run;

data M12b2;
    merge m2b m1b;
    by ID;
run;

proc print data=m12b2;
    title "Second Merge data example - diff merge order";
run;

proc print data=m1b;
run;
proc print data=m2b;
run;

/* what if the data sets have multiple records with an ID? */

data m1c;
    input ID v1 v2;
    datalines;
```