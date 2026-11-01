# PERSISTING DATASET CHANGES

After editing data within a DataSet, it is usually necessary to persist these changes. The most common example is selecting data from a database, displaying it to the user, and returning those updates to the database.

In a less "connected" application, changes might be persisted to an XML file, transported to a middle-tier application server, and then processed to update several data sources.

A DataSet class can be used for either of these examples; what's more, it's easy to do.

# Updating with Data Adapters

In addition to the SelectCommand that a SqlDataAdapter most likely includes, you can also define an InsertCommand, UpdateCommand, and DeleteCommand. As the names imply, these objects are instances of the command object appropriate for your provider such as SqlCommand and OleDbCommand.

With this level of flexibility, you are free to tune the application by judicious use of stored procedures for frequently used commands (say SELECT and INSERT), and use straight SQL for less commonly used commands such as DELETE. In general, it is recommended to provide stored procedures for all database interaction because it is faster and easier to tune.

This example uses the stored procedure code from the "Calling Stored Procedures" section for inserting, updating, and deleting Region records, coupled with the RegionSelect procedure written previously, which produces an example that uses each of these commands to retrieve and update data in a DataSet class. The main body of code is shown in the following section.

# Inserting a New Row

You can add a new row to a DataTable in two ways. The first way is to call the NewRow() method, which returns a blank row that you then populate and add to the Rows collection, as follows:

```
DataRow r = ds.Tables["Region"].NewRow();
r["RegionID"]=999;
r["RegionDescription"]="North West";
ds.Tables["Region"].Rows.Add(r);
```

The second way to add a new row would be to pass an array of data to the Rows.Add() method as shown in the following code:

```
DataRow r = ds.Tables["Region"].Rows.Add
    (new object[] { 999, "North West" });
```

Each new row within the DataTable will have its RowState set to Added. The example dumps out the records before each change is made to the database, so after adding a row (either way) to the DataTable, the rows will look something like the following. Note that the right-hand column shows the row's state:

```
New row pending inserting into database
1  Eastern        Unchanged
2  Western        Unchanged
3  Northern       Unchanged
4  Southern       Unchanged
999 North West    Added
```

To update the database from the DataAdapter, call one of the Update() methods as shown here:

```
da.Update(ds, "Region");
```

For the new row within the DataTable, this executes the stored procedure (in this instance RegionInsert). The example then dumps the state of the data, so you can see that changes have been made to the database.