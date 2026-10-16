```
FROM PRODUCTS
    WHERE PRODCOST > 300;
QUIT;
```

# Results

| Product Name | Product Type | Product Cost |
| Dream Machine | Workstation | $3,200.00 |
| Business Machine | Workstation | $3,300.00 |
| Travel Laptop | Laptop | $3,400.00 |
| Database Software | Software | $399.00 |

PROC SQL also supports the use of truncated string comparison operators. These operators work by first truncating the longer string to the same length as the shorter string, and then perform the specified comparison. The result of using any of the comparison operators has no permanent affect on the strings themselves. The list of truncated string comparison operators and their meanings appear below.

| Truncated String Comparison Operator | Description |
| EQT | Equal to |
| GTT | Greater than |
| LTT | Less than |
| GET | Greater than or equal to |
| LET | Less than or equal to |
| NET | Not equal to |

# Logical Operators

Logical operators are used to connect two or more expressions together in a WHERE or HAVING clause. The available logical operators consist of AND, OR, and NOT. Suppose you want to select only those software products that cost more than $300.00. The example illustrates how the AND operator is used to ensure that both conditions are true.

# SQL Code

```
PROC SQL;
    SELECT PRODNAME,
            PRODTYPE,
            PRODCOST
        FROM PRODUCTS
        WHERE PRODTYPE = 'Software' AND
              PRODCOST > 300;
```