# How to Modify Existing Records

In the SQL language, you may edit existing records using the UPDATE query. This query, which is applied on the WHERE clause, allows you to edit data rows. Here ’ s the syntax that you should use:

```
UPDATE table name
SET column1 = value1, column2 = value2..., columnN = valueN
WHERE [condition];
```

# How to Delete Records

If you want to delete records, you may use SQL ’ s DELETE Query. You can combine this query with SELECT to delete certain rows. On the other hand, you may use DELETE as a standalone query to delete all of the data rows. Here ’ s the syntax of this query:

```
DELETE FROM the_table ’ s_name
WHERE [specify you condition/s];
```

If you need to remove all the records from a table, you may simply remove the WHERE clause. Thus, the syntax will be:

```
DELETE FROM the_table ’ s_name;
```