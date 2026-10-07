# Data Inserting with Visual C#.NET

Because methods 1 and 2 are relatively simple, in this part we will concentrate on inserting data into the database using the TableAdapter methods. First we discuss how to insert records directly into the database using the TableAdapter.Insert() method, and then we discuss how to insert new records into the database using the TableAdapter.Update() method. Method 3 will be discussed in Part II since it contains more completed coding process related to the runtime objects.

# 6.1.1 Insert New Records INTO A Database USING The TableAdapter.Insert Method

When you use this TableAdapter DBDirect method to perform data manipulations to a database, the main query must provide enough information in order for the DBD methods to be created correctly. The so-called main query is the default or original query methods such as Fill() and GetData() when you initially open any Adapter using the TableAdapter Configuration Wizard. Enough information means the data table must contain completed definitions. For example, if a TableAdapter is configured to query from a database that does not have a primary key column, it does not generate DBDirect methods.

Figure 6.1 lists three TableAdapter methods.
It can be seen from Figure 6.1 that the TableAdapter.Update() method has two functions: one is to make all changes in the database based on the parameters contained in the Update() method; the other is to update all changes made in the database to the associated properties of the TableAdapter such as the InsertCommand, UpdateCommand and DeleteCommand.
In this chapter, we take care of the inserting data, so only two methods are discussed in this chapter. The third will be discussed in Chapter 7.

# 6.1.2 Insert New Records INTO A Database USING The TableAdapter.Update Method

To use this method to insert data into the database, one needs to perform the following two steps:

+   1) Add new records to the desired DataTable by creating a new DataRow and adding it to the Rows collection.

+   2) After the new rows are added to the DataTable, call the TableAdapter.Update() method. You can control the amount of data to be updated by passing an entire DataSet, a DataTable, or array of DataRows, or a single DataRow.

| DBDirect Method | Description |
|---|---|
| TableAdapter Insert | Adds new records into a database allowing you to pass in individual column values as method parameters. |
| TableAdapter.Update | Updates existing records in a database. The Update method takes original and new column values as method parameters to locate the original record, and the new values are used to update that record. The TableAdapter Update method is also used to recognize changes and sync back to the database by taking a DataSet, DataTable, DataRow, or array of DataRows as method parameters. |
| TableAdapter.Delete | Deletes existing records from the database based on the original column values passed in method parameters. |

Figure 6.1 TableAdapter DBDirect methods.