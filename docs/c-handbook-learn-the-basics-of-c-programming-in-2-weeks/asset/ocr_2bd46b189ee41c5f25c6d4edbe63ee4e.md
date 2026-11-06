# ### How to Add New Data Rows

The INSERT INTO command allows you to add new data rows to an existing table. This command involves two syntaxes:

# ### The First Syntax

```
```
INSERT INTO TABLE NAME (column1, column2, column3,...columnN)]
VALUES (value1, value2, value3,...valueN);
```
```

You should use this syntax if you want to add data into certain columns.

# ### The Second Syntax

```
```
INSERT INTO TABLE_NAME VALUES (value1,value2,value3,...valueN);
```
```

You must use this syntax if you want to add values to all of the columns of your table. That means you won’t have to identify the columns you are working on. However, make sure that the sequence of the values is the same as that of the existing columns in the table.