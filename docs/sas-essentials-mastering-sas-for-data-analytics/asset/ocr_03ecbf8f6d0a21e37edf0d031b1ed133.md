# TABLE 5.4 Common Options and Statements for SAS PROCS

Common Options for SAS PROCS

| PROC Option | Meaning |
| --- | --- |
| DATA=dataset | Specifies which data set to use in the analysis |
| OUT=dataset | Creates an output data set containing results from the procedure |

Common statements for SAS PROCS

| PROC statement | Meaning |
| --- | --- |
| VAR variable(s); | Instructs SAS to use only the variables in the list for the analysis |
| BY variable(s); | Causes SAS to repeat the procedure for each different value of the named variable(s). (The data set must be sorted by the variables listed in the BY statement.) |
| ID variable(s); | Instructs SAS to use the specified variable as an observation identifier in a listing of the data |
| LABEL var='label'; | Assigns a descriptive label to a variable. (This statement can also appear in the DATA step.) |
| WHERE condition; | Specifies a condition for which only records meeting the condition are used in the procedure |

A simplified syntax for the SAS PROC statement is as follows:

```
PROC name <options>
<Statements/statementoptions>
RUN;
```

The most commonly used option within the PROC statement is the DATA= option. For example:

```
PROC PRINT DATA=MYDATA;
RUN;
```

The DATA= option tells SAS which data set to use in the analysis. If there has been only one data set previously created (within a session), there is no need for this statement. However, if you've created more than one data set during a particular SAS session, it's a good idea to include a DATA= option to specify which data set is to use. If you do not specify a DATA= option, SAS will use the most recently defined data set for the specified procedure.

Procedure statements are often required to indicate information about how an analysis is to be performed. For example, in the code

```
PROC PRINT;
VAR GROUP TIME1 TIME2;
RUN;
```

the VAR statement indicates that only the listed variables are to be used in the procedure. Statements can themselves have options. For example:

```
PROC FREQ;
TABLE GROUP*SOCIO/CHISQ;
RUN;
```