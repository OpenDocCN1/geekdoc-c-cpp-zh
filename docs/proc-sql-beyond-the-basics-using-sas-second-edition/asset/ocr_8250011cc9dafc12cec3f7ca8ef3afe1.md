# SAS Log Results

```
PROC SQL;
    SELECT *
        FROM PURCHASES (RENAME=ITEM=ITEM_PURCHASED);
    QUIT;
NOTE: PROCEDURE SQL used:
    real time            0.31 seconds
    cpu time             0.02 seconds
```

# Renaming a Table

The SQL procedure does not provide a standard ANSI approach to renaming a table in a SAS library. Consequently, the DATASETS procedure is the recommended method to accomplish this relatively simple task. Suppose that you want to rename the PRODUCTS table in the WORK library to MANUFACTURED_PRODUCTS.

# SAS Code

```
PROC DATASETS LIBRARY=WORK DETAILS;
    CHANGE PRODUCTS = MANUFACTURED_PRODUCTS;
QUIT;
```

# SAS Results

| Directory |
|---|---| 
| Libref | WORK |
| Engine | V9 |
| Physical Name | C:\Users\KPL\AppData\Local\Temp\SAS Temporary Files\_TD3004_KPL-PC_ |
| Filename | C:\Users\KPL\AppData\Local\Temp\SAS Temporary Files\_TD3004_KPL-PC_ |

| # | Name | Member Type | Obs, Entries or Indexes | Vars | Label | File Size | Last Modified |
|---|---|---|---|---|---|---|---|
| 1 | CUSTOMERS | DATA | 18 | 3 |  | 5120 | 01Sep13:20:09:10 |
| 2 | INVENTORY | DATA | 7 | 5 |  | 5120 | 01Sep13:20:09:10 |
| 3 | INVOICE | DATA | 7 | 6 |  | 5120 | 01Sep13:20:09:10 |
| 4 | MANUFACTURED_PRODUCTS | DATA | 10 | 5 |  | 17408 | 01Sep13:20:09:10 |
|  | MANUFACTURED_PRODUCTS | INDEX | 2 |  |  | 13312 | 01Sep13:20:09:10 |
| 5 | MANUFACTURERS | DATA | 6 | 4 |  | 5120 | 01Sep13:20:09:10 |
| 6 | PURCHASES | DATA | 57 | 4 |  | 5120 | 01Sep13:20:09:10 |