3. The SqlDataAdapter contains all of the commands necessary to interact with the data source. There are two ways to add insert, update, and delete commands : via SqlDataAdapter properties or with a SqlCommandBuilder.

```
-Using SqlCommandBuilder
SqlCommandBuilder cmdBldr = new SqlCommandBuilder(daBooks);
```

4. SqlCommandBuilder is instantiated with a single constructor parameter of the SqlDataAdapter, daBooks, instance. This tells the SqlCommandBuilder what SqlDataAdapter to add commands to. The SqlCommandBuilder will read the SQL select statement (specified when the SqlDataAdapter was instantiated), infer the insert, update, and delete commands, and assign the new commands to the Insert, Update, and Delete properties of the SqlDataAdapter, respectively.

Note that, SqlCommandBuilder would work for single table and not for multiple table joins.

# Filling the DataSet

```
daBooks.Fill(dsBooks, "Books");
```

The Fill method, in the code above, takes two parameters : A DataSet and a table name. The DataSet must be instantiated before trying to fill it with data. The second parameter is the name of the table that will be created in the DataSet.

The Fill method has an overload that accepts one parameter for the DataSet only. In that case, the table created has a default name of "table1" for the first table. The number will be incremented (table2, table3, ..., tableN) for each table added to the DataSet where the table name was not specified in the Fill method.

# Using the DataSet

A DataSet will bind with both ASP.NET and Windows forms DataGrids.

```
//Illustration with of DataSet assigned to a Windows forms DataGrid
dgBooks.DataSource = dsBooks;
dgBooks.DataMember = 'Books';
```

DataSet is assigned to the DataSource property of the DataGrid.

To specify exactly which table to use, set the DataGrid's DataMember property to the name of the table.

# Updating Changes

After modifications are made to the data, if it is to be updated to actual database, the Update method of the SqlDataAdapter is used to put modifications to the database.

```
daBooks.Update(dsBooks, "Books");
```

The Update method, above, is called on the SqlDataAdapter instance that originally filled the dsBooks DataSet. The second parameter to the Update method specifies which table, from