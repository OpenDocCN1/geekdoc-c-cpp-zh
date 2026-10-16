# Results

The SAS System

| Product Number | Inventory_Status |
|---|---|
| 5001 | Low on Stock - Reorder |
| 5002 | Low on Stock - Reorder |
| 5001 | Low on Stock - Reorder |
| 1700 | Stock Levels OK |
| 5003 | Stock Levels OK |
| 1110 | Plenty of Stock |
| 5004 | Plenty of Stock |

# Logic and Nulls

The existence of null values frequently introduces complexities for programmers. Instead of coding two-valued logic conditions, such as “True” and “False,” logic conditions must be designed to handle three-valued logic: “True,” “False,” and “Unknown.” When developing logic conditions, programmers need to be ready to deal with the possibility of having null values. Program logic should test whether the current value of an expression contains a value or is empty (null).

Let’s examine a CASE expression that is meant to handle the possibility of having missing values in a table. Returning to an example presented earlier in this chapter, suppose that you want to assign a value of “South East,” “Central,” “South West,” “Missing,” or “Unknown” to each of the manufacturers based on their state of residence.

# SQL Code

```
PROC SQL;
    SELECT MANUNAME,
           MANUSTAT,
           CASE
               WHEN MANUSTAT = 'CA' THEN 'South West'
               WHEN MANUSTAT = 'FL' THEN 'South East'
               WHEN MANUSTAT = 'TX' THEN 'Central'
               WHEN MANUSTAT = ' ' THEN 'Missing'
               ELSE 'Unknown'
           END AS Region
    FROM MANUFACTURERS;
QUIT;
```