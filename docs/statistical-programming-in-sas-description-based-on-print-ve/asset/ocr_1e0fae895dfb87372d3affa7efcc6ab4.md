```
1 2 3
1 4 5
2 6 7
;
run;

data m2c;
    input ID var1;
    datalines;
1 11
2 21
2 22
;
run;

data m12c;
    merge m1c m2c;
    by ID;
proc print data=m12c;
    title "many to one merging issues";
run;

data m1d;
    input ID v1 v2;
    datalines;
1 2 3
1 4 5
;
run;

data m2d;
    input ID var1;
    datalines;
1 11
1 12
1 13
;
run;

data m12d;
    merge m1d m2d;
    by ID;
run;

proc print data=m12d;
    title "many to many merging issues";
run;

/* =============================
/* BASIC SQL STUFF
/* =============================

options formdlim="-";
data junk;
    input cgroup $ x y @@;
```