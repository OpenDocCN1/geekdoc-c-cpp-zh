Figure 14-3 illustrates the application running. The image in the background of Figure 14-3 shows what the form looks like before the Load Data button is clicked. Its event-handler method populates the `DataGrid` object from the `member.acdb` database by first calling the `Fill( )` method of the `OleDbDataAdapter` class.Notice that two arguments to the `Fill( )` method are the `DataSet` object and the database table.These are the same two arguments used to call the `DataGrid` object's `SetDataBinding( )` method to set its `DataSource` and the `DataMember` properties.

![](bbox=[0.173, 0.247, 0.635, 0.563])

Figure 14-3 Output from DataSetExample after the database is loaded

One of the powerful features of the `DataGrid` object is that it enables you to delete or insert new records (rows) into the data grid. You can also change the values of individual fields (columns) in the data grid. However, the changes are to the local copy of the database. To update the live database, those changes must be posted back to the `DataMember` database table.This is done in Example 14-9 when the Update Data button is clicked.

This `btnUpdate_Click( )` event-handler method included a call to the `Update( )` method of the `OleDbDataAdapter` class.The live database connection is reopened, and the current contents of the dataset (bound to the data grid) are written to the database table specified by the `DataMember` property listed as the second argument.

As shown in Figure 14-4, several changes were made to the local database to illustrate that records could be inserted (Charlene Boswick), or deleted (Gary Jones and Colleen Bennett), and values in fields could be changed (Ralph Abbott changed to Roger Adams).The back image in Figure 14-4 shows the updated database table.The image in the foreground in Figure 14-4 shows the changed values in the `DataGrid` object.