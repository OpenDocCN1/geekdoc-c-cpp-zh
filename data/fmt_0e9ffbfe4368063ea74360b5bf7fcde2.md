
最后需要检查的 `ExpressionBuilder` 重写是 `SupportsEvaluate` 和 `EvaluateExpression` 成员。如果您在无编译场景下运行网站（您在 `@Page` 指令中指定了 `compilationMode = "never"`），则需要重写这些方法。`SupportsEvaluate` 属性返回一个布尔值，指示在无编译模式下执行页面时 ASP.NET 是否可以进行评估。如果返回 `True` 且页面正在无编译模式下执行，则当 `GetCodeExpression` 返回一个表示数据值的对象时，`EvaluateExpression` 方法将返回该数据值。参见列表 7-69。

```cs
CodeExpression(BoundPropertyEntry entry, object parsedData,
ExpressionBuilderContext context)
{
    return new CodeCastExpression("Int64",
    new CodePrimitiveExpression(parsedData));
}
```

```cs
public override object ParseExpression
(string expression, Type propertyType, ExpressionBuilderContext context)
{
    return expression;
}
```

```cs
public override bool SupportsEvaluate
{
    get
    {
        return true;
    }
}
public override object EvaluateExpression(object target,
BoundPropertyEntry entry, object parsedData,
ExpressionBuilderContext context)
{
    return parsedData;
}
```

如列表 7-69 所示，如果你想重写 `EvaluateExpression` 方法，只需向 `SupportsEvaluate` 属性返回 `True`。然后，你只需要从 `EvaluateExpression` 方法返回一个对象。

## 总结

在本章中，我们研究了 ASP.NET 中的数据绑定。`SqlDataSource` 控件、`ObjectDataSource` 控件或 `XmlDataSource` 控件的引入，使得从多个数据源查询和显示数据变成了一项易举的任务。通过使用数据控件，你学习了即使是初学者也可以通过极少的代码使用 `GridView`、`ListView` 和 `DetailsView` 控件创建数据处理应用程序。

你看到 ASP.NET 包含了许多可以绑定数据的控件，具体研究了 ASP.NET 工具箱中的 `GridView`、`TreeView`、`Menu` 和 `FormView` 等控件，这些控件在 10/1 版本中得到了增强。最后，我们查看了内联绑定语法如何改进和加强。

# 8 使用 ADO.NET 进行数据管理

本章提供了关于使用 ADO.NET 进行数据管理功能的信息，它是 .NET 框架的核心组件。讨论将从 ADO.NET 的基础开始，深入探讨如何使用 ADO.NET 功能处理关系型数据库的数据。

`ADO.NET` 首先在 1.0 版本中引入，提供了一系列功能来处理连接模式或断开模式下的实时数据。`ADO.NET` 1.0 的主要开发是为了解决用户面临的特定问题，即如何访问数据并遍历数据集合。这种需求在 Web 应用程序开发中经常出现。

`ADO.NET` 处理了今天最常用的数据访问策略。当经典 ADO 被开发时，许多应用程序可以连接到数据存储。随着互联网作为数据通信手段的爆发，需要一种新技术使数据在断开架构中是可用且可更新的。

这些常见的数据访问场景之一是用户必须定位数据位置并遍历数据。这是 Web 页面的常用场景。当收到数据请求时，你可以简单地从数据存储读取数据并填充表格。在这种情况下，目标是尽可能快获取数据。

在断开架构中处理数据的第二种方法是获取数据集合并单独使用它。这可能在服务器上，也可能在客户端上。尽管架构允许你在客户端保留数据（将所有表和关系都放在该处），但经典 ADO 是为二层环境（客户端-服务器）设计的，而 `ADO.NET` 则解决了多层环境的问题。由于 ASP.NET 包含了许多相同的控件，`ADO.NET` 是易于操作的，因为它有一个统一的编程模型。这种统一的编程模型使得在服务器上处理数据与在客户端处理数据是相同的。因为模型是相同的，你会发现在使用 `ADO.NET` 时工作效率更高。

# ADO.NET 基础功能

本章从快速回顾 `ADO.NET` 的基础开始，然后提供了 `ADO.NET` 能力、命名空间和类的概述。它回顾了如何使用 `Connection`、`Command`、`DataAdapter`、`DataSet` 和 `DataReader` 对象。

# 常见 AD.NET 任务

数据源连接打开并准备就绪后，你可能想从数据源读取数据。如果你不想操作数据，只需将其从一个地方读取到另一个地方，请使用 `DataReader` 类。在以下示例（列表 8-1）中，你将使用 `GetCompanyNameData()` 函数从 SQL 数据库提供公司列表。

## 列表 8-1：使用 DataReader 从 SQL 数据库读取数据

```vb
Imports Microsoft.VisualBasic
Imports System.Collections.Generic
Imports System.Data
Imports System.Data.SqlClient

Public Class SelectingData
    Public Function GetCompanyNameData() As List(Of String)
        Dim conn As SqlConnection
        Dim cmd As SqlCommand
        Dim cmdString As String = "Select CompanyName from Customers"
        conn = New SqlConnection("Data Source=SQLEXPRESS;AttachDbFilename=|DataDirectory|\NORTHIND.MDF;Integrated Security=True;UserInstance=True") ' 在代码中将此字符串放在一行
        cmd = New SqlCommand(cmdString, conn)
        conn.Open()

        Dim myReader As SqlReader
        Dim returnData As List(Of String) = New List(Of String)
        myReader = cmd.ExecuteReader(CommandBehavior.CloseConnection)

        While myReader.Read()
            returnData.Add(myReader("CompanyName").ToString())
        End While
        Return returnData
    End Function
End Class
```

```csharp
using System.Data;
using System.Data.SqlClient;
using System.Collections.Generic;

public class SelectingData
{
    public List<string> GetCompanyNameData()
    {
        SqlConnection conn;
        SqlCommand cmd;
        string cmdString = "Select CompanyName from Customers";
        conn = new SqlConnection("Data Source=SQLEXPRESS;AttachDbFilename=|DataDirectory|\NORTHIND.MDF;Integrated Security=True;UserInstance=True"); // 在代码中将此字符串放在一行
        cmd = new SqlCommand(cmdString, conn);
        conn.Open();

        SqlDataReader myReader;
        List<string> returnData = new List<string>();

        myReader = cmd.ExecuteReader(CommandBehavior.CloseConnection);

        while (myReader.Read())
        {
            returnData.Add(myReader["CompanyName"].ToString());
        }
        return returnData;
    }
}
```

在此示例中，你创建了 `SqlConnection` 和 `SqlCommand` 类的实例。然后，在打开连接之前，你通过 `SqlCommand` 命令从 Northwind 数据库选择特定数据。连接打开后（基于传入的命令），你创建一个 `DataReader` 来读取数据，通过使用 `MyReader.Read()` 方法遍历数据。`List(String)` 对象被构建，连接被关闭，对象从函数返回。

# 插入数据

处理数据时，你通常会将数据插入数据源。列表 8-2 显示了如何执行。这些数据可能是通过 XML Web 服务传递给最终用户的，也可能是你在类逻辑中生成的。

## 列表 8-2：向 SQL Server 插入数据

```vb
Public Sub InsertData()
    Dim conn As SqlConnection
    Dim cmd As SqlCommand
    Dim cmdString As String = "Insert Customers (CustomerID, CompanyName, ContactName) Values ('BILLE', 'XYZ Company', 'Bill Evjen')"
    conn = New SqlConnection("Data Source=SQLEXPRESS;AttachDbFilename=|DataDirectory|\NORTHIND.MDF;Integrated Security=True;UserInstance=True") // 在代码中将此字符串放在一行
    cmd = New SqlCommand(cmdString, conn)
    conn.Open()

    cmd.ExecuteNonQuery()
    conn.Close()
End Sub
```

```csharp
public void InsertData()
{
    SqlConnection conn;
    SqlCommand cmd;
    string cmdString = "Insert Customers (CustomerID, CompanyName, ContactName) Values ('BILLE', 'XYZ Company', 'Bill Evjen')";
    conn = new SqlConnection("Data Source=SQLEXPRESS;AttachDbFilename=|DataDirectory|\NORTHIND.MDF;Integrated Security=True;UserInstance=True"); // 在代码中将此字符串放在一行
    cmd = new SqlCommand(cmdString, conn);
    conn.Open();

    cmd.ExecuteNonQuery();
    conn.Close();
}
```

### 第 8 章：使用 ADO.NET 进行数据管理

向 SQL 插入数据非常直接且简单。使用 SQL 命令字符串，你可以为特定列插入特定值。实际的插入操作是通过 `cmd.ExecuteNonQuery()` 命令启动的。当你不需要返回任何结果时，可以使用此命令在数据上执行操作。

# 更新数据

除了向数据库插入新记录外，你还经常需要更新表中现的数据行。想象有一个可以一次性更新多个记录的表。在示例 8-3 中，如果员工在公司工作了五年或以上，你希望通过在 `emp_bonus` 列中设置特定值来更新该员工。

## 示例 8-3：在 SQL Server 中更新数据

```VB
Public Function UpdateEmployeeBonus() As Integer
Dim conn As SqlConnection
Dim cmd As SqlCommand
Dim RecordsAffected As Integer
Dim cmdString As String = "UPDATE Employees SET emp_bonus=1000 WHERE " & \
"yrs_duty>=5"
conn = New SqlConnection("Data Source=\SQLEXPRESS;AttachDbFilename=\DataDirectory\NORTHWND.MDF;IntegratedSecurity=True;UserInstance=True") // 将此字符串在代码中独占一行
cmd = New SqlCommand(cmdString, conn)
conn.Open()

RecordsAffected = cmd.ExecuteNonQuery()
conn.Close()

Return RecordsAffected
Function
```

```csharp
public int UpdateEmployeeBonus()
{
    SqlConnection conn;
    SqlCommand cmd;
    int RecordsAffected;
    string cmdString = "UPDATE Employees SET emp_bonus=1000 WHERE yrs_duty>=5";
    conn = new SqlConnection("Data Source=\SQLEXPRESS;AttachDbFilename=\DataDirectory\NORTHWND.MDF;IntegratedSecurity=True"); // 将此字符串在代码中独占一行
    cmd = new SqlCommand(cmdString, conn);
    conn.Open();

    RecordsAffected = cmd.ExecuteNonQuery();
    conn.Close();

    return RecordsAffected;
}
```

此更新函数遍历表中的所有员工，如果员工在公司工作已超过五年，则将 `emp_bonus` 字段的值更改为1000。这是通过 SQL 命令字符串实现的。这些更新功能很棒的一点是，你可以通过将 `ExecuteNonQuery()` 命令赋值给 `RecordsAffected` 变量来捕获更新的记录数。该函数返回受影响记录的总数。

# 删除数据

除了读取、插入和更新数据外，你有时需要从数据源删除数据。删除数据是一个简单的过程，即使用 SQL 命令字符串并像在更新示例那样使用 `ExecuteNonQuery()`。参见示例 8-4 的说明。

## 示例 8-4：从 SQL Server 中删除数据

```VB
Public Function DeleteEmployee() As Integer
Dim conn As SqlConnection
Dim cmd As SqlCommand
Dim RecordsAffected As Integer
Dim cmdString As String = "DELETE Employees WHERE LastName='Evjen'"
conn = New SqlConnection("Data Source=\SQLEXPRESS;AttachDbFilename=[DataDirectory]\\NORTHWIND.MDF;IntegratedSecurity=True;")
// 将此字符串在代码中独占一行
cmd = New SqlCommand(cmdString, conn)
conn.Open()

RecordsAffected = cmd.ExecuteNonQuery()
conn.Close()

Return RecordsAffected
End Function
```
