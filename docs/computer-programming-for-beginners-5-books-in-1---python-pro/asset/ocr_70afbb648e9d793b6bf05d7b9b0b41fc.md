| ID | FIRST_NAME | LAST_NAME | CAPITAL | ADDRESS |
|---|---|---|---|---|
| 1 | Robert | Page | 5000 | 282 Patterson Avenue, Illinois |
| 2 | John | Halley | 7000 | 5 Lake View New York |
| 3 | Kristen | Johnston | 4000 | 35 Jump Road Florida |
| 4 | Jack | Burns | 5000 | 5 Green Meadows California |
| 5 | James | Hunt | 7500 | NULL |

5 rows in set (0.00 sec)

# Adding a New Column

Since you're now working on a different set of data, you may decide to add another column to make the data on the INVESTORS table more relevant. You can add a column that will store the number of stocks owned by each investor. You may name the new column STOCKS. This column will accept integers up to 9 digits.

You can use the following statement to add the STOCKS column:

```
ALTER TABLE INVESTORS ADD STOCKS INT(9);
```

The following is the updated INVESTORS table: