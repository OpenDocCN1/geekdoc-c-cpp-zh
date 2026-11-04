# # 37

# # LINQ to SQL

Lesson 36 provided an introduction to LINQ to Objects. This lesson gives a brief introduction to another of the LINQ family of technologies: LINQ to SQL.

LINQ to SQL lets you use queries similar to those provided by LINQ to Objects to manipulate SQL Server databases. It uses a set of classes to represent database objects such as tables and records. The classes provide intuitive methods for adding, modifying, deleting, and otherwise manipulating the records.

In this lesson you learn the basics of LINQ to SQL. You learn how to make LINQ objects representing a SQL Server database and how to add records to the database. You also learn how to perform queries similar to those described in Lesson 36 to filter and sort data taken from the database.

Note that the programs and techniques described in this lesson demonstrate only very simple uses of LINQ to SQL. For more information, search the web. Microsoft’s “LINQ to SQL” page at msdn.microsoft.com/library/bb386976.aspx provides a good starting point for learning more about LINQ to SQL.

# ## CONNECTING TO THE DATABASE

The first step in creating a LINQ to SQL program is connecting to the database. Create a Windows Forms application as usual. Then open the Server Explorer shown in Figure 37-1. (Use the View menu’s Server Explorer command if you can’t find it.)