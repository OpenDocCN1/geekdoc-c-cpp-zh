# 250 Learning SAS as Example: A Programmermer's Guide, Second Edition

To display summary statistics for each value of one or more GROUP or ORDER variables, use the BREAK statement. If you want to see the total Quantity and TotalSales for each region in the Sales data set, use the following program:

# Program 15.15: Demonstrating the BREAK Statement of PROC REPORT

```
title "Producing Report Breaks";nproc report data=Learn.Sales;
column Region TotalSales;
define Region / order width=8 format=comma8;
define Quantity / sum "Total Sales" width=9
define TotalSales / sum format=dollar9;
break after region / summarize;
```

The BREAK statement uses the same location keywords as the RBREAK statement. With the BREAK statement, you also need to specify one or more GROUP or ORDER variables that determine where to print the summary statistics. The option SUMMARIZE provides the appropriate summary statistic after the break. In Program 15.15, a line showing the sum of Quantity and TotalSales is printed for each change in the Region value. The output from this program is follows:

# Program 15.14: Output from Program 15

| Region | Quantity | Total Sales |
| East | 100 | $699 |
| | 100 | $899 |
| | 500 | $19,995 |
| | 2 | $20,000 |
| East | 702 | $41,593 |

| Region | Quantity | Total Sales |
| West | 50 | $300 |
| | 1,000 | $1,990 |
| West | 1,050 | $2,290 |

If you don't want the summary line to contain the values of the BREAK variable(s), use the SUPPRESS option, like this:

```
break after region / summarize suppress;
```