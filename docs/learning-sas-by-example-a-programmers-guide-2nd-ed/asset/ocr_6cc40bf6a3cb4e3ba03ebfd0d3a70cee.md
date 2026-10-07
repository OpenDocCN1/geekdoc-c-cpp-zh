```
proc report data=Learn.Sales;
column EmpID Quantity TotalSales;
  define EmpID / order "Employee ID" width=8;
  define Quantity / width=8 format=comma8;
  define TotalSales / "Total Sales" width=9
    format=dollar9;
```

The keyword ORDER in the DEFINE statement for EmpID produces the report in order of ascending EmpID. This saves you the trouble of having to sort your data set prior to requesting the report.
The resulting report is shown next:

Figure 15.10: Output from Program 15.11

| Employee ID | Quantity | TotalSales |
|---|---|---||
| 0017 | 100 | $1,995 |
| | 500 | $19,995 |
| 0177 | 5 | $53 |
| | 100 | $699 |
| | 100 | $889 |
| | 2 | $20,000 |
| 1843 | 10 | $300 |
| | 50 | $450 |
| | 100 | $599 |
| | 1 | $5,129 |
| | 1 | $9,109 |
| | 3 | $15,597 |
| | 3 | $15,597 |
| 9888 | 50 | $300 |
| | 1,000 | $1,990 |

# 15.10 Applying the ORDER Usage to Two Variables

You can apply the ORDER usage to several variables. For example, suppose you want the same report as the one produced by Program 15.11, but you want to see the total sales for each employee in decreasing order of total sales. Here is the program: