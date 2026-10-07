# Data Upating and Deleting with C#.

these three tables together. The faculty id is a primary key in the Faculty table, a foreign key in both Login and the Course tables. In order to update or delete data from any of those tables, one needs to follow the sequence above. As a case of updating or deleting a record against the database, the following data operation sequence must be performed:

+   1) First, remove or delete record from the child tables, Login and Course tables, respectively.
2) Update or delete record in the parent table, Faculty table.
3) Finally, updated record can be inserted into the child tables as Login and Course tables for the data updating operation. There is no any data action for the data deleting operations for the child tables.

It would be complicated if we update a full record (including the primary key) for any existing record in our sample database. In practice, it is unnecessary to update a primary key for any record since the primary key has the same lifetime as a database. A better popular way to do this updating is to remove undesired records and insert new records with primary keys. Therefore, in this chapter, we will concentrate on updating existing data in our sample database without touching the primary key. For data deleting, we can delete a full record with the primary key and all related records in the child tables will also be deleted since all tables have set in a Cascade Delete mode when we built these tables for our sample database CSE_DEPT in Section 2.9.4 in Chapter 2.

# UPDATE OR DELETE DATA AGAINST DATABASE USING TableADBDIRECT METHODS

Three typical TableAdapter's DBDIRECT methods are listed in Figure 6.1 in Chapter 6. For your convenience, we redraw that in table, which is shown as Figure 7.1.

Both DDIRECT methods, TableAdapter.Update and TableAdapter.Delete(), need the original values as parameters when these methods are executed. The TableAdapter.Update() method needs both the original and the new column values to perform the data updating. Another point to be noted is when the application uses the object to store the data, for instance, in our sample project we use TextBox objects to store our data; this DBDIRECT method to perform the data manipulations against the database.

# UPDATE OR DELETE DATA AGAINST DATABASE USING TableAdapter.Update METHOD

You can use the TableAdapter.Update() method to update or edit records in a database. The Table TableAdapter.Update() provides several operations that perform depending on

| TableAdapter DBDIRECT Method | Description |
|---|---|n| TableAdapter.Insert | Adds new records into a database allowing you to pass in individual column values as method parameters. |
| TableAdapter.Update | Updating existing records in database. The Update method takes original and new column values as method parameters. The original values are used to locate the record, and the new values are used to update that record. The TableAdapter.Update method is used to reconcile changes in a dataset by taking a DataTable, DataTable, DataRow, or array of DataRows as method parameters. |
| TableAdapter.Delete | Deletes existing records from the database based on the original column values as method parameters. |

Figure 7.1 TableAdapter DBDIRECT methods.