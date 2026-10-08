# 9-14 Chapter 9 Combining SAS® Data Sets

1. Submit step 1 to sort orion.order_fact by Customer_ID, create work.order_fact, and match-merge orion.order_customer with the newly created set work.order_fact.

```
*** Step 1 ****************************************************
proc sort data=orion.order_fact
    out=work.order_fact;
    by Customer_ID;
    where year(Order_Date)=2007;
run;

data custard;
    merge orion.customer(in=cust)
           work.order_fact(in=order);
    by Customer_ID;
    if cust=1 and order=1;
        keep Customer_ID Customer Name Quantity
        Total_Retail Price Product_ID;
run;
```

2. Examine the output data set, work.custord. Notice that it contains only matches, with a total of 128 observations.

Partial PROC PRINT Output

| Obs | Customer_ID | Customer_Name | Product_ID | Quantity | Total_Retail_Price |
|---|---|---|---|---|-|
| 1 | 5 | Sandrina Stefano | 23010050026 | 1 | $247.50 |
| 2 | 5 | Sandrina Stefano | 24010100433 | 1 | $3.00 |
| 3 | 5 | Sandrina Stefano | 24070300032 | 2 | $43.98 |
| 4 | 5 | Sandrina Stefano | 23010500093 | 2 | $285.60 |
| 5 | 5 | Sandrina Stefano | 23100600030 | 1 | $86.30 |

3. Submit step 2 to sort work.custord by Product_ID. Match-merge work.custord with orion.product_dim by Product_ID.

```
*** Step 2 ******************************************************
proc sort data=custord;
    by Product_ID;
run;

data custardprod;
    merge custard(in=ord)
           orion.product_dim(in=prod);
    by Product_ID;
    if ord=1 and prod=1;
        Supplier=catx(' ', Supplier_Country, Supplier_ID);
        keep Customer_Name Quantity
        Total_Retail Price Product Name Supplier;
run;
```

4. Examine the output data set, work.custordprod. It is in order by Product_ID.