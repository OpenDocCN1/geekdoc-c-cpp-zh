records are kept in a set for subsequent analyses on that particular data set. The WHERE
statement affects only the data used for a particular procedure. For example, in the ID
example, suppose you want to output data only for procedure A in the PROC PRINT state-
ment. Use the statement

```
WHERE TRT="A";
```

in the PROC PRINT (or any) procedure to limit the analysis to only those records that
meet the criteria in the WHERE statement. Subsequent procedures within the same SAS
program will not be subject to the WHERE restriction unless it is invoked again for
procedure.

# HANDS-ON EXAMPLE

In this example, you will learn how to use the WHERE statement.

+   1. In the SAS file D_ID.SAS used in the previous Hands-on Example, modify the PROC
PRINT statement to read:

PROC PRINT LABEL DATA=WEIGHT;
ID_RAT;
LABEL TRT='Treatment';
WHERE TRT="A";
RUN;
2. Run the program and observe the output given in Table 5.9. Note that the WHERE
statement only changed the output for the PROC PRINT (where it was used) and not
the PROC MEANS procedure.

Only the records that match the criterion specified by the WHERE statement are
included in the output.

TABLE 5.9 Selection Using the Where Statement
| RAT_ID | MDATE | WT_GRAMS | Treatment | PINKEYE |
|---|---|---|---|{}|
| 001 | 03FEB2009 | 93 | A | Y |
| 003 | 04FEB2009 | 103 | A | Y |
| 005 | 07FEB2009 | 99 | A | Y |

# 5.6 USING PROC PRINT

Although several previous examples have used a simple version of the PROC PRINT pro-
cedure, a number of options for this procedure have not been discussed. As demonstrated
in previous examples, PROC PRINT outputs the data values in a SAS data set.