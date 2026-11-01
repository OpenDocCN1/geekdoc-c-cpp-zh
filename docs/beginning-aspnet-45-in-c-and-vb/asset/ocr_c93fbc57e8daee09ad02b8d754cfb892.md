# Re-Creating the Database

Although every host has its own rules and procedures when it comes to providing access to their SQL Server, they can be grouped in three categories.

> NOTE For detailed information about hosting your site with an external hosting party, check out the tutorials in the hosting section of the official ASP.NET site at www.asp.net/learn/hosting.

First, some hosts don’t give you remote access to their database and require you to submit a .sql file so they can execute it for you. In this case, you don’t have to do anything other than send the file and wait for the host to create your database.

The second category contains the hosts that allow you to execute SQL statements through a web interface. You typically log in to your online control panel and then execute the SQL statements created by the scripting tool, either by uploading the file or by pasting its contents in a text area in a web page. Regardless of the method, you then end up with a database that you can access from your application. How this works exactly is different with each host, so consult the hosting service’s help or support system for more information. Some known issues exist with web-based database management tools from some providers, resulting in errors when you try to run the generated SQL file. Although the file itself is technically valid, the tool may still run into issues with it. If that’s the case, contact your host for help on resolving the issue. If you run into issues, one of the things you may want to try is to save your SQL file in a different format. The default format is Unicode, which not all providers understand. To change the format, choose ANSI Text for the Save As option when exporting your data, as shown in Figure 19-16.

The final category contains hosts that allow you to connect to their SQL Server over the Internet. This enables you to use tools like SQL Server Management Studio to connect to the database at your host right from your desktop and execute the SQL scripts remotely. Refer to the first exercise in the section "Using SQL to Work with Database Data" of Chapter 12 to learn more about executing SQL files against a database using SSMS.

After your database is re-created at your target server, you need to reconfigure your ASP.NET application to use the new database by changing the connection strings in your website. For this to work, you need to modify two connection strings: the PlanetWroxConnectionString1 and the PlanetWroxEntities you created in an earlier chapter. How your connection string must look depends on the database you are using and its configuration. Your hosting company or database administrator typically provides this information. For many examples of proper connection strings, check out www.connectionstrings.com. The following snippet provides a simple example that reconfigures your application to use a database server called DatabaseServer. This example shows a connection string for a SQL Server that requires you to log in with a username and password (in your configuration file, each connection string should be on a single line):

```
<connectionStrings>
    <add name="PlanetWroxConnectionString1" connectionString="Data Source=DatabaseServer;Initial Catalog=PlanetWrox;User Id=YourUserName; Password=YourPassword;" providerName="System.Data.SqlClient"/>
</connectionStrings>
```