
## Figure 24.4: Selecting Data Source

![](img/e073a4882197be4ab61103cbe0bcb394_1181_0.png)

On clicking the Change button, the Change Data Source dialog box appears to allow you to select the data source for your application (Figure 24.5).

- 4. Select a data source from the list shown in the Change Data Source dialog box. In our case, we have selected Microsoft SQL Server as the data source that is shown in Figure 24.5.

## Figure 24.5: Changing the Data Source

![](img/e073a4882197be4ab61103cbe0bcb394_1181_1.png)

- 5. Click the OK button (Figure 24.5). You return to the Add Connection dialog box with different options after clicking the OK button (Figure 24.6).

- 6. Enter or select the server name of your SQL Server in the Server name combo box. In our case, we have entered UMAR-PC (Figure 24.6).

- 7. Select the Use Windows Authentication radio button in the Log on to the server group (Figure 24.6).

- 8. Enter the database name in the Select or enter a database name drop-down list in the Connect to a database group. In our case, we have entered the Northwind database (Figure 24.6).

- 9. Click the Test Connection button. A message box appears with the message Test Connection succeeded, as shown in Figure 24.6:

![](img/e073a4882197be4ab61103cbe0bcb394_1182_0.png)

Figure 24.6: Testing Connection

- 10. Click the OK button of the message box (Figure 24.6).
- 11. Click the OK button of the Add Connection dialog box (Figure 24.6).
- You will notice that the data source is added to your application in Server Explorer, as shown in Figure 24.7:

![](img/e073a4882197be4ab61103cbe0bcb394_1182_1.png)

Figure 24.7: Showing the Added Connection in the Server Explorer

12. Select the data source in the Server Explorer and press F4 to view the properties of the data source in the Properties window, as shown in Figure 24.8:

![](img/e073a4882197be4ab61103cbe0bcb394_1183_0.png)

## Figure 24.8: Property of the Connection String

You can find the full details about the connection string in the properties window. The Name is the name of database that you have attached with your application. The Case Sensitive property implies whether the connection string is case sensitive or not. In this case, the value of Case Sensitive is set to False. The Connection String property specifies the full path of the connection string of the data source. The Owner property specifies the name of the administrator of the system, on which you are currently working. The property window also specifies the Provider for that particular connection string, which in this case is .NET Framework Data Provider for SQL Server. The State specifies if the connection is Open or Close. The Type property specifies the Type of data source you have used, which in this case is Microsoft SQL Server.

The syntax of the connection string depends on the data provider. The syntax error results in a run-time exception. After validating the connection string of the syntax, the data source opens the connection. You can get or set the connection string for an OLE DB data source, such as Microsoft Access, by using the ConnectionString property of the OleDbConnection class. For SQL Server, you can use the ConnectionString property of the SqlConnection class to set the connection string. The ConnectionString property of OracleConnection allows you to get or set a connection string for an ORACLE data source. The basic syntax of the connection string includes a series of keywords separated by semicolons. The equal sign connects each keyword and its value. The value must be enclosed within double quotation marks. The syntax of the connection string for each of the data source is different. You can create a connection string through the wizard, as shown in the chapter. In some cases, you can create a connection string through the code-behind file. For this, you should be aware of the syntax of the connection string for each of the data source. Let’s look at the syntax of a different connection string for each of the data source.

For the Microsoft SQL Server data source, you need to pass the following connection string:

```
Data Source=.;Initial Catalog=Northwind;Integrated Security=True
```

The parameters of the SQL Server connection string are discussed as follows:

- Data Source – Represents the name or the network address of the instance of the SQL Server to which you need to connect.
- Initial Catalog – Represents the name of the database.
- Integrated Security – Accepts two values: True and False. If the value is False then you need to specify the User ID and Password specified in the connection. If the value is True, then the current Windows account credentials are used for authentication. The default value is True.

Another type of data source is the OLEDB data provider. You can access the SQL, Access, and Oracle database with the OLEDB data provider. In this case, we have used the Access database or the MS Jet database. You need to pass the following connection string for MS Jet database:

```
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=D:\C#_BB\Northwind Database Files\Northwind.mdb"
```

The parameters of the MS Jet connection string are discussed as follows:

- Provider – Represents the type of database that you want to access
- Source – Represents the path of the database file stored on your machine

For the Oracle data source, you need to pass the following connection string:

```
"Data Source=Oracle81;Integrated Security=yes"
```

The parameters of the Oracle connection string are discussed as follows:

- Data Source – Represents the name or network address of the instance of Oracle to which you need to connect.
- Integrated Security – Represents whether the connection is secure or not. It takes two values: Yes and No. The default value is Yes.

For the ODBC data source, you need to pass the following connection string:

```
Dsn=myDSN;UID=;Pwd=;
```

In the ODBC connection string, Dsn is the only parameter passed which stores the information about your data source.

## Creating a Connection to a Database

You need a connection to the database with which you want to work. In Visual C#, you can create a connection to the database in two ways. You can either create a connection to the database through the Server Explorer or code-behind file. As you have learned in the In Depth section of this chapter, ADO.NET provides access to data sources, such as Microsoft SQL Server, OLEDB, and XML. However, you need to have different connections for the different types of data sources. You learn about connecting to all the three types of databases available in ADO.NET in both the ways in the following section.

We are going to display the data from the Customers table in the Northwind sample database. Therefore, we need to connect to the Northwind sample database.

## SQL Server Database

In .NET 4.0, you can connect to the SQL Server database in two ways, through the wizard or code-behind file. Let’s create a Windows application named SQLServerDatabase (available in the CD-ROM) in which you can retrieve the data from SQL Server in both ways. Perform the following steps to retrieve the data from SQL Server:

- 1. Add a Button and two DataGridView controls to Form1 from the Toolbox, as shown in Figure 24.9:

![](img/e073a4882197be4ab61103cbe0bcb394_1184_0.png)

Figure 24.9: Adding Controls on the Form

2. Change the Text property of the Button control to Generate Data in the Properties window (Figure 24.9).

In the first grid, we generate data through wizard and in the second, we generate data through code on the click of the button. Let's first generate data in the dataGridView1 control through wizard by performing the following steps:

- 1. Select the dataGridView1 control and click its Smart Tag.
- 2. Select the Add Project Data Source option from the Choose Data Source drop-down list in the Smart Tag of the dataGridView1 control, as shown in Figure 24.10:

![](img/e073a4882197be4ab61103cbe0bcb394_1185_0.png)

This opens the Data Source Configuration Wizard (Figure 24.11).

- 3. Select Database as the data source type and click the Next button, as shown in Figure 24.11:

![](img/e073a4882197be4ab61103cbe0bcb394_1185_1.png)
