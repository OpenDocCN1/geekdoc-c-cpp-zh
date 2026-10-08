# Execution: Formatted Input

```
data work.discounts;
infile "&path\offers.dat"; Initialize PDV
input @1 Cust type 4.
@5 Offer dt mmddyy8.
@14 Item gp $8.
@22 Discount percent3.
run;
```

|Input Buffer 1 2
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5|

|Cust_type | Offer_dt | Item_gp | Discount
|---|---|---|---|n|N 8 | N 8 | $8 | N 8 |

# Execution: Formatted Input

```
data work.discounts; Specify input data file
infile "&path\offers.dat";
input @1 Cust type 4.
@5 Offer dt mmddyy8.
@14 Item gp $8.
@22 Discount percent3.
run;
```

|Input Buffer 1 2
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5|

|Cust_type | Offer_dt | Item_gp | Discount
|---|---|---|---|n|N 8 | N 8 | $8 | N 8 |