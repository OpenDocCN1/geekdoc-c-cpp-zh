330 Learning SAS by Example: A Programmer's Guide, Second Edition

# ### Program 19.4: Using an ODS SELECT Statement to Restrict PROC UNIVARIATE Output

```
ods select extremeobs;

title "Extreme Values of RBC";nproc Univariate data=Learn.Blood;
  id Subject;
  var RBC;
run;
```

When you run this program, the only output is as follows:

# ### Program 19.5: Output from Program 19.4
Extreme Values of RBC

| Variable: RBC |
|---||
| Extreme Observations | | |
| Value Subject Obs | Value Subject Obs |
|---|---|---|---|---|---||
| 1.71 | 525 | 525 | 7.99 | 565 | 565 |
| 2.33 | 440 | 440 | 8.12 | 984 | 984 |
| 2.55 | 113 | 113 | 8.26 | 288 | 288 |
| 2.92 | 293 | 293 | 8.43 | 726 | 726 |
| 3.13 | 635 | 635 | 8.75 | 135 | 135 |

This seems simple enough, but how do you determine the name of the output objects (in this case, EXTREMEOBS?) One way is to run the procedure sandwiched between ODS TRACE ON and ODS TRACE OFF statements, like this:

# ### Program 19.5: Using the ODS TRACE Statement to Identify Output Objects

```
ods trace on;

title "Extreme Values of RBC";nproc Univariate data=Learn.Blood;
  id Subject;
  var RBC;
run;
```