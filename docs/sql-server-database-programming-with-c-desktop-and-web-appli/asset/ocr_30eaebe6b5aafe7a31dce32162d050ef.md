# Data Selection Query with Visual#.NET

However, if a SQL Server Authentication Mode is used for this connection, a completed connection string, including the Server, Database, User and Password, is needed, and it looks like:

```
Connection = new SqlConnection("Server=SMART\SQL2019EXPRESS"; + \
"Initial Catalog=CSE_DEPT"; + \
"User ID=UserID"; + \
"Password=MyPassword");
```

where the database name is replaced by the Initial Catalog and the Integrated Security is replaced by Username and Password.

By default, SQL Server 2019 Express used Windows Authentication to authenticate connections when it is installed in your machine. In most popular database applications, a mixed or a SQL Server Authentication Mode is adopted for most database drivers. To match applications, the default Windows Authentication Mode needs to be changed to the SQL Server Authentication Mode. Two ways can be utilized to change that connection mode:

+   1) Select the SQL Server Authentication Mode when installing SQL Server 2019 Express database in your machine.
2) Change the Windows Authentication Mode to the SQL Server Authentication Mode after the SQL Server 2019 Express database has been installed in your machine with the Windows Authentication Mode.

Refer to Appendix C on the CRC ftp site to perform this operation if one wants to use the SQL Authentication Mode to connect to our sample database.
In the sections below we have used the SelectWizard Project, to make things simple, we created and added our DataSet into project using the default Windows Authentication Mode to connect to our sample. If one wants to build a DataSet to connect to the sample database with SQL Server Authentication Mode via design tools and wizards, refer to Appendix D on the CRC ftp site, which provides details to carry out this connection. In the following projects, we will use both authentication methods to connect to our sample database to perform data queries.

In this section, we use an SQL Server 2019 Express database and connect it with our example project using the SQL Server database used in this sample project CSE_DEPT, which was developed in Chapter 2. The advantages of using the Express version of SQL 2019 include, but are not limited to the following:

+   - The SQL Server 2019 Express is fully compatible with SQL Server 2019 database and has the full functionalities of the latter.
- The SQL Server 2019 can be easily downloaded from the Microsoft site free of charge.
- The Microsoft SQL Management Studio 18 is also downloaded and installed on your local computer free of charge. You can use this tool to build your database easily and conveniently.
- The SQL Client can be downloaded and installed on your local computer free of charge. You can install both SQL Server and Client on your local computer to develop professional data-driven applications to connect to your SQL database easily.

# 5.15.2 Create A New C# Project RTOSelect Project

Now we need to create a Visual C# 2022 project RTOSelect to query data from samples in our database. To make things simple, we only need to use some Windows Forms, such as Login Form, Selection Form, Faculty Form and Course Form, to perform related queries. We only need to build these Forms in this new project. One easy way to build Forms is to use some existing Forms, Login.cs, Selection.cs, Faculty.cs, and Course.cs, which can be