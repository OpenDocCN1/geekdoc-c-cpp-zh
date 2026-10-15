+   - Scalar functions — Returns a single value, such as numbers, floating points, Booleans, and strings
+   - Table-valued functions — Returns a set of rows from a table

Listing 23.4 shows an example of a UDF:

# Listing 23.4: Showing an Example of a UDF

```
CREATE FUNCTION RectArea(@RectLength decimal(4,1), @RectWidth decimal(4,1))
RETURNS decimal(8,2)
AS
BEGIN
RETURN ( @RectLength * @RectWidth )
END
```

In Listing 23.4, we are creating a UDF, RectArea, with two parameters, RectLength and RectWidth. The RectArea function is created to calculate the area of any item having the rectangular shape. Now, let’s use the RectArea UDF in a SQL query to create a table, as shown in Listing 23.5:

# Listing 23.5: Showing a Query to Create a Table Using a UDF

```
CREATE TABLE Papers
(
    PaperID int PRIMARY KEY,
    PaperLength decimal(4,1),
    PaperWidth decimal(4,1),
    PaperArea AS
        (
            dbo.RectArea(PaperLength, PaperWidth)
        )
)
```

In Listing 23.5, we are creating a table, named Papers, with four columns: PaperID, PaperLength, PaperWidth, and PaperArea. The PaperArea column is using the RectArea function, which is already created in T-SQL (given in Listing 23.4), to calculate the area of a paper in rectangular shape.

Let’s now learn about UDT.

# Exploring UDT

UDT is a customized type, which is a collection of other data types, data values, or methods. In SQL, there are various built-in data types, such as Integer, Varchar, and Decimal. You can combine these built-in data types into groups to create customized type with specific capabilities. In SQL Server 2008, you can create a UDT by using the sp_addtype stored procedure. An example of UDT in SQL Server 2008 is given as follows:

```
EXEC sp_addtype StudentID 'CHAR(10)', 'NOT NULL'
```

In the preceding example, a UDT, named StudentID, of CHAR type is created. The StudentID type can accept the data of 10 characters at maximum, but not a null value.

Let’s learn how to handle the XML data in SQL Server 2008.

# Using XML Data in SQL Server

One of the important data types in SQL is XML data type. In the older versions of SQL Server, XML data is stored in the form of string or binary large objects (blobs) form. However, now the XML data type allows you to mix the SQL queries with XQuery expressions to search within an XML file. An XML data type can be used as a variable, column, parameter, or a return value by a UDF. Using Microsoft Office, you can also store Word and Excel documents in the form of XML data. Moreover, the output of Microsoft Office applications can be directly stored in SQL Server.

As far, you have taken the conceptual overview of the integration of CLR and SQL Server. Now, let’s learn about creating CLR objects in .NET Framework and using these objects in SQL Server 2008, which you learn in the Immediate Solutions section.