+   - INNER JOIN
+   - LEFT OUTER JOIN
+   - RIGHT OUTER JOIN
+   - FULL OUTER JOIN

# Inner join

Inner join selects the entire record from Table A and Table B where the Join condition is satisfied. The syntax for creating inner join in SQL is defined as follows:

```
SELECT column name
FROM table1
INNER JOIN table 2
ON table1.column_name = table2.colmn_name;
```

# Left Join

The Left join selects the entire record from Table A combined with the records from Table B where the join condition is satisfied. Syntax for creating LEFT JOIN in SQL is defined as follows:

```
SELECT column name
FROM table1
LEFT JOIN table 2
ON table1.column_name = table2.colmn_name;
```

# Right Join

The Right join select all records from Table B combined with the records from Table A where the join condition is satisfied. Syntax for creating RIGHT JOIN in SQL is defined as follows:

```
SELECT column name
FROM table1
RIGHT JOIN table 2
ON table1.column_name = table2.colmn_name;
```

# Full outer Join

The Full outer Join selects all records from Table A and Table B even if the join condition is not met. Syntax for creating FULL JOIN in SQL is defined as follows:

```
SELECT column name
FROM table1
FULL OUTER JOIN table 2
ON table1.column_name = table2.colmn_name
WHERE condition;
```