```
~~~sql
ON table2.column_n_name=table2.column_n_name;
~~~
```

In some database systems, the RIGHT OUTER JOIN is used instead of LEFT JOIN. Here’s the syntax for this variation:

```
~~~sql
SELECT column_n_name(s)
FROM table1
RIGHT OUTER JOIN table2
ON table2.column_n_name=table2.column_n_name;
~~~
```

[http://www.sql-join.com/sql-join-types/](http://www.sql-join.com/sql-join-types/)

# ## FULL OUTER JOIN

This JOIN operation displays all rows when at least one table meets the condition. It combines the results from both RIGHT and LEFT join operations.

Here’s the syntax:

```
~~~sql
SELECT column_n_name(s)
FROM table1
FULL OUTER JOIN table2
ON table2.column_n_name=table2.column_n_name;
~~~
```

To demonstrate the JOIN operation in SQL, use the Branch_Sales and Branch_Location tables:

Branch_Sales Table

| Branch | Product_ID | Sales |
| --- | --- | --- |
| New York | 101 | 7500.00 |
| Los Angeles | 102 | 6450.00 |
| Chicago | 101 | 1560.00 |
| Philadelphia | 101 | 1980.00 |
| Denver | 102 | 3500.00 |
| Seattle | 101 | 2500.00 |
| Detroit | 102 | 1450.00 |

Location Table

| Region | Branch |
| --- | --- |
| East | New York City |