
## Chapter 22: Using Advanced Features of User-Defined Formats and Informats

## Program 22.15: Using the Nested Format in a DATA Step

```sas
data Conference;
  input @1 Name $10;
    @11 Date mmddyy10;
  format Date Registration;
datalines;
Smith 10/21/2018
Jones 11/13/2017
Harris 01/03/2018
Arnold 02/12/2019
;
```

A listing of data set Conference is shown here:

## Figure 22.16: Listing of Data Set Conference

| Name | Date |
| --- | --- |
| Smith | 10/21/2018 |
| Jones | Not Open |
| Harris | 01/03/2018 |
| Arnold | Too Late |

This is a very powerful feature of PROC FORMAT. It saves having to write an IF-THEN-ELSE statement in a DATA step.

The next example uses user-written informats. In this example, you are given data on benzene exposure. Some of the values are actual benzene levels in per million, while other values are the year worker exposed. For each of the years from 1946 to 1952, benzene levels were tabulated. For years outside this range, the actual benzene levels were reported. Some sample data from Benzene.txt, consisting of either a year or a benzene level, is shown next:

```
001 90
002 1950
003 217
004 1952
005 177
```

All of the benzene levels are much less than any of the year values, so there is no confusion whether to read a value as a year or a benzene level. Creating a data set of IDs and benzene levels is greatly simplified by nesting informats, like this:

## Program 22.16: Creating a Data Set of Benz Levels

```sas
proc format;
  value YearExp 1946 = 250
                    1947 = 244
                    1948 = 240
                    1949 = 200
                    1950 = 188
                    1951 = 150;
  1952 -;
  value Exp Low - <1946 = [7.1]
                    1946 - 1952 = [Yearexp].
                    1952< high = [7.1];

data Benzene;
  infile 'C:\Learning\Benzene.txt';
  input Exposure = Exp4.;
```

The first informat, YAREXP, substitutes a benzene level for each of the years from 1946 to 1952. The informat EXP uses a SAS 7.1 informat for values less than 1946 or greater than 1952. Otherwise, the YAREXP informat is used.

Here is a listing of the data set:

## Figure 22.17: Listing of Data Set Benzene

## Listing of Data Set Benzene

| ID | Exposure |
| --- | --- |
| 1 | 9.0 |
| 2 | 188.0 |
| 3 | 21.7 |
| 4 | 100.0 |
| 5 | 17.7 |

This problem could also have been solved using formats instead of informats. To use formats, you would need to read a raw data value and use a PUT function to obtain a formatted value. Because the result of a PUT function is a character value, you would also need to use an INPUT function to obtain a benzene level as a numeric value. Creating formats makes the process much simpler.

## 22.10 Multilab Formats

Under normal circumstances, you can get an error message if any of your format ranges overlap. However, you can create a format with overlapping ranges if you use the MULTILABEL option in the VALUE statement. Certain procedures that use multilabels can then use the MULTILABEL format (MLF) to produce tables showing all of the format ranges. Here is an example.

You want to see the variable Age (from the Survey data set) broken down two ways: one, in 20-year intervals, and the other by a split at 50 years old. You first create a MULTILABEL format like this:

## Program 22.17: Creating a MULTILABEL Format

```sas
proc format;
  value AgeGroup (multilabel)
    0 <20 = '00 to <20'
    20 <40 = '20 to <40'
    40 <60 = '40 to <60'
    60 <80 = '60 to <80'
    80 - high = '80 +'

    0 <50 = 'Less than 50'
    50 - high = '> or = to 50';
run;
```

Without the MULTILABEL option, PROC FORMAT issues an error message about overlapping ranges and fails to create the format.

You can use this format in PROC MEANS, PROC SUMMARY, and PROC TABULATE. Here is a PROC MEANS example:

## Program 22.18: Using a MULTILABEL Format with PROC MEANS

```sas
title "Demonstrating Multilabel Format"
title2 "PROC MEANS Example";
proc means data=Learn.Survey / MLF;
  class Age;
  var Salary;
  format AgeGroup;
run;
```

It is important to use the MLF option in the CLASS statement if you want to use this feature of the format. Here is the output:

## Figure 22.18: Output from Program 22.18

## Demonstrating Multilabel Format PROC Example

| Analysis Variable : Salary | Obs | Mean | Std Dev | Maximum |
| --- | --- | --- | --- | --- |
| Age of 1/1/2006 | N | | | |
| 20 to <40 | 3 | 3 | 29186.67 | 6798.13 | 36560.00 |
| 40 to <60 | 2 | 2 | 76111.50 | 16234.56 | 76100.00 |
| 60 to <80 | 2 | 2 | 109000.00 | 26870.06 | 90000.00 |
| > or = to 50 | 3 | 3 | 98041.00 | 26857.01 | 76123.00 |
| Less than 50 | 4 | 4 | 40915.00 | 24104.46 | 76100.00 |

You can use MULTILABEL formats with PROC TABULATE to create interesting tables. Here is a program to compute frequencies in a table of Age by Gender:

## Program 22.19: Demonstrating Multilabel Format

```sas
title "Demonstrating Multilabel Format";
title2 "PROC TABULATE Example";
proc tabulate data=Learn.Survey;
  class Age / MLF;
  table Age * Gender;
  format AgeGroup;
run;
```

This produces the following output:

## Program 22.19: Output from Program 22.19 Demonstrating Multilabel Format PROC TABULATE Example

| | Female | Male |
| --- | --- | --- |
| | N | N |
| Age as 1/1/2006 | | |
| 20 to <40 | | 3 |
| 40 to <60 | 2 | |
| 60 to <80 | 1 | 1 |
| or = to 50 | 2 | 1 |
| Less than 50 | 1 | 3 |

Notice that certain age groups are not shown in the table. For example, there were no subjects in the 0 <20 age group. To see all of the possible format ranges in your table, you can use the PRELOADFMT option in the CLASS statement. Preloaded formats allow PROC TABULATE to list categories for which there are no data values.

## Program 22.20: Using the PRELOADDFMT, PRINTMISS, and MISSTEXT Options with PROC TABULATE

```sas
title "Demonstrating a Multilabel Format";
title2 "PROC TABULATE Example";
proc tab data=Learn.Survey;
  class Age / MLF preloadfmt;
  table Age;
    Gender / printmiss misstext=' ';
  format AgeGroup.;
run;
```

The PRELOADDFMT option forces the procedure to list all of the format ranges. This option has no effect with the PRINTMISS option in the TABLE statement. Remember that PRINTMISS is an instruction to include categories that contain one or more missing values of a CLASS variable. Finally, MISSTEXT= tells the procedure which character (or characters) you would like that that represents missing values (the period). Here you choose a blank to represent missing values. Finally, the output:

## Figure 22.20: Output from Program 22.20

| Gender | Female | Male |
| --- | --- | --- |
| Age as 1/1/2006 | N | N |
| 0 to <20 | | |
| 20 to <40 | | 3 |
| 40 to <60 | 2 | |
| 60 to <80 | 1 | 1 |
| 80 + | | |
| > or = to 50 | 2 | 1 |
| Less than 50 | 1 | 3 |

Now all the Age ranges appear in the table and the missing values print blanks.

## 22.11 Using the INPUTN Function to Perform a More Complicated Lookup

The problem: you have a table of years (1944 to 1949) and job codes. Each combination of year and job code has a benzene exposure (in parts million) associated with it. The following table values are:

| Year | A | B | C | D | E |
| --- | --- | --- | --- | --- | --- |
| 1944 | 220 | 180 | 210 | 110 | 90 |
| 1945 | 202 | 170 | 208 | 100 | 85 |
| 1946 | 150 | 110 | 150 | 60 | 50 |
| 1947 | 105 | 56 | 88 | 40 | 30 |
| 1948 | 60 | 30 | 40 | 20 | 10 |
| 1949 | 45 | 22 | 22 | 10 | 8 |

One way to compute an exposure, given a year and job code, is to create an informat for each year, assigning each of the job codes a label containing the exposure value. An informat is used instead of a format because you can use an INPUT (or, as you will see, INPUTN) function with the user-defined informats to obtain a numeric value directly. If you did this “by hand,” you would proceed like this:

## Program 22.21: Partial Program Showing How to Create Several Informats

```sas
proc format;
  invalidate Exp1944fmt (upcase);
    'A' = 220
    'B' = 180
    'C' = 210
    'D' = 110
    'E' = 90
  other = ;
  invalidate Exp1945fmt (upcase);
    'A' = 202
    'B' = 170
    'C' = 208
    'D' = 100
    'E' = 85
  other = ;
  invalidate Exp1946fmt (upcase);
    'A' = 150
run;
```

It takes less work to create an input control data set (CNTLIN) to create the required informats. You proceed as follows:
