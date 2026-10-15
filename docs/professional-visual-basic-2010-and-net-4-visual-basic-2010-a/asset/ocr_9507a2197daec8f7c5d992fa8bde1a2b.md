# LINQ TO SQL AND VISUAL BASIC

LINQ to SQL in particular is a means to have a strongly typed interface against a SQL Server database. You will find that the approach that LINQ to SQL provides is by far the easiest approach there is at present for querying SQL Server. It’s not simply about querying single tables within the database; for instance, if you call the authors table of the Microsoft sample pubs database and want to pull a title for each author from the same database, then LINQ will use the relations of the tables and make the query on your behalf. LINQ will query the database and load up the data for you to work with from your code (again, strongly typed).

Keep in mind that LINQ to SQL is not only about querying data; you can also perform the INSERT, UPDATE, and DELETE statements that you need to perform.

In addition, you can interact with the entire process and customize the operations performed to add your own business logic to any of the CRUD operations (CREATE/READ/UPDATE/DELETE).

Visual Studio is highly integrated with LINQ to SQL in that it offers an extensive user interface that enables you to design the LINQ to SQL classes you will work with.

The following section demonstrates how to set up a LINQ to SQL instance and pull items from the pubs database.

# Retrieving Data Using LINQ to SQL: Creating the Console Application

To illustrate using LINQ to SQL, the `LinqReading` example begins by calling a single table from the pubs database and using this table to populate some results to the screen.

The next step is to add a LINQ to SQL class. When working with LINQ to SQL, one of the big advantages is that Visual Studio does an outstanding job of making it as easy as possible. Visual Studio provides an object-relational mapping designer, called the Object Relational Designer (O/R Designer), that enables you to visually design the object-to-database mapping.

To start this task, right-click on your solution and select Add | New Item from the provided menu. From the items in the Add New Item dialog, select the LINQ to SQL Classes option, as shown in Figure 10-4.

![](bbox=[0.094, 0.572, 0.749, 0.934])