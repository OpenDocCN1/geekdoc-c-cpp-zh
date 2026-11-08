
### 4.1.5 The FORCE Option

When the OUT= option is not used on the PROC SORT statement, the incoming data set is replaced with its sorted analogue. When the data set is indexed or if the metadata sort indicators (such as is created by the SORTEDBY= data set option – see Section 4.4) indicate that the data set is already sorted, the sorting does not take place. For indexed data sets this protects the index, and for data sets that are already sorted this conserves resources. When this default behavior is not what you want, the FORCE option can be used.

### 4.1.6 The EQUALS or NOEQUALS Options

Typically when PROC SORT reorders observations based on the levels of the BY variables, the block of observations within a given level or BY group does not change their order. Generally we do not care about the order of the rows within a BY group; if we did we would add another variable to the BY list. While this default behavior can be controlled at the operating system option level using the SORTEQUALS or the NOSORTEQUALS option, it can also be controlled at the PROC SORT step level using the EQUALS or NOEQUALS options.

Under earlier versions of SAS this order preservation made sense from an operational point of view. Fewer resources were expended by handling the rows as a block. Under the current versions of SAS this default behavior may no longer be our best choice. With multi-threading available to the SORT procedure, portions of these blocks may be divided up across processors. When the rows are returned from the different threads, additional resources may actually be expended just to preserve the order within a block, an order that we probably do not care about.

The NOEQUALS option can be used on the PROC SORT statement to allow SAS to not worry about maintaining the original order within groups. Allowing the within block order to change (by not forcing it to be preserved) through the use of the NOEQUALS option can save resources; however, it can also have other impacts. The order returned, especially when multiple processors are involved, can change from one sort to the next. Since the NODUPREC option (see Section 4.1.1) relies on observation order, its results may also vary from one run to the next when the NOEQUALS option is used.

### MORE INFORMATION

Caveats associated with the use of the NODUPREC option are discussed in Section 4.1.1.

## 4.2 Using Data Set Options with PROC SORT

One of the primary efficiency techniques used to speed up our programs is to eliminate variables and/or observations as soon as possible in the data handling process. Just as we will seldom carry a parka in our luggage when visiting Miami, we should not carry the extra baggage of variables or observations that are not needed. Trimming up the data can have a major impact in the time needed to complete a PROC SORT.

Fortunately for us the process of culling unneeded variables and observations can be handled within the PROC SORT step itself through the use of data set options.

### MORE INFORMATION

The use of threads to improve efficiency is discussed in Section 4.5. Differences between the BY and CLASS statements for the MEANS or SUMMARY procedures are discussed in Section 7.12.

## Anticipate Procedure Output Order

For procedures that create output data sets, the order of the data is generally known or at least knowable, and knowing the order of the generated data, or planning the procedure so that it generates data in the desired order can eliminate the necessity of a subsequent PROC SORT. To control the possible orderings of the output data set, be sure to take advantage of the ORDER= option. Generally speaking, the order of the classification variables on the incoming data does not affect the output order unless the ORDER= option is set to DATA (see Section 2.6.2).

Even procedures that do not support the CLASS statement may have implied classification variables (e.g., PROC FREQ), and the values of these variables, along with the ORDER= option, help to determine the order of any generated data sets.

The following table is a listing of a data set that was created by a PROC SUMMARY step.

| Obs | race | edu | symp | _TYPE_ | _FREQ_ | mean HT |
|---:|---:|---:|---:|---:|---:|---:|
| 1 | . | . | . | 0 | 8 | 66.25 |
| 2 | . | 01 | . | 2 | 2 | 64.00 |
| 3 | . | 02 | . | 2 | 4 | 66.50 |
| 4 | . | 03 | . | 2 | 2 | 68.00 |
| 5 | 12 | . | . | 1 | 4 | 67.50 |
| 6 | 14 | . | . | 1 | 2 | 64.00 |
| 7 | 15 | . | . | 1 | 2 | 66.00 |
| 8 | 12 | 02 | . | 3 | 2 | 67.00 |
| 9 | 12 | 03 | . | 3 | 2 | 68.00 |
| 10 | 14 | 01 | . | 3 | 2 | 64.00 |
| 11 | 15 | 02 | . | 3 | 2 | 66.00 |
| 12 | 1 | . | 4 | 5 | 6 | 67.00 |
| 13 | 4 | . | 4 | 5 | 2 | 64.00 |
| 14 | 1 | 02 | 5 | 7 | 4 | 66.50 |
| 15 | 1 | 03 | 5 | 7 | 2 | 68.00 |
| 16 | 4 | 01 | 5 | 7 | 2 | 64.00 |
| 17 | 1 | 12 | 6 | 7 | 4 | 67.50 |
| 18 | 1 | 15 | 6 | 7 | 2 | 66.00 |
| 19 | 4 | 14 | 6 | 7 | 2 | 64.00 |
| 20 | 1 | 12 | 02 | 7 | 2 | 67.00 |
| 21 | 1 | 12 | 03 | 7 | 2 | 68.00 |
| 22 | 1 | 15 | 02 | 7 | 2 | 66.00 |
| 23 | 4 | 14 | 01 | 7 | 2 | 64.00 |

By inspection you can see the sort order and you could even infer the CLASS statement. You can also infer the ORDER= option associated with each variable on the CLASS statement.

Assuming that the classification variables are not formatted, inspection of this table suggests the following CLASS statement (for this procedure INTERNAL is the default value for the ORDER= option).

```sas
class race edu symp /
      order=internal;
```

If this data set was to be used in a subsequent step, each of these BY statements could be used without first using a PROC SORT.

```sas
by _type_;
```

```sas
by race edu symp;
```

```sas
by _type_ race edu symp;
```

## Avoid Sorting by Using Indexes

Indexes provide you with a way to establish one or more virtual sort orders against a data set. While an index must be created and maintained, for stable data sets this cost may be minimal relative to the cost of sorting and then re-sorting the data.

When an index is created it is stored in a separate file from the data set itself. Whenever the data set is modified, even if the modification does not alter the order of the rows, the index must be recreated. The index file itself will take storage space. The amount of required space will depend on several factors, including the number of rows in the table, the number of indexes that have been established, and the number of variables that make up each index. Additional benefits of indexes include optimized searches with WHERE clauses and the ability to perform double SET statement merges and table look-ups without sorting (see Sections 6.4 and 6.6).

### MORE INFORMATION

Indexes are discussed in more detail in Section 5.3.

## Using PROC SQL to Avoid Sorts

When PROC SQL operates on a data table, the entire table is loaded into memory. While this means that PROC SQL can be limited in what it can do with larger tables (limited by available memory), it also means that the sort order of incoming data is rarely an issue within the SQL step.

A match merge in the DATA step requires a BY statement; however, this is not the case with the equivalent JOIN in an SQL step. Also, the GROUP BY clause, which is analogous to the CLASS statement, is also available in the SQL step. Before sorting the data, consider whether or not the use of an SQL step might yield the same result, while avoiding a SORT, as well as an additional pass of the data.

If a data set is too large to sort, especially if you have tried the TAGSORT option, then it is likely to be too large to be effectively handled by an SQL step.

## 4.4 Metadata Sort Information

When data are sorted or indexed, information about the sort is stored as a part of the table’s metadata. In this example a simple PROC SORT is executed, and the data set’s metadata is then displayed using PROC CONTENTS.

```sas
title1 '4.4a Showing SORT Meta-data';
proc sort data=advrpt.v_lab_chemistry
          out=lab_chem
          noduplicates;
  by subject visit labdt;
run;
proc contents data=lab_chem;
run;
```

Among other things, information about how the data is sorted is contained in two different sections of the PROC CONTENTS output.

The upper-most section shows the internal sorted flag ❶, which takes on the values of either YES or NO.
