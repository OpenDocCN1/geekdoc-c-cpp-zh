
# CHAPTER 10: ANALYZING COUNTS AND TABLES

PROC FREQ <options(s)>; <statements> TABLES requests </options>

Some common options for PROC FREQ are listed in Table 10.1.
Some common statements for PROC FREQ are listed in Table 10.2.

| Option | Meaning |
| --- | --- |
| DATA=datename | Specifies which data set to use |
| ORDER=option | Specifies the order in which results are listed in the output table Options DATA, FORMATTED, FREQ, and INTERNAL. This is illustrated in an upcoming example |
| PAGE | Specifies that only one table will appear per page (not applicable to HTML output) |
| ALPHA=n | Sets the level for confidence limits (default 0.05) |
| COMPRESS | Begins the next table on the same page when possible (not applicable to HTML output) |
| NOPRINT | Used when you want to capture output but not display tables |

| Option | Meaning |
| --- | --- |
| EXACT | Produces exact p-values for tests. Fisher's Exact test automatically calculated for a 2x2 table |
| OUTPUT=variable | Creates an output data set containing statistics from an analysis |
| WEIGHT | Identifies a weight variable that contains summarized counts |
| TABLES <variable-combinations/<options>>; | Specifies which tables will be displayed. More information about this statement is given below (Required) |
| TEST | Specifies which statistical tests will be performed (requires a TABLES statement) |
| BY, FORMAT, LABEL, WHERE | These statements are common to most procedures and may be used here |

## 10.1.1 The TABLES Statement

The TABLES statement is required for all of the examples in this chapter. Its format is as follows:
TABLES <variable-combinations/<options>>

where variable-combinations specifies frequency or cross-tabulation tables.
For examples, see Table 10.3.
Options for the table follow a slash (/). For example,
TABLES A*B / CHISQ;

requests that the chi-square and related statistics will be reported for the cross-tabulation A*B. Commonly used TABLE options following a / are listed in Table 10.4.

For example, in a simple use of PROC FREQ, to obtain counts of the number of subjects observed in each category of group (GP), use the following:

```
PROC FREQ; TABLES GP; RUN;
```

To produce a cross-tabulation table of GENDER by treatment GP, use

```
PROC FREQ; TABLES GENDER*GP; RUN;
```

The variables specified in the TABLES statement can be either type categorical/character or numeric (where numeric values represent discrete categories). To request chi-square statistics for a table, include the option /CHISQ at the end of the TABLES statement. For example,

```
PROC FREQ; TABLES GENDER*GP/CHISQ;
```

# TABLE 10.3 Sample TABLES Statements

| Table | Description |
| --- | --- |
| TABLES A; | Specifies frequencies for a single variable |
| TABLES A*B; | Specifies a cross-tabulation between two variables |
| TABLES A*B B*C X*Y; Also, TABLES A* (B C D); is the same as TABLES A*B A*C A*D; | Specifies several cross-tabulation tables |
| TABLES (A - C)*; is the same as TABLES A* B*X C*X; | Uses a range of variables in a TABLES statement |

# TABLE 10.4 Options for the Table Statement

| Option | Description |
| --- | --- |
| AGREE | Requests kappa statistic (inter-rater reliability). To include significance tests for kappa, add a TEST statement. For example, TABLES A*B /AGREE; TEST KAPPA; |
| RELRISK | Requests relative risk calculations |
| FISHER | Requests' Exact test for tables greater than 2x2 |
| SPARSE | Requests all possible combinations of variable levels even when a combination never occurs |
| MISSING | Requests that missing values be treated as nonmissing |
| CELLCHI2 | Displays the contribution to chi-square for each cell |
| NOCOL | Suppresses percentages for each cell |
| NOCUM | Suppresses cumulative and cumulative percentages in one-way frequency tables and in list format |
| NOFREQ | Suppresses frequency count for each cell |
| NOPERCENT | Suppresses row and column percentage in cross-tabulation tables, or cumulative percentages in one-way frequency tables and in list format |
| NOPRINT | Suppresses tables but displays statistics |
| NOROW | Suppresses row percentage for each cell |
| TESTP=(list) | Specifies a test based on percentages for the chi-square test (see the goodness-of-fit example) |

## 10.2 ANALYZING ONE-WAY FREQUENCY TABLES

When count data are collected, you can use PROC FREQ to produce tables of the counts by category as well as to perform statistical analyses on the counts. This section describes how to create tables of counts by category and how to perform a goodness-of-fit test.

The number and type of tables produced by the PROC FREQ procedure are specified WITH a TABLES statement. When individual variables are used in the TABLES statement, PROC FREQ produces a frequency table. The following Hands-on-Example illustrates how to create a frequency table for a single variable.

> Recall that sample data sets are in the C:\SAS folder and SOMEDATA contains a sample data set of 50 records. In the following Hands-on Example, note DATA= statement could also be DATA=MYSASLIB if you have MYSASLIB defined.

### HANDS-ON EXAMPLE
In this example, you will learn how to use PROC FREQ to display frequency information for a qualitative (categorical) data.

1. Open the program file FREQ1.SAS.
```
PROC FREQ DATA="C:\SAS\SOMEDATA";
TABLES STATUS;
TITLE 'Simple Example of PROC FREQ';
RUN;
PROC FREQ DATA="C:\SAS\SOMEDATA" ORDER=FREQ;
TABLES STATUS;
TITLE 'Example of PROC FREQ Using ORDER';
RUN;
```
This code includes two PROC FREQ statements. In the first example, a table is requested for the variable STATUS. The second example is similar, but an additional option, ORDER=FREQ, is used to request that the table be sorted by the frequency count. Following are some of the PROC FREQ ORDER= options values by their order in the data set.

# TABLE 10.6 PROC FREQ Output Using the ORDER = FREQ Option

| Example of PROC FREQ Using ORDER= |
| --- |
| The FREQ Procedure |
| Socioeconomic Status |
| STATUS | Frequency | Percent | Cumulative Frequency | Percent |
| 5 | 26 | 52.00 | 26 | 52.00 |
| 4 | 8 | 16.00 | 34 | 68.00 |
| 2 | 7 | 14.00 | 41 | 82.00 |
| 3 | 6 | 12.00 | 47 | 94.00 |
| 1 | 3 | 6.00 | 50 | 100.00 |

The following example illustrates another way to change the order in which the categories are displayed. This example uses the ORDER=FORMAT option for PROC FREQ. In this case, you must first create a custom format in a PROC FORMAT to define the order that you want be used in your output table.

### HANDS-ON EXAMPLE
1. Open the program file FREQ2.SAS.
```
PROC FORMAT;
VALUE $RACE "African American"=1 "Hispanic"=2 "Other"=3 "White"=4;
RUN;

nPROC FREQ ORDER=FORMATTED DATA="C:\SAS\SURVEY";
TABLES RACE;
TITLE "Example of PROC FREQ using FORMAT";
FORMAT $RACE.;
RUN;
```
This program uses the ORDER=FORMATTED option to control the order in which the categories will be displayed in the table. To use this option, you must define a format where the labels are in an ascending order you want use. In this program, a format named $RACE is created in a PROC FORMAT statement.

### HANDS-ON EXAMPLE
This example illustrates how to summarize counts from a data set into a frequency table.

1. Open the program file FREQ3.SAS.
```
DATA COINS;
INPUT @1 CATEGORY $9. @11 NUMBER 3;
DATLINES;
CENTS 152
CENTS 100
NICKELS 49
DIMES 59
QUARTERS 21
HALF 44
DOLLARS 21;

PROC FREQ WEIGHT NUMBER;
TITLE 'Reading Summarized Count data';
TABLES CATEGORY;
RUN;
```
Note that the data are already in counts. The statement WEIGHT NUMBER tells PROC FREQ that for the variable NUMBER are counts. Even though there are two records for CENTS, the program is able to combine the WEIGHT (counts) into a single CENTS category (252 CENTS).

2. Run the program and observe the output for PROC FREQ, as given in Table 10.8.

# TABLE 10.8 Simple Output for PROC FREQ
Reading Summarized Count data FREQ Procedure

| CATEGORY | Frequency | Percent | Cumulative Frequency | Cumulative Percent |
|---|---|---|---|---|
| CENTS | 252 | 56.50 | 252 | 56.50 |
| DIMES | 59 | 13.23 | 311 | 69.73 |
| DOLLARS | 21 | 4.71 | 332 | 74.44 |
| HALF | 44 | 9.87 | 376 | 84.30 |
| NICKELS | 49 | 10.99 | 425 | 95.29 |
| QUARTERS | 21 | 4.71 | 446 | 100.00 |
