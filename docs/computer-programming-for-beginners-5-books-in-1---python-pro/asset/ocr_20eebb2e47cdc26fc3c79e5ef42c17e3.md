```
```sql
mysql> SELECT * FROM EMPLOYEES
    -> ORDER BY SALARY DESC;
```
```

| ID | NAME | ADDRESS | AGE | SALARY |
|---:|---|---|---:|---:|
| 5 | Nicholas | nicol442 | 45 | 5000.00 |
| 3 | Joel | Joel42 | 30 | 4000.00 |
| 7 | Grace | gra361 | 35 | 4000.00 |
| 2 | Mercy | Mercv32 | 25 | 3500.00 |
| 4 | Alice | Alic442 | 31 | 2500.00 |
| 6 | Milly | mi1342 | 32 | 2000.00 |

6 rows in set (0.05 sec)

mysql>

[https://www.tutorialspoint.com/sql/sql-top-clause.htm](https://www.tutorialspoint.com/sql/sql-top-clause.htm)

# GROUP BY Clause

This clause is used together with the SELECT statement to group data that is related together, creating groups. The GROUP BY clause should follow the WHERE clause in SELECT statements, and it should precede the ORDER BY clause.

The following is the syntax:

```
SELECT column_1, column_2
FROM tableName
WHERE [ conditions ]
GROUP BY column_1, column_2
```