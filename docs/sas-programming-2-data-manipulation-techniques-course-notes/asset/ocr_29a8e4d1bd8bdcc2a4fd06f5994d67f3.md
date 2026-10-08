# Completed Business Scenario Program

Use the SUM, MEAN, and N functions to calculate the donation statistics.

```
data donation_stats;
  set orion.employee;
  keep Employee_ID Total AvgQt NumQt;
  Total=sum(of Qtr1-Qtr4);
  AvgQt=round(mean(of Qtr1-Qtr4));
  NumQt=n(of Qtr1-Qtr4);
run;
proc print data=donation_stats noobs;
  var Employee_ID Total AvgQt NumQt;
run;
```

| Employee_ID | Total | AvgQt | NumQt |
|---|---|---||}{
| 120265 | 25 | 25 | 1 |
| 120267 | 60 | 15 | 4 |
| 120269 | 80 | 20 | 4 |

# Exercises

If you restarted your SAS session since the last exercise, open and submit the libname.sas program found in the data folder.

# Level 1

# 8. Calculating Statistics and Round

The set orion.orders_midyear contains an observation for each customer, with the total retail value of the monthly orders for the first half of the year.

Partial Listing of orion.orders_midyear (24 Total Observations)

| Customer_ID | month1 | month2 | month3 | month4 | month5 | month6 |
|---|---|---|---|---|---||}{
| 5 | 213.1 | | 478.0 | 525.80 | 394.35 | 191.79 |
| 10 | 188.1 | 414.09 | 2876.9 | | 2373.44 | 169.29 |
| 11 | 78.2 | | | | | 70.38 |
| 12 | 135.6 | | | 117.6 | 129.36 | 97.02 | 122.04 |
| 18 | | | | 29.4 | 32.34 | 24.26 |
| 24 | | 265.80 | | | | | 83.70 |
| 27 | 310.7 | 782.90 | | | | | 279.63 |
| 31 | 1484.3 | 293.30 | | | | | 1335.87 |
| 34 | 642.5 | | | 86.3 | 94.93 | 71.20 | 578.25 |

+   a. Create a data set work.sale_stats with three new variables for all months in which the customer placed an order.
  * The variable AvgMonth should contain the average.