
## SUMMARY

In this chapter, you have seen how to create and consume web services using C# and the Visual Studio .NET development platform. Doing this is perhaps surprisingly simple, but is instantly recognizable as something that could prove to be incredibly useful.

It has also been pointed out that web services may be accessed from any platform. This is the result of using the SOAP protocol, which doesn't limit you to .NET.

The main example developed in this chapter illustrates how you can create .NET-distributed applications with ease. I have assumed here that you are using a single server to test things, but there is no reason why the web service shouldn't be completely separate from the client. It may even be on a separate server from the database if an additional data tier is required.

The use of data caching throughout is another important technique to master for use in large-scale applications, which might have thousands of users connecting simultaneously.

Exchanging data via SOAP headers, introduced in the last example, is another useful technique that can be worked into your applications. The example uses the exchange of a login token, but there is no reason why more complex data shouldn't be exchanged in this way. Perhaps this could be used for simple password protection of web services, without having to resort to imposing more complex security.

Remember that web service consumers don't necessarily have to be web applications. There is no reason why you can't use web services from Windows Forms or WPF applications — which certainly seems to be an attractive option for a corporate intranet. One added bonus concerning web services in ASP.NET is the ability to call web services asynchronously, using a simple, event-driven system. This fits in perfectly with Windows Forms applications, and means that you can keep your applications responsive while complicated web services carry out hard work for you.

As a final note, it is worth mentioning that web services can be seen as a stripped down subset of the more recent WCF technology, covered in Chapter 43, “Windows Communication Foundation.” This doesn’t mean, though, that you should always use WCF services rather than web services — web services are much simpler to implement and the simplicity is a great thing.

## LINQ to SQL

### WHAT'S IN THIS CHAPTER?

- Working with LINQ to SQL using Visual Studio 2010
- Mapping LINQ to SQL objects to database entities
- Building LINQ to SQL operations without the O/R Designer
- Using the O/R Designer with custom objects
- Querying the SQL Server database using LINQ
- Stored procedures and LINQ to SQL

You will probably find the .NET Language Integrated Query Framework (LINQ) in C# 4.0 to be one of the more exciting features the language has to offer. Basically, what LINQ provides is a lightweight façade over programmatic data integration. This is such a big deal because *data is king.*

Pretty much every application deals with data in some manner, whether that data comes from memory (in-memory data), databases, XML files, text files, or something else. Many developers find it very difficult to move from the strongly typed object-oriented world of C# to the data tier where objects are second-class citizens. The transition from one world to the next was a kludge at best and was full of error-prone actions.

In C#, programming with objects means a wonderful, strongly typed ability to work with code. You can navigate very easily through the namespaces, work with a debugger in the Visual Studio IDE, and more. However, when you have to access data, you will notice that things are dramatically different.

You end up in a world that is not strongly typed, where debugging is a pain or even non-existent, and you end up spending most of the time sending strings to the database as commands. As a developer, you also have to be aware of the underlying data and how it is structured or how all the data points relate.

LINQ provides a strongly typed interface to the underlying data stores. It provides the means for developers to stay within the coding environment that they are used to and access the underlying data as objects that work with the IDE, IntelliSense, and even debugging.

## LINQ TO SQL USING VISUAL STUDIO 2010

LINQ to SQL in particular is a means to have a strongly typed interface against a SQL Server database. You will find the approach that LINQ to SQL provides is by far the easiest approach to querying SQL Server available at the moment. It is not just about querying single tables within the database. For instance, if you call the Customers table of the Northwind database and want to pull a customer's specific orders from the Orders table in the same database, LINQ will use the relations of the tables and make the query on your behalf. LINQ will query the database and load up the data for you to work with from your code (again, strongly typed).

It is important to remember that LINQ to SQL is not only about querying data, but you are also able to perform the Insert/Update/Delete statements needed.

You can also interact with the entire process and customize the operations performed to add your own business logic to any of the CRUD operations (Create/Read/Update/Delete).

Visual Studio 2010 comes into strong play with LINQ to SQL in that you will find an extensive user interface that allows you to design the LINQ to SQL classes you will work with.

The next section focuses on how to set up your first LINQ to SQL instance and pull items from the Products table of the Northwind database.

### Calling the Products Table

For an example of using LINQ to SQL, this section starts by calling a single table from the Northwind database and using it to populate results to the screen.

To start off, create a console application (using .NET Framework 4) and add the Northwind database file to this project (Northwind.mdf).

> The following example makes use of the Northwind.mdf SQL Server Express Database file. To get this database, search for "Northwind and pubs Sample Databases for SQL Server 2000." You can find this link at http://www.microsoft.com/downloads/details.aspx?FamilyID=06... When installed, you will find the Northwind.mdf file in the C:\SQL Server 2000 Sample Databases directory. To add this database to your application, right-click the solution you are working with and select Add Existing Item. From the provided dialog box, you are then able to browse to the location of the Northwind.mdf file that you just installed. If you are having trouble getting permissions to work with the database, make a data connection to the file from the Visual Studio Server Explorer and you will be asked to be made the appropriate user of the database. VS will make the appropriate changes on your behalf for this to occur.

By default now, when creating many of the application types provided in .NET Framework 4 within Visual Studio 2010, you will notice that you already have the proper references in place to work with LINQ. When creating a console application, you will get the following using statements in your code:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

From this, you can see that the LINQ reference required is already in place.

### Adding a LINQ to SQL Class

The next step is to add a LINQ to SQL class. When working with LINQ to SQL, one of the big advantages you will find is that Visual Studio 2010 does an outstanding job of making it as easy as possible. Visual Studio provides an object-relational mapping designer, called the O/R Designer, which allows you to visually design the object to database mapping.

To start this task, right-click your solution and select Add New Item from the provided menu. From the items in the Add New Item dialog box, you will find LINQ to SQL Classes as an option. This is presented in Figure 56-2.

![](img/d7d2ffa0a76feaab821930e95daace93_1795_0.png)

FIGURE 56-2

Because this example is using the Northwind database, name the file Northwind.dbml. Click the Add button, and you will see that this operation creates a couple of files for you. Figure 56-3 presents the Solution Explorer after adding the Northwind.dbml file.

A number of things were added to your project with this action. The Northwind.dbml file was added and it contains two components. Because the LINQ to SQL class that was added works with LINQ, the following references were also added on your behalf: System.Core, System.Data.DataSetExtensions, System.Data.Linq, and System.Xml.Linq.

### Introducing the O/R Designer

Another big addition to the IDE that appeared when you added the LINQ to SQL class to your project (the Northwind.dbml file), was a visual

![](img/d7d2ffa0a76feaab821930e95daace93_1795_1.png)

FIGURE 56-3
