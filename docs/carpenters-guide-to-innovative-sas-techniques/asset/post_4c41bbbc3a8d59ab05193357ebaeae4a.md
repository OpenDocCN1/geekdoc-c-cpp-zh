
## 4.4a Showing SORT Metadata

**The CONTENTS Procedure**

| Property | Value | Property | Value |
|---|---|---|---|
| Data Set Name | WORK.LAB_CHEM | Observations | 165 |
| Member Type | DATA | Variables | 6 |
| Engine | V9 | Indexes | 0 |
| Created | Thu, Nov 05, 2009 02:26:48 PM | Observation Length | 56 |
| Last Modified | Thu, Nov 05, 2009 02:26:48 PM | Deleted Observations | 0 |
| Protection |  | Compressed | NO |
| Data Set Type |  | Sorted | **YES** ❶ |

When the SORTED flag ❶ contains YES, indicating that the data are sorted, an additional section is added to the PROC CONTENTS output. This section lets us know more about the conditions of the sort, including the BY variables ❷ and sort options ❹.

| Sort Information |
|---|
| **Sortedby** SUBJECT VISIT LABDT ❷ |
| **Validated** YES ❸ |
| **Character Set** ANSI |
| **Sort Option** NODUPREC ❹ |

❸ When SAS does the sorting, the VALIDATED flag is set to YES.

### The SORTEDBY Data Set Option

When the data are already sorted, but not by SAS, the SORTED metadata flag will not be changed to YES, and we can miss out on performance enhancements that take advantage of known sort order. We can let SAS know that the data are actually sorted by setting the SORTED flag to YES. You can set the SORTED metadata indicator flag directly by using the SORTEDBY data set option.

```
title1 '4.4b Using the SORTEDBY Option';
data lab2(sortedby=subject visit);
    set lab_chem;
    run;
proc contents data=lab2;
    run;
```

| Sort Information |
|---|
| **Sortedby** SUBJECT VISIT |
| **Validated** NO ❺ |
| **Character Set** ANSI |

Not only is the SORTED flag set to YES, but the sort information section is also completed. Notice, however, that the VALIDATED indicator is still set to NO ❺. We are trusted, but only trusted so far.

## 4.5 Using Threads

Some operations within a computer are computationally intensive. This is especially true for sorting operations and also for the calculation of large numbers of summary statistics. When multiple CPUs are available, some procedures will follow the principle of ‘divide and conquer,’ and they can split up computationally challenging tasks by spreading the work out among the available CPUs. This distributed workload can offer substantial improvements in the elapsed time to complete tasks.

The system option THREADS is used to allow SAS to take advantage of multiple CPUs. Although some of the documentation refers to the option in the singular, it needs to be THREADS. When multi-threads are used, a note is added to the LOG.

A number of Base SAS procedures, as well as several in SAS/STAT®, support multi-threaded operations. Additionally, support can also be found in some SAS Enterprise Miner® procedures and in some SAS/ACCESS® engines. Base procedures which have multi-threaded capabilities include: SORT, MEANS, SUMMARY, SQL, TABULATE, and REPORT.

Although the use of multiple threads will generally improve processing throughput, this does not necessarily have to be the case. Since resources are used not only to create and maintain the threads, but also to coordinate the information flow between threads, it is possible that the use of these resources can outweigh the advantage of the multiple threads. It is important for you to test your environment with and without threads to determine which is the better performance. You should test with both THREADS and NOTHREADS and, depending on your data and code, determine which is more efficient.

When more than two CPUs are present on the system, you may not want all of them to be available for use by SAS. The system option, CPUCOUNT, is used to control how many of the available CPUs can be used by SAS.

### SEE ALSO

Additional information on multi-threading can be found on the SAS R&D site  
[http://support.sas.com/rnd/scalability/procs/index.html](http://support.sas.com/rnd/scalability/procs/index.html).

![](img/4b16455363806a3241267bf9f49ba5d1_225_0.png)

## Chapter 5

### Working with Data Sets

- **5.1 Automating the COMPARE Process** 198
- **5.2 Reordering Variables on the PDV** 200
- **5.3 Building and Maintaining Indexes** 202
  - 5.3.1 Introduction to Indexing 203
  - 5.3.2 Creating Simple Indexes 204
  - 5.3.3 Creating Composite Indexes 206
  - 5.3.4 Using the IDXWHERE and IDXNAME Options 206
  - 5.3.5 Index Caveats and Considerations 207
- **5.4 Protecting Passwords** 208
  - 5.4.1 Using PROC PWENCODE 208
  - 5.4.2 Protecting Database Passwords 209
- **5.5 Deleting Data Sets** 211
- **5.6 Renaming Data Sets** 211
  - 5.6.1 Using the RENAME Function 212
  - 5.6.2 Using PROC DATASETS 212

While we are usually most interested in the data values and the analysis results that they generate, there are a number of operations that take place at the data table level. Sometimes we need to be able to work with the entire table and not just at the observation level. Fortunately SAS provides us with a number of tools for this type of processing.

## 5.1 Automating the COMPARE Process

`_TYPE_` refers to the two data sets being compared. ❶

- **BASE** — the data set identified with the DATA= option
- **COMPARE** — the data set identified in the COMPARE= option

Each pair of rows in the data set WORK.CMPR ❷ has at least one difference; however, searching these pairs of rows for the differences is only incrementally easier than searching the original output. We need to further isolate the individual values that are different. Since we know that there is at least one difference within each BASE/COMPARE pair of observations, we need to examine each pair of values for each variable individually within this observation pair. This can be more easily accomplished if we first transpose the data so that each value pair can be isolated.

PROC TRANSPOSE is used to create a data set with one observation per pair of variables within each of the two observations. Again the BY and ID statements are used to isolate the key variables. The variable `_OBS_`, which reflects the original observation number, is added to the BY statement to help make the identification process easier.

```
proc sort data=cmpr; ❸
    by subject visit labdt _obs_;
    run;

proc transpose data=cmpr
                out=tdiff(drop=_label_
                          rename=_name_=_variable_);
    by subject visit labdt _obs_; ❻
    var _numeric_ _character_; ❼
    id _type_; ❽
    run;
```

❻ The BY statement is used to identify down to the two rows with differences. The ID statement ❽ further identifies down to the specific row.

❼ In the VAR statement we need to list all the variables that need to be compared. Since we do not necessarily know the names of the variables we can use variable list abbreviations (see Section 2.6.1). `_ALL_` could also have been used here. When the variables to be compared are known (as is technically the case in this example) they can be named explicitly.

❽ The ID variable `_TYPE_`, which contains ‘BASE’ and ‘COMPARE’, is used to name the two new columns formed in the transformation process. These will be character variables when the variables in the VAR statement are either all character or a mixture of numeric and character. When there is a mixture of variable types, as is the case in this example, a conversion note is written to the LOG.

The data set TDIFF will now have one row for each original variable, and the values from the two original data sets are stored in the variables BASE and COMPARE. By selecting for unequal BASE and COMPARE values, we can determine the differences that have been detected in the comparison process.

```
title3 'After Transpose';
proc print data=tdiff(where=(variable ne '_TYPE_'
                           & base ne compare❾));

    run;
```

❾ The variables BASE and COMPARE now contain the original values of the variable named VARIABLE, which was renamed from `_NAME_`.

```
5.1 Automated Comparisons
Obs with differences
After Transpose

Obs  SUBJECT  VISIT       LABDT       _OBS_  variable  BASE  COMPARE
 6    200       2        07/13/2006      2   SODIUM     144    1A4
14    202       1        07/07/2006     20   SODIUM     139    1A9
```

In this example the differences are only printed; however, they could have been easily stored in a data set for further processing.

### MORE INFORMATION

A macro that further generalizes the comparison process can be found in program E5_1b.sas, which is located in the sample programs accompanying this book.

## 5.2 Reordering Variables on the PDV

The order of the variables on the Program Data Vector, PDV, is generally of no concern to the SAS programmer. Indeed there are no tools in the language that are specifically designed to help us to change the order once it has been established. Although they come up fairly infrequently, there are legitimate occasions that force us to either know or change the order of the variables on the PDV.

Sometimes when we create an EXCEL spreadsheet, the resulting columns need to be in a specific order. PROC EXPORT (see Section 1.2) will use the PDV order of the variables to determine the order of the EXCEL columns. To change this order we need to change the order of the variables going into PROC EXPORT.

The current order of the variables can be seen in a number of ways. Some of the most straightforward of these include:

- When PROC PRINT is used without an ID, BY, or VAR statement, the variables are printed in the order of their position.
- VIEWTABLE in the Display Manager displays the variables in position order.
- PROC CONTENTS displays the position of each variable, and with the VARNUM option (formerly the POSITION option) it will also list the variables in position order.
- The COLUMNS window in the Display Manager displays the columns in position order by default.

Within a DATA step the order of the variables on the PDV is determined as the step is compiled. If the step reads a data set, as with a SET statement, the incoming data set is examined and its variables are added to the PDV using the same order. Once the order is determined on the PDV it is fixed and cannot be altered. If we want to control the order we must do so before it is fixed.

Using the VARNUM option in a PROC CONTENTS step reveals, among other attributes, the order of the variables in ADVPRT.DEMOG. The left-most column is the variable or position number.
