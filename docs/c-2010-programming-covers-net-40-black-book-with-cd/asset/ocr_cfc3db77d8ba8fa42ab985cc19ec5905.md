The parameters of the MS Jet connection string are discussed as follows:

+   - Provider – Represents the type of database that you want to access
+   - Source – Represents the path of the database file stored on your machine

For the Oracle data source, you need to pass the following connection string:

```
"Data Source=Oracle81;Integrated Security=yes"
```

The parameters of the Oracle connection string are discussed as follows:

+   - Data Source – Represents the name or network address of the instance of Oracle to which you need to connect.
+   - Integrated Security – Represents whether the connection is secure or not. It takes two values: Yes and No. The default value is Yes.

For the ODBC data source, you need to pass the following connection string:

```
Dsn=myDSN;UID=;Pwd=;
```

In the ODBC connection string, Dsn is the only parameter passed which stores the information about your data source.

# Creating a Connection to a Database

You need a connection to the database with which you want to work. In Visual C#, you can create a connection to the database in two ways. You can either create a connection to the database through the Server Explorer or code-behind file. As you have learned in the In Depth section of this chapter, ADO.NET provides access to data sources, such as Microsoft SQL Server, OLEDB, and XML. However, you need to have different connections for the different types of data sources. You learn about connecting to all the three types of databases available in ADO.NET in both the ways in the following section.

We are going to display the data from the Customers table in the Northwind sample database. Therefore, we need to connect to the Northwind sample database.

# SQL Server Database

In .NET 4.0, you can connect to the SQL Server database in two ways, through the wizard or code-behind file. Let’s create a Windows application named SQLServerDatabase (available in the CD-ROM) in which you can retrieve the data from SQL Server in both ways. Perform the following steps to retrieve the data from SQL Server:

+   1. Add a Button and two DataGridView controls to Form1 from the Toolbox, as shown in Figure 24.9:

![](bbox=[0.215, 0.62, 0.77, 0.915])

Figure 24.9: Adding Controls on the Form