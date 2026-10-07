# 488 Learning SAS by Example: A Programmermer's Guide, Second Edition

```
*20-5;
title "Scatter Plot with Regression Line and Confidence Limits";
proc sgplot data=SASHelp.Heart;
  reg x=Height y=Weight /M CLI;
run;
```

```
*20-7;
title "Demonstrating PBSPLINE Smoothing";
proc sgplot data=SASHelp.Heart (obs=100);
  bspline x=Height y=Weight;
run;
```

```
*20-9;
title "Histogram for Cholesterol";
proc sgplot data=SASHelp.Heart;
histogram Cholesterol;
run;
```

```
*20-11;
title "Horizontal Box Plots";
proc sgplot data=SASHelp.Heart;
hhbox Cholesterol / group=Sex;
run;
```

# Chapter 21 Solutions

```
*21-1;
data prob21_1;
infile 'C:\books\learning\test_scores.txt' missover;
/* or truncator */
input Score1-3;
run;
```

```
title "Listing of PROB21_1";
proc print data=prob21_1 noobs;
run;
```

```
*21-3;
data prob21_3;
infile 'C:\books\learning\scores_column.txt' pad;
input Score 1-2
Score2 3-4
Score3 5-6;
run;
```

```
title "Listing of PROB21_3";
proc print data=prob21_3 noobs;
run;
```

```
*21-5;
title "Summary Report from BICYCLES Data Set";
data prob21_5;
set learn.bicycle end=lastrec;
TotalUnits + units;
Sum_of_Sales + TotalSales;
file print;
if lastrec then
  put "--------------------------------"
       "Total Units Sold is " TotalUnits comma10. /
       "Sales Total is " Sum_of_Sales dollar10.0;";
run;
```