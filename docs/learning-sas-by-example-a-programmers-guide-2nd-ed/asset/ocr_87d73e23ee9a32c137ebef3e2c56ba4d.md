# 222 Learning SAS by Example: A Programmer's Guide, Second Edition

The variable (or variables) you place in the ID statement replaces the Obs column and is printed in the left-columns of your listing.

Notice when you place a variable name in the ID statement, you do not list it in the VAR statement. If you do, that appears twice in the listing.

An alternative way to omit the Obs column is to use PROC PRINT with the option NOOBS. The advantage of using an ID statement is that the ID variable begins each page if you have more variables that will fit across a single page.

# 14.4 Changing the Appearance of Values

Suppose you would like the TotalSales values to appear with dollar signs and commas. You can change the appearance of values in your listing by associating a format with one or more variables. SAS has built-in formats that can add dollar signs to numbers or display dates in different ways. 14.4 adds a FORMAT statement to list TotalSales with dollar signs and Quantity with

Program 14.4: Adding a FORMAT statement to PROC PRINT

```
title "Listing of Sales";nproc print data=Learn.Sales;
id EmpID;
var Customer Quantity TotalSales dollar$10.2 comma7;
run;
```

Notice the change in the Quantity and TotalSales columns.

Figure 14.4: Partial Listing from Program 14.4

| Listing of Sales |
| EmpID | Customer | Quantity | TotalSales |
|---|---|---||}{
| 1843 | Barco Corporation | 50 | $449.50 |
| 1843 | Cost Cutter's | 100 | $599.00 |
| 1843 | Minimart Inc. | 3 | $15,597.00 |
| 1843 | Barco Corporation | 1 | $5,129.00 |
| 1843 | Ely Unlimited | 10 | $299.50 |
| 0177 | Food Unlimited | 100 | $699.00 |
| 0177 | Shop and Drop | 100 | $899.00 |
| 1843 | Cost Cutter's | 1 | $919.00 |
| 9888 | Cost Cutter's | 50 | $299.50 |
| 9888 | Pet's are Us | 1,000 | $1,990.00 |