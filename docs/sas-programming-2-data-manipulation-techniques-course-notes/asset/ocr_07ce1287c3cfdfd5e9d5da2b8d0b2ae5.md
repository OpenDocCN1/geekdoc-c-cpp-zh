# Execution: Correct Program

```
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3.;
if Location='USA' then
input @10 SaleDate mddyyy1.
@20 Amount 7;
elelse if Location='EUR' then
input @10 SaleDate date9.
@20 Amountmaxx7;
```

> Do not read new record at next INPUT statement

run;

Input Buffer

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---||
| 1 | 0 | 1 | | U | S | A | | 1 | - | 2 | - | 2 | 0 | 1 | 1 | | 3 | 2 | 9 | 5 | . | 5 | 0 | | | |

| SaleID | Location | SaleDate | Amount |
|---|---|---|---||
| $4 | | N 8 | N 8 |

PDV

| SaleID | Location | SaleDate | Amount |
|---|---|---|---||
| $4 | | N 8 | N 8 |
| 101 | USA | 1-20-2011 | 329.50 |

# Execution: Correct Program

```
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3.;
if Location='USA' then
input @10 SaleDate mddyyy1.
@20 Amount 7;
else if Location='EUR' then
input @10 SaleDate date9.
@20 Amountmaxx7;
```

True

run;

Input Buffer

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---||
| 1 | 0 | 1 | | U | S | A | | 1 | - | 2 | - | 2 | 0 | 1 | 1 | | 3 | 2 | 9 | 5 | . | 5 | 0 | | | |

PDV

| SaleID | Location | SaleDate | Amount |
|---|---|---|---||
| $4 | | N 8 | N 8 |
| 101 | USA | 1-20-2011 | 329.50 |