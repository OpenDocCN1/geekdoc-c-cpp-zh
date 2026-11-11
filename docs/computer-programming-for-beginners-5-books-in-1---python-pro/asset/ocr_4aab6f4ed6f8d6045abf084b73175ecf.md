comes after the FROM statement.

EQUALS – This is used to find an exact match. The syntax below uses the WHERE clause for a column that contains the exact string of ‘Value’. Note that strings need single quotes around them, while numerical values do not.

```
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 = 'Value'
```

BETWEEN – Typically used to find values between a certain range of numbers or date ranges. It’s important to note that the first value in the BETWEEN comparison operator should be lower than the value on the right. Note the example below comparing between 10 and 100.

```
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 BETWEEN 10 AND 100
```

GREATER THAN, LESS THAN, LESS THAN OR EQUAL TO, GREATER THAN OR EQUAL TO – SQL Server has comparison operators that you can use to compare certain values.

```
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 <= 1000 --Note that you can also use <, >, >= or even <> for not equal to
```

LIKE – This searches for a value or string that is contained within the column. You still use single quotes but include the percent symbols indicating if the string is in the beginning, end or anywhere between ranges of strings.

```
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 LIKE '%Value%' --Searches for the word 'value' in any field
```

```
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 LIKE 'Value%' --Searches for the word 'value' at the
```