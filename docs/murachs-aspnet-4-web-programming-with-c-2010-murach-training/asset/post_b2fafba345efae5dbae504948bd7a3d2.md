
![](img/c024ccf88e28c30c07dd410d4342288f_806_0.png)

## The SQL Server Configuration Manager

## How to install SQL Server 2008 Express
- Run the setup program. When the SQL Server Installation Center dialog box is displayed, select the Installation option, select the “New installation or add feature to an existing installation” option to start the SQL Server 2008 R2 Setup Wizard, and respond to the resulting dialog boxes.
- At the Feature Selection step, select all available features.
- At the Instance Configuration step, create a named instance with a name of SQLEXPRESS.
- At the Server Configuration step, select NT AUTHORITY\SYSTEM as the account name for the SQL Server Database Engine service to run SQL Server on your computer.
- At the Database Engine Configuration step, you can accept the default setting of Windows Authentication Mode. You can also click the Add Current User button to add the current user as a SQL Server administrator.

## How to use SQL Server Express
- After you install SQL Server Express, it will start automatically each time you start your PC. To start or stop this service or change its start mode, start the SQL Server Configuration Manager (Start→All Programs→Microsoft SQL Server 2008 R2→Configuration Tools→SQL Server Configuration Manager), select the server in the right pane, and use the buttons in the toolbar.
- The setup program creates a copy of SQL Server with a name that consists of your computer name followed by \SqlExpress. You can use this name to define connections to the databases that you use with this server.

## Description
- If you’re using Visual Studio 2010, you can install SQL Server 2008 Express at the same time that you install Visual Studio.
- If you’re using Visual Web Developer 2008 Express Edition, you can download the setup file for SQL Server 2008 Express Edition Release 2 from Microsoft’s web site for free. Then, you can run the setup file to install SQL Server Express.

## How to create the Halloween database

If you want to use the database that’s available with the download for this book, you can do that without much trouble. First, you’ll need to download and install the book files as described in figure A-1. Then, you can run the batch file named create_database.bat that’s in the C:\Murach\aspnet4_cs\database directory. This batch file runs a SQL Server script named create_database.sql that creates the Halloween database and attaches it to the SQL Server Express database server that’s running on your computer.

Note, however, that if the database server on your system has a name other than the computer name appended with SQLEXPRESS, the batch file we provide won’t work. But you can easily change it so it will. To do that, just open the file in a text editor such as NotePad. When you do, you’ll see a single command with this server specification:

```
sqlcmd -S localhost\SQLEXPRESS -E /i create_database.sql
```

Then, you can just change this specification to the name of your server. You’ll also need to make this change to the other batch files that we provide.

Figure A-6 shows the beginning of the create_database.sql file. Although you don’t need to understand all the details of this script, you may want to have a general idea of how it works.

To start, this script checks if the Halloween database already exists. If it does, the database is deleted. In either case, the database is created. This makes it possible to use this script to create the database initially and to restore the database to its original state if you ever need to do that.

After it creates the database, this script creates each table in the database and then inserts the required rows into that table. In this figure, for example, you can see the Create Table statement that creates the States table. This statement is followed by four Insert statements that insert the first four rows into the table. Similar statements are used for each of the other tables. Finally, it creates the foreign key constraints that define the relationships between the tables.

If you’ll be running the database applications under IIS, you’ll also need to grant ASP.NET access to the database. To do that under Windows XP, you can run the grant_access_windows_xp.bat file in the database directory. But first, you must modify the grant_access_windows_xp.sql file that this batch file runs so it uses the name of your computer. To do that, open the file in a text editor, and replace each occurrence of [machineName] with the name of your computer. Then, save and close this file, and run the grant_access_windows_xp.bat file to grant ASP.NET access to the Halloween database.

You use a similar technique to grant ASP.NET access to the database under Windows 7 and Windows Vista. Specifically, you run the grant_access_windows_7_vista.bat file, which runs the grant_access_windows_7_vista.sql file. If you open this file, you’ll see that it actually grants access to the ASP.NET 4 application pool. This is the application pool that your ASP.NET 4 applications will run in by default if you run them under IIS. You’ll learn more about application pools in appendix B.

## The beginning of the script for creating the Halloween database

```
IF DB_ID('Halloween') IS NOT NULL
DROP DATABASE Halloween

CREATE DATABASE Halloween
GO

USE [Halloween]
GO
/****** Object: Table [dbo].[States] Script Date: 01/11/2011 17:06:16
******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[States](
    [StateCode] [char](2) NOT NULL,
    [StateName] [varchar](20) NOT NULL,
CONSTRAINT [PK_States] PRIMARY KEY CLUSTERED
(
    [StateCode] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NO RECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]
GO
SET ANSI_PADDING OFF
GO
INSERT [dbo].[States] ([StateCode], [StateName]) VALUES (N'AK', N'Alaska')
INSERT [dbo].[States] ([StateCode], [StateName]) VALUES (N'AL', N'Alabama')
INSERT [dbo].[States] ([StateCode], [StateName]) VALUES (N'AR', N'Arkansas')
INSERT [dbo].[States] ([StateCode], [StateName]) VALUES (N'AZ', N'Arizona')
.
```

## Description
- To create the Halloween database, you can use Windows Explorer to navigate to the C:\Murach\aspnet4_cs\database folder and double-click the create_database.bat file. This runs the create_database.sql file that creates the database objects and inserts the rows into each table.
- The create_database.sql file starts by deleting the Halloween database if it already exists. That way, you can use it to recreate the database and restore the original data if you ever need to do that.
- When you create the Halloween database, two files named Halloween.mdf and Halloween_log.ldf are created and stored in the default data directory for your instance of SQL Server. For SQL Server 2008, for example, that directory is C:\Program files\Microsoft SQL Server\MSSQL10.SQLEXPRESS\MSSQL\DATA.
- To grant ASP.NET access to the database under Windows XP, you modify the grant_access_windows_xp.sql file so it uses your computer name and then run the grant_access_windows_xp.bat file. To do that under Windows 7 or Windows Vista, you just run the grant_access_windows_7_vista.bat file.

## How to use the downloaded web applications

You can use two techniques to run the downloaded web applications for this book. First, you can open the applications in Visual Studio and then run them using the built-in development server. Second, you can run them under a local IIS server. Figure A-7 describes both of these techniques.

Before you can run an application under a local IIS server, you must create a virtual directory for the application within IIS. A virtual directory is a directory that contains a pointer to the directory that actually contains the files for a web site. To create a virtual directory, you can use the procedure shown in this figure. But first, if you’re using Windows 7, you should set the application pool that IIS will use when you create a virtual directory for an existing application from Visual Studio. To do that, you use the IIS Management Console as shown in figure B-4 of appendix B.

Once you create a virtual directory for a web application, you can also run the application from outside of Visual Studio. To do that, open a browser window and specify //localhost/ followed by the virtual directory name and the starting page. For example, if the virtual directory name is Ch03Cart and the starting page is Order.aspx, you can run the application by entering //localhost/Ch03Cart/Order.aspx in the browser’s address bar.
