# Execution: Formatted Input

```
data work.discounts;
infile "&path\offers.dat";
input @1 Cust_type 4.
@5 Offer dt mmddyy8.
@14 Item gp $8.
@22 Discount percent3.;
```

Input Buffer 1
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5
10 4 0 1 2 / 0 2 / 11 u t d o o r s 1 5%

| Cust_type | Offer_dt | Item_gp | Discount |
| N 8 | N 8 | $8 | N 8 |

# Execution: Formatted Input

```
data work.discounts;
infile "&path\offers.dat";
input @1 Cust_type 4.
@5 Offer dt mmddyy8.
@14 Item gp $8.
@22 Discount percent3.;nPDV
```

Input Buffer 1
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5
10 4 0 1 2 / 0 2 / 11 u t d o o r s 1 5%

| Cust_type | Offer_dt | Item_gp | Discount |
| N 8 | N 8 | $8 | N 8 |
| 1040 | | |