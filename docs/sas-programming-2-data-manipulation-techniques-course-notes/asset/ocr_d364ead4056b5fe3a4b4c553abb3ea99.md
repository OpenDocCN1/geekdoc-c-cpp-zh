# 3.1 Creating an Accumulating Total Variable

# Level 1

# 1. Creating Accumulating Totals

The data set orion.order_fact contains information about orders for several years, sorted by Order_Date. Each observation represents one order, and Total_Retail_Price contains the sales value for the order.

Partial Listing of orion.order_fact (617 Total Observations, 12 Total Variables)

| Order_ID | Date | Total_Retail_Price |
|---|---|*|
| 123005823 | 11JAN2007 | $16.50 |
| 123008011 | 15JAN2007 | $247.50 |
| 123016683 | 20JAN2007 | $28.30 |
| 123014744 | 28JAN2007 | $32.00 |
| 123031508 | 27FEB2007 | $63.60 |

+   Orion Star would like to examine growth in sales during the date range of 01Nov2008 to 14Dec2008.
- Open file p203e01. It creates and produces a data set named work.mid_q4 orion.order_fact. The DATA step uses the WHERE statement to read only the observations in the specified date:
- Modify the program to create an accumulating total, Sales2Dte, to display the sales-to-date total.
- Also create an accumulating variable, Num_Orders, indicating how many orders-to-date that total represent. Each observation counts as one order.

```
where '01Nov2008'd <= Order_Date <= '14Dec2008'd;
```

+   Modify the PROC PRINT step to show your results.
- Display Sales2Dte with a DOLLAR10.2 format.
- Show only the columns Order_ID, Order_Date, Total_Retail_Price, Sales2Dte, and Num_Orders.

| Obs | Order_ID | Date | Total_Retail_Price | Sales2Dte | Num Orders |
|---|---|---|---|---|*|
| 1 | 123403037 | 01NOV2008 | $53.70 | $53.70 | 1 |
| 2 | 123409222 | 10NOV2008 | $7.20 | $60.90 | 2 |
| 3 | 123413379 | 17NOV2008 | $328.30 | $389.20 | 3 |
| 4 | 123418633 | 25NOV2008 | $200.10 | $589.30 | 4 |
| 10 | 1234031319 | 1DEC2008 | $105.60 | $1,664.20 | 10 |

Partial PROC PRINT Output from 01Nov2008 through 14Dec2008

# Level 2

# 2. Creating Accumulating Totals with Conditional Logic

The data set orion.order_fact contains a group of orders across several years, sorted by Order_Date.