
## Chapter 3: Formatting Output

- Introduction ........................................................................................................................ 92
- Formatting Output................................................................................................................ 92
- Writing a Blank Line between Each Row ........................................................................................ 92
- Displaying Row Numbers................................................................................................................ 93
- Using the FORMAT= Column Modifier to Format Output ................................................................ 96
- Concatenating Character Strings ................................................................................................... 97
- Inserting Text and Constants between Columns............................................................................... 99
- Using Scalar Expressions with Selected Columns ........................................................................... 101
- Ordering Output by Columns.......................................................................................................... 104
- Grouping Data with Summary Functions ........................................................................................ 107
- Grouping Data and Sorting ............................................................................................................ 109
- Subsetting Groups with the HAVING Clause ................................................................................... 110
- Formatting Output with the Output Delivery System ....................................................................... 112
- ODS and Output Formats............................................................................................................... 113
- Sending Output to a SAS Data Set................................................................................................ 114
- Converting Output to Rich Text Format ........................................................................................ 115
- Exporting Data and Output to Excel .............................................................................................. 116
- Delivering Results to the Web ........................................................................................................ 118
- Summary ................................................................................................................................... 119

## Introduction

Programmers want and expect to be able to format output in a variety of ways. The SQL procedure has forged innovative ways to enhance the appearance of output including double-spacing rows of output, concatenating two or more columns, inserting text and constants between selected columns, displaying column headers for derived fields, and much more. As a value-added feature, the SQL procedure (not part of ANSI-standard SQL—see the “Introduction” section of this book) can be integrated with the Output Delivery System to enhance and format output in ways not otherwise available. As you review the many examples in this chapter, the following points should be kept in mind:

## Formatting Output

As a language, PROC SQL consists of a standard set of statements and options to create, retrieve, alter, transform, and transfer data regardless of the operating system or where the data is located. These features provide tremendous power as well as control when integrating information from a variety of sources in a number of ways. Because emphasis is placed on PROC SQL’s data manipulation capabilities and not on its format and output capabilities, many programmers are unfamiliar with the SQL procedure’s output-producing side. Consequently, programmers resort to using report writers or special outputting tools to create the best looking output. To illustrate the virtues of PROC SQL in SAS, this chapter presents numerous examples of how output can be formatted and produced.

## Writing a Blank Line between Each Row

The ability to display a blank line between each row of output is available as a procedure option in PROC SQL. As with the PRINT procedure, specifying DOUBLE in the SQL procedure inserts a blank line between each physical row of output (NODOUBLE is the default). Setting this option is especially useful when one or more flowed lines spans or wraps in the output because it provides visual separation between each row of data. This example illustrates using the DOUBLE option to double-space output.

### SQL Code

```
PROC SQL DOUBLE;
    SELECT *
        FROM INVOICE;
QUIT;
```

### Results

The SAS System
| Invoice Number | Manufacturer Number | Customer Number | Invoice Quantity - Units Sold | Invoice Unit Price | Product Number |
| 1001 | 500 | 201 | 5 | $1,495.00 | 5001 |
| 1002 | 600 | 1301 | 2 | $1,598.00 | 6001 |
| 1003 | 210 | 101 | 7 | $245.00 | 2101 |
| 1004 | 111 | 501 | 3 | $9,600.00 | 1110 |
| 1005 | 500 | 801 | 2 | $798.00 | 5002 |
| 1006 | 500 | 901 | 4 | $396.00 | 6000 |
| 1007 | 500 | 401 | 7 | $23,100.00 | 1200 |

To revert back to single-spaced output, the RESET statement can be specified as long as the QUIT statement has not been issued to turn off the SQL procedure. When PROC SQL is active, the RESET statement can be specified with or without options to reestablish each option’s original settings. All SQL options are reset to their original settings when RESET is specified without any options. When the RESET statement is specified with one or more options, only those options are reset. This example illustrates using the NODOUBLE option to turn off double-spaced output and reset printing to the default single-spaced output.

### SQL Code

```
PROC SQL;
    RESET NODOUBLE;
QUIT;
```

## Displaying Row Numbers

You can specify an SQL procedure option called NUMBER to display row numbers on output under the column heading Row. As with the Obs column produced by the PRINT procedure, the NUMBER option displays row numbers on output. The next example shows the NUMBER option being specified with the SQL procedure to display row numbers on output.

### SQL Code

```
PROC SQL NUMBER;
    SELECT PRODNUM,
           UNITS,
           UNITCOST
    FROM PURCHASES;
QUIT;
```

### Results

The SAS System
| Row | Prodnum | Units | Unitcost |
| --- | --- | --- | --- |
| 1 | 1110 | 1 | $3,200.00 |
| 2 | 5001 | 7 | $299.00 |
| 3 | 5001 | 11 | $299.00 |
| 4 | 5003 | 8 | $299.00 |
| 5 | 5002 | 4 | $399.00 |
| 6 | 5004 | 3 | $299.00 |
| 7 | 1700 | 2 | $3,400.00 |
| 8 | 1200 | 3 | $3,300.00 |
| 9 | 1110 | 2 | $3,200.00 |
| 10 | 5001 | 3 | $299.00 |
| 11 | 5003 | 5 | $299.00 |
| 12 | 5002 | 2 | $399.00 |
| 13 | 1700 | 2 | $3,400.00 |
| 14 | 1200 | 3 | $3,300.00 |
| 15 | 1110 | 5 | $3,200.00 |
| 16 | 5001 | 9 | $299.00 |
| 17 | 5002 | 5 | $399.00 |
| 18 | 5003 | 8 | $299.00 |
| 19 | 5004 | 2 | $299.00 |
| 20 | 5001 | 11 | $299.00 |

|  |  |  |  |
|---|---|---|---|
| 21 | 5002 | 5 | $399.00 |
| 22 | 5003 | 7 | $299.00 |
| 23 | 5004 | 3 | $299.00 |
| 24 | 1700 | 3 | $3,400.00 |
| 25 | 1200 | 6 | $3,300.00 |
| 26 | 5001 | 6 | $299.00 |
| 27 | 5001 | 6 | $299.00 |
| 28 | 5003 | 9 | $299.00 |
| 29 | 5002 | 4 | $399.00 |
| 30 | 1700 | 3 | $3,400.00 |
| 31 | 5001 | 2 | $299.00 |
| 32 | 5001 | 2 | $299.00 |
| 33 | 2102 | 5 | $175.00 |
| 34 | 2102 | 9 | $175.00 |
| 35 | 2102 | 11 | $175.00 |
| 36 | 2102 | 7 | $175.00 |
| 37 | 2102 | 5 | $175.00 |
| 38 | 2102 | 12 | $175.00 |
| 39 | 2102 | 8 | $175.00 |
| 40 | 2200 | 3 | $130.00 |
| 41 | 2102 | 9 | $175.00 |
| 42 | 5003 | 3 | $299.00 |

| 43 | 5004 | 2 | $299.00 |
| 44 | 1200 | 3 | $3,300.00 |
| 45 | 1700 | 5 | $3,400.00 |
| 46 | 1700 | 3 | $3,400.00 |
| 47 | 1700 | 7 | $3,400.00 |
| 48 | 1700 | 4 | $3,400.00 |
| 49 | 1700 | 5 | $3,400.00 |
| 50 | 1700 | 2 | $3,400.00 |
| 51 | 1200 | 8 | $3,300.00 |
| 52 | 5001 | 3 | $299.00 |
| 53 | 5003 | 5 | $299.00 |
| 54 | 5004 | 1 | $299.00 |
| 55 | 1700 | 4 | $3,400.00 |
| 56 | 5001 | 6 | $299.00 |
| 57 | 2102 | 9 | $175.00 |

## Using the FORMAT= Column Modifier to Format Output

The SQL procedure supports the specification of a FORMAT= column modifier for purposes of providing instructions on how to write character and numeric data values by a query expression. The general syntax for writing a format follows:

```
<$>format<w>.<d>
```

where

$ is used to reference a character format and its absence references a numeric format.

format is the name of the desired SAS format or user-defined format to be used (see the SAS Language Reference: Dictionary, Fourth Edition for a complete listing and description of the available character, numeric, and date formats).

w references the format width, which is typically represented by the number of output columns used for the data.
