
## NEW CONNECTION

If the database is not already attached, the option to add a **New Connection** is selected, as shown in Figure 14-7. Connections that are already established are available from the drop-down list shown to the left of the **New Connection** button.

![](img/36e48639a06772bcb0fa1ea2525b33a3_962_0.png)

FIGURE 14-7 Add a New Connection

You follow these steps whether you are connecting to a Microsoft SQL Server, Oracle, or Microsoft Access database. To establish a new connection, select **New Connection**. A dialog box similar to the one shown in Figure 14-7 is displayed, enabling you to change the **Data Source** provider. Next you are able to enter details regarding the database to which you want to connect as shown in Figure 14-8.

![](img/36e48639a06772bcb0fa1ea2525b33a3_963_0.png)

**FIGURE 14-8** Select the data source

To see the list of available databases, click the **Refresh** button after the server name is entered.

## SQL SERVER

If you have Visual Studio 2005 or later, you have SQL Server. It is installed as part of the Visual Studio install and can be used within the Visual Studio IDE to design and manipulate databases. Included with Visual Studio 2012, is a lightweight version of SQL Server, SQL Server Express LocalDB, a streamlined, simplified version of SQL Express that speeds up data development. LocalDB has all the programmability features of a SQL Server database engine and replaces SQL Server Express as the default database engine for development. Visual Studio 2010 and earlier versions use SQL Server Express. If you are connecting to a SQL Server Express database, you would type `(LocalDB)\v11.0` or `.\SQLEXPRESS` in the Server name box shown in Figure 14-8. This assumes the default name was retained during Visual Studio or SQL Server installation. Selecting the **Refresh** button populates the interface with available connections.

## CREATING SQL SERVER DATABASES

To create a new SQL Server database from within Visual Studio, display the **Server Explorer** window (from the VIEW menu). The **Server Explorer** is called **Database Explorer** in Visual Studio Express. Right-clicking the **Data Connections** icon displays a shortcut menu option named **Create New SQL Server Database**, as shown in Figure 14-9.

![](img/36e48639a06772bcb0fa1ea2525b33a3_964_0.png)

**FIGURE 14-9** Server Explorer window

After selecting the option shown in Figure 14–9, you are again asked to enter the server name (`(LocalDB)\v11.0` for Visual Studio 2012 or `.\SQLEXPRESS` for earlier versions) and the name of your new database. After the database is created, you add tables by opening or expanding the tree under the database. Do this by clicking the arrow to the left of the database name. This expands or reveals a number of database features, including **Tables, Views, and Stored Procedures**. To create a new table, right-click the **Tables** node in the **Server Explorer** window and select **Add New Table** from the shortcut menu. You will enter field names and data types next. There are int, money, and float data types. For string-type entries, the SQL varchar(50) data type works well. The SQL bit data type works well for Boolean data types. With Visual Studio 2012 you also have a new feature called **SQL Server Object Explorer** available from the **VIEW** menu, which is similar to the **Server Explorer** window except it only targets SQL Server databases.

Significant security changes were implemented, beginning with SQL Server 2005, to make it more secure. These changes may be problematic for your development. To create or attach to a SQL Server database during development, you need administrative permissions on the local machine. But, it is not enough to have membership in the Windows Administrator group. SQL Server accounts are no longer automatically granted access to SQL Server because of their membership in the Windows Administrator group. Users must be assigned special security roles, such as dbcreator or sysadmin, in order to create database tables.

Creating a SQL Server database using Visual Studio and the **SQL Server Object Explorer** window or the **Server Explorer** window is a fairly simple process. You are encouraged to explore this on your own and use the online MSDN documentation if you need additional help. There are also several Internet resources including tutorials listed at the end of this chapter focusing on creating SQL Server Express LocalDB databases.

## ADDING A CONNECTION

As shown in Figure 14–9, another option when you right-click on the **Data Connections** node is the **Add Connection** option from the shortcut menu in the **Server Explorer** window. If you select this option, a dialog box is displayed that allows you to specify the data source and database filename and test the connection. You can also add the connection using the **Add New Data Source** option from the **PROJECT** menu. Selecting this option launches the **Data Source Configuration Wizard** shown previously in Figures 14–6 and 14–7.

Because of potential permission constraints associated with SQL Server, Microsoft Access data source is used for the remaining examples in this chapter. To connect to an Access database, click the **Change...** button beside the **Data Source**, as shown in Figure 14–8. This opens another dialog box, where you would choose **Microsoft Access Database File** as the Data Source. This option lets you use the .NET Framework Data Provider for OLE DB. If you select the checkbox in the extreme left corner, Always use this selection, Access will become the default data source for future connections.

You select and enter the name of the database file next using the Browse button. When connecting to an Access database, you are asked to enter a username and password for the database. The default (Admin) is automatically added as the User name. You are encouraged to keep this default setting and to leave the Password text box blank.

## TESTING THE CONNECTION

After you locate the appropriate database, the Test Connection button can be used to make sure you are able to connect to the data source. This is illustrated in Figure 14-10. You should perform this test before continuing with the configuration to make sure you are able to connect to the data source.

![](img/36e48639a06772bcb0fa1ea2525b33a3_966_0.png)

FIGURE 14-10 Locate and test the connection

After testing your connection as shown in Figure 14–10, if you are using the **Data Source Configuration Wizard**, you might get a message similar to the one shown in Figure 14–11—especially when you are creating applications that connect to a Microsoft Access database.

![](img/36e48639a06772bcb0fa1ea2525b33a3_967_0.png)

**FIGURE 14–11** Copy database file to your project

## LOCAL COPY OF YOUR DATABASE

The first time you establish a connection to the database for your application, the message shown in Figure 14–11 is displayed. The configuration tool offers to make a copy of the database and place it in your project folder. The file is placed at the same level as the project folder—at the same location where the source code files for the Windows form are stored. Selecting **Yes** copies the database into your project and modifies the connection so that it now points to the database in your project. In addition, selecting **Yes** causes the file to be copied to the project’s output directory (bin\Debug folder) each time you run the application. So you end up with two copies of the database with your application, when you select **Yes**. The copy of the database in the bin\Debug directory reflects any changes made from your application. The other copy, stored at the same directory level as your project folder, is the original unchanged database.

If you choose not to make a copy, and select **No** when prompted as shown in Figure 14–11, then a connection is established, and the database file is left in its original location. No additional copies are made. Either way, whether you select **Yes** or **No**, the next time you create an application and **Add a Data Source**, the connection to the
