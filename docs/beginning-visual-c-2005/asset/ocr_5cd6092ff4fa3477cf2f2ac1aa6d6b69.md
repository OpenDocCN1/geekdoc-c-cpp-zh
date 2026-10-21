ID from one table matched the same field in the other table. This would combine each record from the Products table with the records from the Orders table that related to that product. The statement to do this is:

```
SELECT * FROM Products,Orders
WHERE Products.[Product ID] = Orders.[Product ID];
```

Notice how a specific field for a particular table is identified here. You add the table name as a prefix and separate it from the field name with a period. This qualification of the field name is essential where the same field name is used in both tables. Without the table name, there’s no way to know which of the two fields you mean. With this SELECT statement and the same table contents used previously, you’ll get the recordset shown in Figure 19-5.

Of course, this may still be unsatisfactory because you have two fields containing the Product ID, but you could easily remove this by specifying the field names you want, instead of the * in the SELECT statement. The columns with the same column name, however, would be distinguished by being qualified by the names of the original table when they appear in the recordset.

![](bbox=[0.08, 0.48, 0.92, 0.82])

Result of Join Operation with the condition:
Products."Product ID" = Orders."Product ID"

Figure 19-5