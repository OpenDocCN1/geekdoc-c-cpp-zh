# 274 Learning SAS by Example: A Programmermer's Guide, Second Edition

You can use the _TYPE variable to select the appropriate breakdown. For example, you can use the _TYPE_ values in a WHERE statement in a PROC PRINT statement, like this:

# Program 16.14: Using the _TYPE_ Variable to Select CLASS Variable Breakdowns

```
title "Statistics Broken Down by Gender";nproc print data=Summary(drop = freq_) noobs;
where _TYPE_ = '10';
run;
```

Figure 16.14: Output from Program 16.14

| Gender AgeGroup _TYPE_ | RBC_Mean WBC_Mean RBC_N WBC_N |
|---|---|---|---|---|---||
| Female | 10 | 5.49848 | 7112.43 | 409 | 403 |
| Male | 10 | 5.47146 | 6987.54 | 507 | 505 |

Because the values are broken down by Gender, AgeGroup has a missing value in each observation (it was left in the left for demonstration purposes).

You can also use this summary data to create separate data sets: for the grand mean, for means broken down by Gender, one broken down by AgeGroup, and one containing cell means. You can do this in one DATA step, like this:

# Program 16.15: Using a DATA Step to Create Summary Data Sets

```
Grand (drop = Gender AgeGroup)
By_gender(drop = AgeGroup)
By_Age (drop = Gender)
Cellmeans;
set Summary;
drop _freq_ = Number;
if _type_ = '00' then output Grand;
else if _type_ = '01' then output By_Age;
else if _type_ = '10' then output By_Gender;
else if _type_ = '11' then output Cellmeans;
run;
```

Because you want to select a different selection of variables in each data set, you can use a KEEP= or DROP data set option to make your selection. If you want to drop _TYPE_ from every set, it is easier to do this with a DROP statement in the DATA step. A RENAME statement renames _FREQ_ to Number. Again, this change applies to all four data sets.

_TYPE_ is a character variable of the CHARTYPE option, and you can use it to route each observation to the proper output data.

Below are listings of the four data sets produced by Program 16.15: