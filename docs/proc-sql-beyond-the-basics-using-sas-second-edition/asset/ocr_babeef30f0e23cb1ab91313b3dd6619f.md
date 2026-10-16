# Results

| Product Name | Product Type | DISCOUNT_PRICE | LOSS |
|---|---|---|---|
| Analog Cell Phone | Phone | $28.00 | $7.00 |
| Office Phone | Phone | $104.00 | $26.00 |
| Digital Cell Phone | Phone | $140.00 | $35.00 |
| Spreadsheet Software | Software | $239.20 | $59.80 |
| Graphics Software | Software | $239.20 | $59.80 |
| Wordprocessor Software | Software | $239.20 | $59.80 |
| Database Software | Software | $319.20 | $79.80 |
| Dream Machine | Workstation | $2,560.00 | $640.00 |
| Business Machine | Workstation | $2,640.00 | $660.00 |
| Travel Laptop | Laptop | $2,720.00 | $680.00 |

# Character String Operators and Functions

Character string operators and functions are typically used with character data. Numerous operators are presented to acquaint programmers with the power available with in SQL procedure. As you become familiar with each operator, you’ll find their real strength as you begin to nest functions within each other.

# Concatenating Strings

The following example illustrates a basic concatenation operator that is used to concatenate two columns and a text string. Note that the created column is without a name and has a total length of 23 characters. For more details and special formatting considerations, the concatenation operator "||"will be discussed in greater detail in Chapter 3, “Formatting Output.”

# SQL Code

```
PROC SQL;
    SELECT MANUCITY || "," || MANUSTAT
        FROM MANUFACTURERS;
QUIT;
```