# Data Inserting with C#.Net

357

![](bbox=[0.104, 0.083, 0.896, 0.276])

FIGURE 6.47

Another way to confirm this data insertion is to open the Course table from the Server Explorer. Within the opened course table, one can find out our inserted course, CSE-668, can be found at the bottom of the table, as shown in Figure 6.47.

A completed project RTInsertSP that includes the data insertion using the stored procedure method can be found from the Class DB Projects> Chapter 6 RTInsertSP Solution, which is located under the Students folder on the CRC Fpt site (refer to Figure 1.2 in Chapter 1).

# 6.7 CHAPTER SUMMARY

Four popular data insertion methods are discussed and analyzed with three examples for our SQL Server 2019 database in this chapter:

+   1) Using the TableAdapter.Insert() method to insert data.
2) Using the TableAdapter.Update() method to insert new records that have already been added into the DataTable in the DataSet.
3) Using the Command object's ExecuteNonQuery() method.
4) Using the stored procedures.

Method 1 is developed using the Visual Studio.NET design tools and wizards and allows users to directly access the database and the adapters, such as TableAdapter.Insert() and TableAdapter.Update(), to manipulate the data in the database without requiring DataSet or DataTable to reconcile changes in order to update a database. As we mentioned in the beginning of this chapter, inserting data into a table in a DataSet is different from inserting data into a table. If you use the DataSet to store data in your applications, you need to use the TableAdapter.Update() method which can trigger and set all changes (inserts, updates, and deletes) to the database.

One good habit is to use the TableAdapter.Insert() method when your application uses objects to store data (for example, you are using TextBox to store your data), or when you need finer control over new records in the database.

Method 2 allows users to insert new data into a database with two steps. The first record should be added into the data table that is located in a DataSet; the TableAdapter.Update()