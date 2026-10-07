# 246 CHAPTER 10: ANALYZING COUNTS AND TABLES

statistics for a table, include the option /CHISQ at the end of the TABLES statement. For\example,

```
PROC FREQ; TABLES GENDER*GP/CHISQ;
```

The following sections describe in more detail how to use PROC FREQ to create and
analyse tables of counts.

# 10.2 ANALYZING ONE-WAY FREQUENCY TABLES

When count data are collected, you can use PROC FREQ to produce tables of the countsy category as well as to perform statistical analyses on the counts. This section describes
how to create tables of counts by category and how to perform a goodness-of-fit test.

The number and type of tables produced by the PROC FREQ procedure are specified
WITH a TABLES statement. When individual variables are used in the TABLES statement,
PROC FREQ produces a frequency table. The following Hands-on-Example illustrates how
to create a frequency table for a single variable.

> Recall that sample data sets are in the C:\SASDATA folder and the SOMEDATA data
contains a sample data set of 50 records. In the following Hands-on Example, note
theta DATA= statement could also be DATA=MYSASLIB. SOMEDATA if you have
the MYSASLIB defined.

HANDS-ON EXAMPLE
In this example, you will learn how to use PROC FREQ to display frequency information
for a qualitative (categorical) data variable.
1. Open the program file FREQ1.SAS.
PROC FREQ DATA="C:\SASDATA\SOMEDATA";
TABLES STATUS;
TITLE 'Simple Example of PROC FREQ';
RUN;
PROC FREQ DATA="C:\SASDATA\SOMEDATA" ORDER=FREQ;
TABLES STATUS;
TITLE 'Example of PROC FREQ Using ORDER= Option';
RUN;
This code includes two PROC FREQ statements. In the first example, a table is
requested for the variable STATUS. The second example is similar, but an additional
option, ORDER=FREQ, is used to request that the table be sorted by the descending
order of the frequency count.
Following are some of the PROC FREQ ORDER= options.
DATA
Orders values by their order in the data set.