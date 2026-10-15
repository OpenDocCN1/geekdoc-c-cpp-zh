```
{
    if (s.IsNull || s.Value.ToLower().Equals("null"))
        return Null;
    string[] str = s.ToString().Split(',');
    if (str.Length != 2)
        return Null;
    PolygonUDT p = new PolygonUDT();
    try
    {
        p.numberOfSides = int.Parse(str[0]);
        p.sideLength = double.Parse(str[1]);
        if (p.numberOfSides > 2 && p.sideLength > 0)
            return p;
        else
            return Null;
    }
    catch (Exception)
    {
        return Null;
    }
}
public int NumberOfSides
{
    get { return numberOfSides; }
    set
    {
        if (value > 2)
        {
            numberOfSides = value;
            isNull = false;
        }
        else
            isNull = true;
    }
}
public double SideLength
{
    get { return sideLength; }
    set
    {
        if (value > 0)
        {
            sideLength = value;
            isNull = false;
        }
        else
            isNull = true;
    }
}
[SqlMethod]
public double PolygonArea()
{
    if (!isNull)
        return .25 * numberOfSides * Math.Pow(sideLength, 2) *
               (1 / Math.Tan(Math.PI / numberOfSides));
    else
        return 0;
}
[SqlMethod(IsMutator = true, OnNullCall = false)]
public void UpdateValue(int numberOfSides, double sideLength)
{
    if (numberOfSides > 2 && sideLength > 0)
    {
        this.numberOfSides = numberOfSides;
        this.sideLength = sideLength;
    }
}
```
this.isNull = false;
}
else
    isNull = true;
}

In Listing 23.14, we are creating a UDT, called PolygonUDT, which is implemented as a struct marked with both a Serializable attribute and a SqlUserDefinedType attribute specifying Native serialization. The PolygonUDT type contains two private variables, numberOfSides and sideLength. The NumberOfSides and SideLength properties are used to get and set the value of these variables. The PolygonUDT type implements the INullable interface with the IsNull() method that simply returns the value of a private variable, isNull, which keeps track of whether the PolygonUDT type is null. It also implements the Null() method that instantiates and returns a null instance of the type. Next, the ToString() and Parse() methods are used for displaying the value of a polygon as a string and converting a string to the PolygonUDT type, respectively. Finally, the PolygonUDT type implements the PolygonArea() method for returning the area of a polygon, and the UpdateValue() method for modifying the values of the number and length of side of a polygon.

- 9. Press the CTRL+SHIFT+B keys combination on the keyboard to build the solution.

After creating a UDT as a CLR object, you can use it either directly in T-SQL or in .NET Framework 4.0. Listing 23.15 shows the query to create an assembly, SqlServerProjectUDT, and a type, PolygonUDT, to invoke the created type:

## Listing 23.15: Creating the SqlServerProjectUDT Assembly and the PolygonUDT Type

```
CREATE ASSEMBLY SqlServerProjectUDT
FROM 'D:\Black Books\C# 2010\Chapter 23\SqlServerProjectUDT\SqlServerProjectUDT\bin\Debug\SqlServerProjectUDT.dll'
GO
CREATE TYPE PolygonUDT
EXTERNAL NAME SqlServerProjectUDT
```

Now, let’s check the use of the PolygonUDT type by writing the following query in SQL Server 2008:

```
DECLARE @plg PolygonUDT
SET @plg = CONVERT(PolygonUDT, '7, 3.1')
PRINT @plg.IsNull
PRINT @plg.ToString()
PRINT @plg.NumberOfSides
PRINT @plg.SideLength
PRINT @plg.PolygonArea()
SET @plg.UpdateValue(4, 6)
PRINT @plg.ToString()
PRINT @plg.PolygonArea()
```

## Figure 23.22: Displaying the Result of Using the PolygonUDT Type in SQL

![](img/e073a4882197be4ab61103cbe0bcb394_1167_0.png)

Next, let’s learn how to handle XML data in SQL Server and .NET Framework.

## Handling XML Data in SQL Server and .NET Framework

In the In Depth section, you have already learned about the XML data type, which is used to store the XML data in SQL Server. In this section, you learn to create a table using the XML data type, and then create a console application in C# 2010 to access the XML data of this table. Let’s start with creating a table in SQL Server using the XML data type. Listing 23.16 shows a query to create a table, XMLDataTb, in SQL Server:

## Listing 23.16: Creating a Table Using XML Data Type

```
CREATE TABLE XMLDataTb
(
XMLDataId INT NOT NULL PRIMARY KEY,
XMLContent XML,
DataFeedDate DATETIME DEFAULT GETDATE()
)
insert into XMLDataTb values (1,'<Record><Employee EmpID="1"/>
<Name>Kabir</Name>
<Address>Delhi</Address>
<Phone>1111111</Phone>
</Record>','06/Aug/2010')
insert into XMLDataTb values (2,'<Record><Employee EmpID="4"/>
<Name>Shilpa</Name>
<Address>Delhi</Address>
<Phone>2222222</Phone>
</Record>','05/Aug/2010')
insert into XMLDataTb values (3,'<Record><Employee EmpID="2"/>
<Name>Dheeraj</Name>
<Address>Dubai</Address>
<Phone>4444444</Phone>
</Record>','06/Aug/2010')
```

In Listing 23.16, we are creating the XMLDataTb table using the CREATE TABLE statement. This table is created with three columns, XMLDataId, XMLContent, and DataFeedDate. The data types of these columns are INT, XML, and DATETIME, respectively. Then, three records are inserted in the XMLDataTb table using the INSERT statement.

## NOTE

The XMLDataTb table is created in a user defined database, MyData.

Now, let’s create a console application to access the XMLDataTb table in SQL Server, which stores XML data. The source code of the AccessXMLData application is also available in the provided CD. Listing 23.17 shows the code of the Program.cs file of the AccessXMLData application:

## Listing 23.17: Showing the Code of the Program.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Data;
using System.Data.SqlClient;
using System.Data.SqlTypes;
using System.Xml;
namespace AccessXMLData
{
    class Program
    {
        static void Main(string[] args)
        {
            string connection = @"Data Source=.;Initial Catalog=MyData;Integrated Security=True";
            var con = new SqlConnection(connection);
            var command = con.CreateCommand();
            command.CommandText = "Select * from XMLDataTb";
            con.Open();
            var reader = command.ExecuteReader(CommandBehavior.CloseConnection);
            StringBuilder xmldata = new StringBuilder("-----Employees-----", 40);
            Console.WriteLine(xmldata.ToString());
            while (reader.Read())
            {
                SqlXml xml = reader.GetSqlXml(1);
                XmlReader xmlreader = xml.CreateReader();
                while (xmlreader.Read())
```

```
{
    if (xmlreader.Name == "Employee" && xmlreader.IsStartElement())
    {
        Console.WriteLine("Employee: {0}",
        xmlreader.GetAttribute("EmpID"));
    }
    else if (xmlreader.Name == "Name" && xmlreader.IsStartElement())
    {
        Console.WriteLine("Name: {0}", xmlreader.ReadString());
    }
    else if (xmlreader.Name == "Address" && xmlreader.IsStartElement())
    {
        Console.WriteLine("Address: {0}", xmlreader.ReadString());
    }
    else if (xmlreader.Name == "Phone" && xmlreader.IsStartElement())
    {
        Console.WriteLine("Phone: {0}", xmlreader.ReadString());
    }
    }
    xmlreader.Close();
    Console.WriteLine();
}
reader.Close();
}
}
```

In Listing 23.17, the XML data is retrieved by using an object of the SqlDataReader object. The GetSqlXml() method returns an object of the SqlXml class; while the CreateReader() method returns an object of the XmlReader class. The Read() method of the XmlReader class is used in a while loop to read XML nodes one by one. In the output, you can see the values of the Name, Address, and Phone elements and the EmpID attribute. Figure 23.23 shows the output of Listing 23.17:

![](img/e073a4882197be4ab61103cbe0bcb394_1169_0.png)

## Figure 23.23: Displaying the Output of the AccessXMLData Application

Now, let’s summarize the main topics discussed in this chapter.

## Summary

In this chapter, you have learned the integration of CLR in SQL Server 2008. The chapter has begun with hosting of CLR in SQL Server 2008. Next, you have learned about the Microsoft.SqlServer.Server namespace and available classes, interfaces, and enumerations in the namespace. You have also learned about various CLR objects, such as stored procedures, triggers, and aggregate functions. Next, you have learned how to handle XML data in SQL Server 2008. In the Immediate Solutions section of the chapter, you have learned to create and use different CLR objects in .NET Framework and their use in SQL.

In the next chapter, you learn how to access data in ADO.NET.
