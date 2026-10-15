
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

在清单 23.14 中，我们正在创建一个名为 PolygonUDT 的 UDT，它被实现为一个结构体，该结构体同时标记有 Serializable 属性和 SqlUserDefinedType 属性，后者指定了 Native 序列化。PolygonUDT 类型包含两个私有变量，numberOfSides 和 sideLength。NumberOfSides 和 SideLength 属性用于获取和设置这些变量的值。PolygonUDT 类型实现了 INullable 接口，其 IsNull() 方法仅返回一个私有变量 isNull 的值，该变量用于跟踪 PolygonUDT 类型是否为空。它还实现了 Null() 方法，该方法实例化并返回该类型的空实例。接下来，ToString() 和 Parse() 方法分别用于将多边形的值作为字符串显示以及将字符串转换为 PolygonUDT 类型。最后，PolygonUDT 类型实现了 PolygonArea() 方法用于返回多边形的面积，以及 UpdateValue() 方法用于修改多边形的边数和边长的数值。

- 9. 在键盘上按下 CTRL+SHIFT+B 键组合来构建解决方案。

在将 UDT 作为 CLR 对象创建之后，您可以直接在 T-SQL 中使用它，也可以在 .NET Framework 4.0 中使用它。清单 23.15 显示了创建程序集 SqlServerProjectUDT 和类型 PolygonUDT 以调用所创建类型的查询：

## Listing 23.15: Creating the SqlServerProjectUDT Assembly and the PolygonUDT Type

```
CREATE ASSEMBLY SqlServerProjectUDT
FROM 'D:\Black Books\C# 2010\Chapter 23\SqlServerProjectUDT\SqlServerProjectUDT\bin\Debug\SqlServerProjectUDT.dll'
GO
CREATE TYPE PolygonUDT
EXTERNAL NAME SqlServerProjectUDT
```

现在，让我们通过在 SQL Server 2008 中编写以下查询来检查 PolygonUDT 类型的使用：

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

接下来，让我们学习如何在 SQL Server 和 .NET Framework 中处理 XML 数据。

## Handling XML Data in SQL Server and .NET Framework

在 In Depth 部分，您已经学习了 XML 数据类型，该类型用于在 SQL Server 中存储 XML 数据。在本节中，您将学习如何使用 XML 数据类型创建一个表，然后在 C# 2010 中创建一个控制台应用程序来访问该表的 XML 数据。让我们从使用 XML 数据类型在 SQL Server 中创建表开始。清单 23.16 显示了创建表 XMLDataTb 的查询：

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

在清单 23.16 中，我们使用 CREATE TABLE 语句创建了 XMLDataTb 表。该表创建了三个列，XMLDataId、XMLContent 和 DataFeedDate。这些列的数据类型分别为 INT、XML 和 DATETIME。然后，使用 INSERT 语句在 XMLDataTb 表中插入了三条记录。

## NOTE

XMLDataTb 表是在用户定义的数据库 MyData 中创建的。

现在，让我们创建一个控制台应用程序来访问存储 XML 数据的 SQL Server 中的 XMLDataTb 表。AccessXMLData 应用程序的源代码也可在提供的 CD 上获得。清单 23.17 显示了 AccessXMLData 应用程序的 Program.cs 文件的代码：

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

在清单 23.17 中，XML 数据是通过使用 SqlDataReader 对象的对象检索的。GetSqlXml() 方法返回 SqlXml 类的对象；而 CreateReader() 方法返回 XmlReader 类的对象。XmlReader 类的 Read() 方法在 while 循环中使用，一次读取一个 XML 节点。在输出中，您可以看到 Name、Address 和 Phone 元素的值以及 EmpID 属性的值。图 23.23 显示了清单 23.17 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1169_0.png)

## Figure 23.23: Displaying the Output of the AccessXMLData Application

现在，让我们总结一下本章讨论的主要主题。

## Summary

在本章中，您学习了 CLR 在 SQL Server 2008 中的集成。本章首先介绍了 CLR 在 SQL Server 2008 中的托管。接下来，您学习了 Microsoft.SqlServer.Server 命名空间以及该命名空间中的可用类、接口和枚举。您还学习了各种 CLR 对象，例如存储过程、触发器和聚合函数。接下来，您学习了如何在 SQL Server 2008 中处理 XML 数据。在本章的 Immediate Solutions 部分，您学习了如何在 .NET Framework 中创建和使用不同的 CLR 对象，以及它们在 SQL 中的使用。

在下一章中，您将学习如何在 ADO.NET 中访问数据。

