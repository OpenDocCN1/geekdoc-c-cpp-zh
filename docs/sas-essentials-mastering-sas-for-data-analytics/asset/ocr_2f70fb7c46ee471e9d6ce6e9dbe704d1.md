# CHAPTER 10: ANALYZING COUNTS AND TABLES

(continued)

TABLE 10.6 PROC FREQ Output Using the ORDER = FREQ Option

| Example of PROC FREQ Using ORDER= Option |
| --- |
| The FREQ Procedure |
| Socioeconomic Status | | |
| STATUS | Frequency | Percent | Cumulative Frequency | Percent |
| 5 | 26 | 52.00 | 26 | 52.00 |
| 4 | 8 | 16.00 | 34 | 68.00 |
| 2 | 7 | 14.00 | 41 | 82.00 |
| 3 | 6 | 12.00 | 47 | 94.00 |
| 1 | 3 | 6.00 | 50 | 100.00 |

The following example illustrates another way to change the order in which the categories are displayed. This example uses the ORDER=FORMATTED option for PROC FREQ. In this case, you must first create a custom format in a PROC FORMAT command to define the order that you want to be used in your output table.

# HANDS-ON EXAMPLE

+   1. Open the program file AFREQ2.SAS.

```
PROC FORMAT;
VALUE $FMTRACE "AA="African American"
"H="Hispanic"
"OTH="Other"
"C="White";

RUN;

nPROC FREQ ORDER=FORMATTED DATA="C:\SASDATA\SURVEY";
TABLES RACE;
TITLE "Example of PROC FREQ using OPTION=Formatted";
FORMAT RACE $FMTRACE.;

RUN;
```

This program uses the ORDER=FORMATTED option to control the order in which the categories will be displayed in the table. To use this option, you must define a format where the labels are in an ascending order you want to use. In this program, a format named $FMTRACE is created in a PROC FORMAT statement. To apply this order to the categories, use the ORDER=option: