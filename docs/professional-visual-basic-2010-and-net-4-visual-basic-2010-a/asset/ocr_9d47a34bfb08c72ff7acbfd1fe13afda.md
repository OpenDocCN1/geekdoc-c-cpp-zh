If you pass that to SQL Server using ExecuteReader on SqlCommand (or any execute method, for that matter), SQL Server has to compile the code before it can run it, in much the same way that VB .NET applications have to be compiled before they can be executed. This compilation takes up SQL Server’s time, so it is easy to deduce that if you can reduce the amount of compilation that SQL Server has to do, database performance should increase. (Compare the speed of execution of a compiled application against interpreted code.)

That’s what stored procedures are all about: You create a procedure, store it in the database, and because the procedure is recognized and understood ahead of time, it can be compiled ahead of time and ready for use in your application.

One other benefit of using stored procedures in your code is that it is generally safer. When using SQL without stored procedures, there is always the temptation to build the SQL statement by concatenating strings. With this, there is the danger — particularly if some of those strings are user generated — that the resulting SQL is invalid or malicious; for example, if you had a text box where a user could type in search criteria, that you then concatenated into a query, using code such as:

```
Dim sql As String = "SELECT * FROM myTable WHERE field LIKE '" & query & "%'"
```

This looks innocent enough, but you could get into trouble very quickly if the user entered something like:

```
Bob;delete * from systables;
```

Using stored procedures prevent an attack like this from happening.

Stored procedures are very easy to use, but the code to access them is sometimes a little verbose. The next section demonstrates some code that can make accessing stored procedures a bit more straightforward, but to make things clearer, let’s start by building a simple application that demonstrates how to create and call a stored procedure.

# Creating a Stored Procedure

To create a stored procedure, you can either use the tools in Visual Studio .NET or you can use the tools in SQL Server’s Enterprise Manager if you are using SQL Server 2000, or in SQL Server Management Studio if you are using SQL Server 2005/2008. (Technically, you can use a third-party tool or just create the stored procedure in a good, old-fashioned SQL script.)

This example builds a stored procedure that returns all of the columns for a given author ID. The SQL to do this looks like the following:

```
SELECT
    au_id, au_lname, au_fname, phone,
    address, city, state, zip, contract
FROM
    authors
WHERE
    au_id = whatever author ID you want
```

The “whatever author ID you want” part is important. When using stored procedures, you typically have to be able to provide parameters into the stored procedure and use them from within code. This is not a book about SQL Server, so this example focuses only on the principle involved. You can find many resources on the Web about building stored procedures (they have been around a very long time, and they are most definitely not a .NET-specific feature).

Variables in SQL Server are prefixed by the @ symbol, so if you have a variable called au_id, then your SQL will look like this:

```
SELECT
    au_id, au_lname, au_fname, phone,
    address, city, state, zip, contract
FROM
    authors
WHERE
    au_id = @au_id
```