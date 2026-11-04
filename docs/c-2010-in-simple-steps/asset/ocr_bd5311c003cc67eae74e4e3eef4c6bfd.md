```
SqlConnection con;
con = new SqlConnection("Data Source=TEMP-PC\\SQLEXPRESS;Initial Catalog= D:\\SQL SAMPLE DATABASE\\NORTHWND.MDF;Integrated Security=True");
con.Open();
SqlCommand command =new SqlCommand ("delete from Employees where EmployeeID=6",con);
result=command.ExecuteNonQuery ();
```

In Listing 8.1, an integer variable, result is declared to store the result of the command executed on the data from a data source. An object of the SqlConnection class, con is also created, which takes a connection string as its argument. The connection string, "Data Source=TEMP-PC\\SQLEXPRESS;Initial Catalog= D:\\SQL SAMPLE DATABASE\\NORTHWND.MDF;Integrated Security=True", opens the NORTHWND database on the default SQL Server instance running on the local computer. The connection to the NORTHWND database is established by using the con.Open() command. After establishing a connection with the data source, that is, the NORTHWND database, you need to communicate with it to execute some commands and return the result. For this, the SqlCommand class provides a few methods. In Listing 8.1, the SqlCommand class object, command is instantiated and accepts two parameters, namely the query to be executed in string format and the object of the SqlConnection class, con. The query specifies to delete the details of an employee whose ID is 6 from the Employees table. The result variable returns the result of the ExecuteNonQuery() method.

Let's now learn to add and configure a data adapter in the next section.

# Adding and Configuring a Data Adapter

A DataAdapter object enables you to access data from a database by serving as a bridge between a DataSet object and a data source. A DataAdapter object establishes a connection to and retrieves data from a data source by using a Connection object and a Command object, respectively. All the commands required to manipulate, update, and modify the data in a data source are available in a DataAdapter object.

Let's now learn how to access data in a DataAdapter from a database in a Windows Forms application. In our case, we use the DatabaseOperationsExample application created in the Using the Add Connection Dialog Box section of this chapter.

Perform the following steps to access data in a DataAdapter object from an SQL Server database:

+   1. Set the Text property of Form1 to Basic Database Operations in the DatabaseOperationsExample application.
+   2. Drag an SqlDataAdapter control from the Data tab of Toolbox and drop it into the Form1 form, if the SqlDataAdapter control is available in Toolbox.

> Note
> If the SqlDataAdapter control is not present in the Toolbox, perform steps 3 to 5 to add the SqlDataAdapter control to the Data tab of Toolbox; otherwise directly move to Step 6.

3. Right-click the Data tab in Toolbox and select the Choose Items option from the context menu that appears, as shown in Fig.C8-8:

![](bbox=[0.28, 0.6, 0.68, 0.85])

Fig.C7-8.8

The Choose Toolbox Items dialog box appears (Fig.C8-8.9).