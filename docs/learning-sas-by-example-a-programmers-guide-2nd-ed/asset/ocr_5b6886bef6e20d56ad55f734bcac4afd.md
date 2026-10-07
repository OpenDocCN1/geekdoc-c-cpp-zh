# 14.5 Controlling the Observations That Appear in Your Listing

You can also control which observations appear in a listing by including a WHERE statement in the procedure. For example, suppose you want your listing to contain only observations where the Quantity is greater than 400. The following program would do the trick:

Program 14.5: Controlling Which Observations Appear in the Listing (WHERE Statement)

```
title "Listing of Sales with Quantities Greater than 400";
proc print data=Learn.Sales;
where Quantity gt 400;
id EmpID;
var Customer Quantity TotalSales;
format TotalSales dollar$10.2 Quantity comma7;
run;
```

Figure 14.5: Output from Program 14.5

Listing of Sales with Quantities Greater than 400
| EmpID | Customer | Quantity | TotalSales |
|---|---|---||
| 9888 | Pet's are Us | 1,000 | $1,990.00 |
| 0017 | Roger's Spirits | 500 | $19,995.00 |

Suppose you want to see the sales for two employees: 1843 and 0177. Using an IN operator with a WHERE statement is a convenient way to do this, as shown in Program 14.6.

Program 14.6: Using the IN Operator in a WHERE Statement

```
title "Listing of Sales from Employees 1843 and 0177";
proc print data=Learn.Sales;
where EmpID in ('1843','0177');
id EmpID;
var Customer Quantity TotalSales;
format TotalSales dollar$10.2 Quantity comma7;
run;
```