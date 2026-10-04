
# CHAPTER 12 INTRODUCING DATABASES

> NOTE Installing SQL Server and SSMS if you get stuck, be sure you visit this book's forum at http://p2p.wrox.com to find a helping hand.

# Installing SQL Server 2012 Express

You can download SQL Server Management Studio Express from the following page at the Microsoft site: http://tinyurl.com/SqlExpress2012. If this link no longer works, you can go to www.microsoft.com/express/database/ instead and click the Download button. Alternatively, you can go to the main downloads page at www.microsoft.com/downloads and search for "SQL Server 2012 Management Studio."

In all cases, make sure you install the 2012 version of Management Studio, and not an older or newer version if one has been released by the time of writing. SQL Server 2014 was in beta and the final release will work well with VWD 2013, but the remainder of this book assumes you are using Server 2012. Also, if you don't have SQL Express (the database server) installed, download the package that contains both the Express database engine and the Management Studio tools (it should have a name as Express with Tools or something similar, advertised as SQLEXPRW). You don't need it in the exercises in the next three chapters, but it's used in Chapter 19, which shows how to deploy your website, and in Appendix B, which shows you how to configure other versions of SQL Server. It's quite a large download (around 700MB if you choose Express with Tools) but well worth the time downloading.

After you have downloaded the Management Studio setup file (with the Express database engine included), follow the on-screen instructions. When asked for the Installation Type, choose a New SQL Server stand-alone installation. This option enables you to choose Management Tools as a component to install in Setup. If you're installing the Database Engine Services, accept sqlExpress as the name for the instance. If name is already taken, you already have SQL Server Express installed locally. If this version is SQL Server 2012 (use the Programs and Features of the control panel in Windows to find it), skip installing the Database Engine Services components. If you have a different version installed, you can still install SQL Server 2012 side by side. In that case, choose a name as Sql2012Express for the named instance. From on then, use this name which refers back to SQLExpress as the named instance.

Now that SQL Server Management Studio is installed, it's time to look at how to manage data in SQL Server database. SQL Server supports a query language called SQL that lets you do that.

# USING SQL WITH WORK WITH DATABASE

To get data in and out of a database, you need to use Structured Query Language (SQL). This is the de facto language for querying relational databases that almost all relational systems understand. A number of clear standards exist, with the most popular being the ANSI 92 SQL standard. Besides the grammar that this standard supports, many database vendors have added their extensions to the language, giving it a lot more flexibility and power on their own system, at the cost of decreased interoperability with other systems.

Microsoft SQL Server 2012 is no exception, and supports most of the grammar that has defined in its ANSI 92 SQL standard. On top of this standard, Microsoft has added some proprietary extensions. Collectively, the two are referred to as T-SQL, or Transact SQL. I'll stick to the term SQL for the remainder of this book.

In the following sections, you will see how to use SQL Server 2012 to retrieve and manipulate data in your database. However, before you write your first SQL statement, you need to know how to connect to your database first. The following exercises show you how to create a sample database from a SQL script file that comes with the downloadable code for this book.

# TRY OUT Creating the SQL Server Sample Database

In this exercise you learn how to create and work with a database using Visual Studio. To give you something to work with, the code download for this chapter contains a SQL script that creates two tables and a few sample rows in your database. You can use these rows to test the SQL queries that are shown throughout this chapter. This database is used only for this chapter, and as such, you don't have to create it to follow along with the Planet Wrox website. However, by creating it the following instructions will give you a nice test database to set out SQL queries.

- 1. Start by creating a folder called Databases in the root. This serves as a nice central location for your databases, which makes it easier to manage. If you decide to use a different location, make sure the folder is not located in your Documents folder or you'll run into permissions problems later. It's recommended to use c:\databases for the walk-throughs in this book.
- 2. Start SQL Server Management Studio from the Windows Start menu or Start screen.
- 3. Log in to the SQL Server LocalDB instance by entering (LocalDB)\v11.0 in the Server Name field as figure 12-3, and click Connect.
- 4. After you log in to the database, you should see the Object Explorer (shown in Figure 12-4) on the left. If you don't see it, check View -> Object Explorer from the main menu or press F8.

![](img/9e033e3b9560597824f8b22941d6d8bb_448_0.png)

Figure 12-3

![](img/9e033e3b9560597824f8b22941d6d8bb_448_1.png)

Figure 12-4

- 5. Right-click the Databases node (visible in Figure 12-4) and choose New Database. Type PlanetWroxTemp as the name. Don't use PlanetWrox as the name, because you'll be using that for later exercises in the book. In the Database Files section of the screen, type:\Databases in the Path column for both rows. You may need to scroll to the right to see the Path column. Your dialog box should end up as in Figure 12-5.

![](img/9e033e3b9560597824f8b22941d6d8bb_449_0.png)

FIGURE 12-5

Click OK to create the database.

- 6. Press Ctrl+O to bring up a dialog box that lets you select a file. Browse to the folder C:\ASPNET\Resources\Chapter 12. If you don't have this, refer to the Introduction of this book to learn how to acquire the code that comes with this book. Select the Create PlanetWrox Database.sql file.

- 7. On the SQL Editor toolbar (shown in Figure 12-6) select the PlanetWroxTemp database from the drop-down list.

# Using SQL to Work with Database Data

![](img/9e033e3b9560597824f8b22941d6d8bb_450_0.png)

This makes the PlanetWorcT database active, any queries you execute in the query editor will target that database.

- 8. Click the Execute on the SQL Editor toolbar or F5. This executes the query and creates two tables along with some sample rows. You can take a look at the SQL statements if you want; the correct of inserting the sample rows is explained later in this chapter.

- 9. On the Object Explorer, click the Refresh on the toolbar and then expand Databases, then your database, and then the Tables node. You should see the Genre and Review tables appear as shown in Figure 12-7.

![](img/9e033e3b9560597824f8b22941d6d8bb_450_1.png)

FIGURE 12-7

# How It Works

In this exercise, you connected to an instance of SQL Server called (LocalDB)\v1.0 which is a lightweight version of SQL Server designed for development. In Appendix B see how to connect to other versions of SQL Server for production scenarios. You created a new database-based PlanetWorcT and stored it in the folder C:\databases. The SQL code you executed against this database contains two tables called Genre and Review. The SQL code to create these tables is not so important now; later in this chapter you learn how to create your own tables using SSMS. The file contains SQL INSERT statements to add data to these tables.

When you have a connection to your database in SSMS, you can work with the objects it contains. In the next section you see how you can access and change the data in the tables in your database.
