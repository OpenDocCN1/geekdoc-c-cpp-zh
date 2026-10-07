# CHAPTER 5: PREPARING TO SAS® PROCEDURES

Using the options described in Table 5.10, you can enhance listing to create a more useful report. Some of the options listed duplicate those already discussed but are included for the sake of completeness.

Following are several examples illustrating the use of these options. For example, the N option instructs SAS to print the number of observations and allows you to specify a label to be printed:

```
N='Observations' =
```

The OBS option allows you to specify a label at the top of the Obs column in the data listing.

```
OBS='Subjects'
```

The SUM statement calculates a sum of the values for the variables listed is to be reported. For example:

```
SUM COST;
```

# TABLE 5.10 Common Options and Statement for PROC PRINT

| PROC PRINT Option | Meaning |
| --- | --- |
| DATA=dataset | Specifies which data set to use |
| DOUBLE | Double-spaces the output for ODS output formats such as RTF and PDF (This option has no effect in default SAS output (This is HTML)). |
| LABEL N <= 'label' | Instructs SAS to use variable labels as column headings Includes the number of observations in the listing and optionally specifies a label |
| OBS='label' | Specifies a label for the Obs column |
| NOBS | Suppresses the output column that identifies observations by number |
| ROUND | Rounds numbers to two decimal places unless they are otherwise formatted |
| SPLIT='char' | Defines a split character that is used to split label names for column headings. See the section "Column Titles" in this chapter |
| (FIRSTOBS=nl OBS=n2 | Causes PROC PRINT to only use selected records in a data set from nl as specified by FIRSTOBS= to the n2 as specified by OBS). |

Common statements for PROC PRINT

PROC PRINT statement

| VAR variable | Meaning |
| --- | --- |
| list; | Specifies which variables to include in the listing and in which order |
| SUM vars; | Specifies variables to report sum |
| BY, ID, WHERE | See Table 5.4 |