# 530 SQL Server Database Programming with C#

connection string and connection object in the Web service class as we did in the previous projects. Another way is to define the connection string in the **Web.config** file. The second way is better since the **Web.config** file provides an attribute `<connectionStrings>` for this purpose and ASP.NET 4.7 recommends to store the data components' connection string in the **Web.config** file.

In this project, we will use the second way to store our connection string. To do that, we open our Web service project by double-clicking on it, move to the end of that file, and enter each of the following code segments into this file (just above the configuration ending tag `<configuration>`).

```
<connectionStrings>
<add name="sql_conn" connectionString="Server=localhost\SQL2019EXPRESS;Integrated Security=SSPI;Database=CSE_DEP;" />
</connectionStrings>
```

or

```
<connectionStrings>
<add name="sql_conn" connectionString="Server=localhost\nSQL2019EXPRESS;
Initial Catalog=CSE_DEP;User ID=SMART;Password=Happy2022;" />
</connectionStrings>
```

The important points should be noted when you create this connection string:

+   1. You need to use either the upper or the lower segment as the connection string, not both we set up our sample database with two accessing modes; **Windows Authentication mode** and **SQL Server Authentication mode**. The upper one is used for the former and the lower is used for the later mode.
2. This connectionStrings attribute attribute must be written in a single line in the **Web.config** file. However, due to the space limitation, we used two lines to represent this attribute. But in your real cases, you must place this attribute in a single line in your **Web.config** file; otherwise, a grammar problem will be encountered.
3. Web services that require a database connection in this project use either a SQL Server Authentication mode with a login ID and password for a user account, or without credentials. We used **Windows Authentication mode** when we created our sample database in Chapter 2, but by modifying mode to the **Server Authentication mode** in Chapter 5. In this project you can use either mode as you like.

To test and this connectionString, we can develop some code and modify the code in the default **HelloWorld** Web in the main service to do that. Close the **Web.config** file and open the main service page **WebServicesSelect.asm** by double-clicking on it from the Solution window, and enter the codes shown in Figure 9.17 into this. All modified code have been highlighted with the bold words, and let's see how this piece of codes works to test our connection string.

A. The namespaces that contains the SQL Data Provider and Web service as well as the system configurations are added into this page using the **using** commands since we need to use those data components in page.

B. The ConnectionStrings property of the ConfigurationManager is used to pick up the connection string defined in the **Web.config** file, which can be used as a default connection configuration. The connection name **sql_conn** that works as an argument for this property must be identical with the name we used for the connection name in the **Web.config** file. When this property is used, it returns a **ConnectionStringSettingsCollection** object