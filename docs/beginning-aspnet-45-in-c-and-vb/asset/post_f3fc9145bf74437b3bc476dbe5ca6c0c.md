
![](img/eadab2ccd79b253c01a3fdff2321202d_838_0.png)

## Configuring SQL Server 2012

So far, the exercises in the book assume that you are using Microsoft SQL Express 2012 LocalDB Edition 11.0 as the database for the Planet Wrox project. SQL Express LocalDB Edition 11.0 is great for development because it's free, lightweight, and easy to use. However, it's not designed to be used in a production environment and is limited in terms of processor and memory usage and database size. In cases where the LocalDB edition is not enough, you need to look at its bigger brothers: SQL Server 2012 Express edition or the commercial versions of SQL Server 2012, such as the Standard or Enterprise Editions. In this appendix you learn more about SQL Server 2012, its security model, how to enable your SQL Server 2012 database and ASP.NET 4.5 website to work together, and how to use SQL Server Management Studio Express, a free tool from Microsoft that lets you manage your database.

Although this appendix doesn't discuss earlier versions of SQL Server, you'll find that most of the concepts apply to these older versions as well. In fact, you can also use SQL Server 2012 Management Studio Express to manage older SQL Server 2005 and 2008 databases. This appendix uses SQL Server Express edition because it's a free download, but the same principles apply to the commercial versions of SQL Server.

## CONFIGURING SQL SERVER 2012

Before you can configure your database, you need to be aware of the various security concepts that are inevitably associated with databases and web applications. In Chapter 19 you learned how the account used by the web server plays a big role when configuring security settings for the filesystem, and that's no different when connecting to SQL Server. In the following section, you get a quick primer on the different ways to connect to SQL Server. In the section that follows you see how to attach your .mdf database files to SQL Server, followed by a discussion of configuring your application and database so they can talk to each other.

## Terminology and Concepts

When you connect to a SQL Server database, SQL Server needs to know who you are, so it can enforce the correct access policies on objects like tables in the database. SQL Server supports two different authentication mechanisms: SQL Server Authentication and Windows Authentication (often called Integrated Security). Both come with a few advantages of their own and require you to write different connection strings to connect to SQL Server. In the following section you see the two most common connection strings, but you're advised to visit www.connectionstrings.com for an extensive list of possible connection strings.

## SQL Server Authentication

With SQL Server Authentication, SQL Server takes care of user management. You manage the users for your SQL Server database with Microsoft SQL Server Management Studio, either the Express edition (which you see how to use a little later in this appendix) or the full versions that ship with the commercial versions of SQL Server. SQL Server uses a login that handles authentication. You define this login at the server level by providing a login name and a password. A login can then be mapped to a database user to grant access to a specific database.

To connect your web application to a SQL Server installation that requires you to use SQL Server Authentication, you need to pass a username and password in the connection string of your application. A typical connection string looks like this:

```text
Data Source=ServerName;Initial Catalog=DatabaseName;
User Id=UserName;Password=Password;
```

In this case the Data Source points to an unnamed instance of SQL Server: the SQL Server is addressed by its machine name alone. It's also possible to install SQL Server as a named instance. With a named instance, the name of the server is followed by a backslash (`\`) and the name of a particular SQL Server instance. For example:

```text
Data Source=ServerName\InstanceName;Initial Catalog=DatabaseName;
User Id=UserName;Password=Password;
```

SQL Server Authentication is often used when you need to connect to a remote SQL Server over the Internet because Windows Authentication, discussed next, is not supported in that scenario.

## Windows Authentication

With Windows Authentication, the Windows OS takes care of user management. All interaction with the database is done in the context of the calling user so the database knows who's accessing the system. You still need to map a Windows login to a SQL Server database user so SQL Server can determine whether the account has sufficient permissions. I show you how to do this later.

A typical connection string using Windows Authentication looks like this:

```text
Data Source=ServerName;Initial Catalog=DatabaseName;Trusted_Connection=True
```

Instead of specifying a username and password, you add `Trusted_Connection=True` to the connection string to indicate you want to connect to the server with the user context of the calling user. You may also come across the setting `Integrated Security=True`, which has the same effect.

Because both authentication methods eventually do the same thing (they enable you to connect to SQL Server), you may wonder which one of the two you should use.

## Choosing between Windows and Server Authentication

In general, it’s recommended to use Windows Authentication when possible. The fact that you don’t need to use a password in the connection string means your application will be a bit safer. You don’t need to send the password over the wire, and it’s also not stored in a configuration file for your application.

However, SQL Server Authentication is a bit easier to set up. Because you specify the username and password explicitly, you don’t need to know the final user account that your application runs under.

Later in this appendix you see how to use both authentication mechanisms to connect to your database. However, you need to look at something else first: the tools used to manage SQL Server.

## Using SQL Server Management Studio

You use SQL Server Management Studio to manage your SQL Server and databases. It enables you to attach and detach databases to your SQL Server; create new database objects like tables in existing databases; select, create, edit, and delete data; and much more.

So far, you’ve been using the LocalDB version of SQL Server, the developer-friendly version of SQL Server. In addition to LocalDB, Microsoft has another free version of SQL Server called SQL Server Express. The following sections of this appendix show you how to work with this free SQL Server Express edition, because it’s very similar in use compared to its commercial and production-ready databases. If you only installed LocalDB, you need to download and install SQL Server Express along with the free SQL Server Management Studio Express. The section “Installing SQL Server 2012 Express” in Chapter 12 explains how to acquire SQL Server 2012 Express Edition as well as its Management Studio component.

If you are already using a commercial version of SQL Server, you already have access to the full version of SQL Server Management Studio, because it comes bundled with the database engine.

If you are having trouble connecting to a remote SQL Server (for example, an instance of SQL Server that is not on the same physical server as the one on which you’re running Management Studio), you may need to enable remote connections for that SQL Server first. This is discussed next.

## Enabling Remote Connections in SQL Server

When working with SQL Server, you may receive an error stating that the server was not found, not accessible, or that remote connections may not be configured properly.

Although you may get this error when the database server is down, you also get this error when SQL Server is not configured for remote connections. In a default installation, SQL Server allows only local applications to connect and blocks remote connections automatically. To resolve this, and grant remote systems access to the server as well, follow these steps:

- 1. Open the SQL Server Configuration Manager from the Start menu or Start screen. Depending on the version of SQL Server you’re using, this item may be located under the Microsoft SQL Server 2012/Configuration Tools submenu.
