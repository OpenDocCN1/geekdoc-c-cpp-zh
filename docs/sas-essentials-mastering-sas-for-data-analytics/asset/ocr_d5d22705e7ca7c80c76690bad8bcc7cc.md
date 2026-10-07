# METHODS OF READING DATA INTO SAS 35

| TABLE 2.8 Example SAS (Output) FORMATs |
| Format | Meaning |
| --- | --- |
| 5. | Write data using five columns with no decimal points. For example, 12345 |
| 5.1 | Write data using five columns with one decimal point. For example, 123.4 places. |
| DOLLAR10.2 | Write data with a dollar sign, commas at thousands, and with two decimal places. For example, $1234.56 |
| COMMA10.1 | Write data with commas at thousands and one decimal place. For example, 1,234.5 |
| MMDDY10.1 | Displays days in common American usage as in 01/09/2016 |
| DATE9. | Displays time using a military style format. For example, 09JAN2016 |
| WORDDATE12. | Displays days with abbreviated month names as in Jan, 2016 |
| WORDDATE18. | Displays days with full month names as in January, 2016 |
| WEEKDATE29. | Displays days with day of week as in Saturday, January 9, 2016 |
| BESTW. | Prints out numbers with maximum precision according to the designated width |

tells SAS to use the format DOLLAR10.2 when displaying the variable OWE PROC PRINT (or any other procedure). The general syntax for the FORMAT statement is follows:

FORMAT VAR1. VAR2 VAR3 VAR4 FORMAT2.etc. . . ;

FORMAT is the keyword that begins the statement. VAR1 is a variable name to which a format is applied and FORMAT1 is the name of the FORMAT (3., COMMA6., etc.) to apply to VAR1 in this case. FORMAT2, applies to VAR2, VAR3, and VAR4. You may define any number of formats to variables within this statement. Some commonly used formats are listed in Table 2.7. Note that a specification used as an input format can also be used as an output format, so there are some that are the same as in Table 2.8.

> If a data has a decimal such as 4.9 and you output the data using a format such as 4. that does not have a decimal place, SAS will output a rounded integer (i.e., in this case, 4.9 gets rounded to 5).

The following example illustrates how you could use both INFORMATs and FORMATs in a SAS program.

```
DATA REPORT;
INPUT _1 NAME $10 @11 SCORE 5.2 @18 DATE9;
FORMAT WORDDATE12;
```

This code uses the DATE9. input format to read in a data value called BDATE. The FORMAT statement tells SAS to output the same value, this time using the (output) format WORDDATE12. For the SCORE value, the number is read in a 5.2 input format. No format is defined for this value, so it is output using the SAS default format, which in this case is called the BEST12. format, which writes out a number to the most possible decimals. In this case, there are two decimal places read in, so two are written out.