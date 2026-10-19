Step 1-7: Select *Microsoft SQL Server Database File* for Data Source. The dropdown list for Data Provider should show .Net Framework Data Provider for Microsoft SQL Server.

Click *Continue*. The following Add Connection window appears:

![](bbox=[0.15, 0.14, 0.5, 0.345])

Click *Browse*, and select HR.mdf from the local directory. Click *Open*.

Click *OK*. If the database is not compatible with the current instance of SQL Server, you will be asked whether you want to upgrade the database. Select *Yes*.

# Step 1-8: Click *Next*. You may be asked whether you want to copy the file to your project. Make sure you select *No*.

If you answer *Yes*, Visual Studio will copy the database file to the project directory, and by default, changes made to the database at runtime will be lost the next time the project is run.

Click *Next*. You will be asked whether you want to save the connection string.

Accept the default (*Yes*), and Click *Next*. You will be asked to select the database objects, as shown in Figure 12-5.

# Figure 12-5: Selecting database objects

![](bbox=[0.08, 0.65, 0.4, 0.92])