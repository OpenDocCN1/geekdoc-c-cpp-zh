
程序集创建在 `C:\Windows\.NET\Framework\v4.0.30319`。你需要将程序集拷贝到你保存程序集的位置。

之后，使用 SQL Server 2008 使用以下查询创建程序集。列表 20.7 显示了如何创建程序DetailsSP 程序集以及 GetDetailsSP 存储过程以调用 SqlObject。

### 列表 20.7：创建 ProductDetailsSP 程序集和 GetDetailsSP 存储过程

```sql
CREATE ASSEMBLY productdetailssp
GO
'D:\share\2012_chapter_20\productdetailssp\productdetailssp.dll'
GO
CREATE PROCEDURE Getproductdetails
  (@ProductID INT)
AS EXTERNAL NAME productdetailssp.Storedprocedures.GetDetailsSP
```

在列表 20.7 中，创建了程序集 `ProductDetailsSP`，然后在 CLR 对象侧创建了存储过程 `GetDetailsSP`。

> 注意
以下查询显示如何在 SQL Server 2008 中执行 CLR：

```sql
exec_sp_configure 'clr enabled', 1
reconfigure
go
```

执行列表 20.7 中的查询后，你可以按照如下查询执行 `GetDetailsSP` 存储过程：

```sql
EXEC GetDetailsSP 3
```

| Results | Messages | ProductID | Name | QuantityPerUnit | Unit | InStock |
|---|---|---|---|---|---|---|
| 1 | | 3 | Imported Syrup | 12 - 500 ml | 10.00 | 13 |

图 20.6：`GetDetailsSP` 存储过程的输出

除了在 T-SQL 中调用存储过程外，你还可以在 C# 的 Windows 应用程序或控制台应用程序中使用。让我们在控制台中使用 `GetDetailsSP` 存储过程。

执行以下步骤创建 `UseProductSP` 应用程序：

- 1. 打开 Microsoft Studio 2012。
- 2. 创建名为 `UseProductSP` 的控制台应用程序。
- 3. 如列表 20.8 所示修改 `Program.cs` 的代码。

# 第 20 章：NET 与 SQL Server

列表 20.8：`Program.cs`文件的代码
```csharp
using System;
using System.Collections.Generic;
using System.Data;
using System.Data.SqlClient;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace useProductSP
{
    class Program
    {
        static void main(string[] args)
        {
            string conn = "Data Source=DEBOLENA-PC;Initial Catalog=master;Integrated Security=True";
            var conn = new SqlConnection(conn);
            SqlCommand cmd = conn.CreateCommand();
            cmd.CommandText = "ProductDetails";
            cmd.CommandType = CommandType.StoredProcedure;
            var param = new SqlParameter("ProductID", 1);
            cmd.Parameters.Add(param);
            conn.Open();
            SqlDataReader dr = cmd.ExecuteReader();
            while (dr.Read())
            {
                Console.WriteLine("Product ID: " + dr[0] + " \nitem: " + dr[1] + " \nquantity: " + dr[2] + " \nprice: " + dr[3] + " \nunstock: " + dr[4] + " \nproductname: " + dr[5] + " \nQuantityUnit: " + dr[6] + " \nunitprice: " + dr[7] + " \nunitStock: " + dr[8]);
            }
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
        }
    }
}
```

在列表 20.8 中，创建了一个 `SqlConnection` 变量来执行 `ProductDetails` 存储过程。该存储过程由 `ExecuteReader()` 方法返回，并在 `while` 循环中使用 `Read()` 方法显示所选项目的详细信息。

- 4. 按键盘上的 `CTRL+F5` 键执行 `UseProductSP` 应用程序。显示 `UseProductSP` 应用程序的输出：

![](img/17af790174c480761404624aeed9b30b_975_0.png)

图 20.7：`UseProductSP` 应用程序的输出

接下来，让我们学习创建和使用 CLR 对象——触发器。

## 创建和使用触发器

在本节中，你将学习如何在 .NET Framework 中创建 CLR 对象。要实现这一点，你需要在 SQL Server 项目中添加一个触发器类 CLR 对象。我们创建了一个名为 `SqlSqlServerTrg` 的 SQL Server 项目，并向其添加一个触发器 `InsertPersonalDetailsTrg.cs`。

按照以下步骤在 Visual Studio 2012 中创建 `SqlServerProjectTrg` 项目：

- 1. 打开 Visual Studio 2012。
- 2. 创建一个名为 `SqlServerProjectTrg` 的 SQL Server 数据库项目，如图 20.8 所示。

![](img/17af790174c480761404624aeed9b30b_976_0.png)

图 20.8：创建 `SqlServerProjectTrg` 项目

- 3. 点击 `OK` 按钮（图 20.8）。Visual Studio 2012 中将显示 `SqlServerProjectTrg` 项目。
- 4. 在解决方案管理器中右键点击 `SqlServerProjectTrg` 项目，选择“添加→新建项”。将出现“新建项-SqlServerProjectTrg”数据库对话框。
- 5. 选择 `InsertPersonalDetailsTrg` 并使用默认名称或输入新名称。在我们的情况下，我们在 `Name` 框中输入名称 `InsertPersonalDetailsTrg`。
- 6. 点击添加 按钮。`InsertPersonalDetailsTrg.cs` 文件被添加到 `SqlServerProjectTrg` 项目中。
- 7. 修改 `InsertPersonalDetailsTrg.cs` 文件的代码，如图 20.9 所示。

列表 20.9：`InsertPersonalDetailsTrg.cs`文件的代码

```csharp
using System;
using System.Data;
using System.Data.SqlClient;
using Microsoft.SqlServer.Server;
using System.Text.RegularExpressions;
public class ClassTriggers
{
    // 为目标输入表或视图并取消注释属性行
    // [Microsoft.SqlServer.Server.Trigger("InsertPersonalDetailsTrg", Target = 
    // "PersonalDetails_Trg", Event = "INSERT")]
    public static void InsertPersonalDetailsTrg()
    {
        SqlTriggerContext triggerContext = SqlContext.TriggerContext;
        if (triggerContext.TriggerAction == TriggerAction.Insert)
        {
            var conn = new SqlConnection("Context Connection=true");
            var cmd = new SqlCommand();
            cmd.Connection = conn;
            cmd.CommandText = "SELECT UserName FROM INSERTED";
            conn.Open();
            string uname = (string)cmd.ExecuteScalar();
        }
    }
}
```

```csharp
conn.Close();
if (!Regex.IsMatch(uname, "@([\w-]+\.)([\w-]+\.)*([\w-]+\.)*?[\w-]+")) {
    throw new FormatException("Invalid user name");
} else {
    SqlContext.Pipe.Send("Trigger FIRED");
}
```

在 2019 中，我们在 `PersonalDetails_Trg` 表上创建了一个名为 `InsertPersonalDetailsTrg` 的用户自定义触发器。该触发器检查提供的用户名是否符合正确格式。如果不符合，则抛出 `FormatException`；否则，将发送“Trigger FIRED”消息。

以下命令允许你编译并执行触发器。

## 第20 章：.NET SQL Server

```cs
total += Value.Value;
}
public void Merge(MyAgg_Total group) {
    total += group.Total;
}
public SqlInt32 Terminate() {
    return new SqlInt32(total);
}
// 这是一个占位成员字段
private int _val;
}
```

在列表 20.11 中，我们创建了一个名为 `MyAgg_Total` 的用户定义聚合函数，它由 `Init()`、`Accumulate()` 和 `Terminate()` 方法组成。有一个 `int` 类型的变量 `total`，它在 `Init()` 中初始化。`total` 变量的值在 `Accumulate()` 和 `Merge()` 方法中更新。`total` 中存储最终值由 `Terminate()` 方法返回。

现在，打开 VS2012 开发者命令提示符并执行以下命令：
`csc %SystemRoot%\Microsoft.NET\Framework\v4.0.30319 /target:library`
`C:\Sharp2012_BlackBook\Chapter_20_Code\SqlSqlServerProjectagg\SqlServerProjectagg\MyAgg_Total.Total.dll`

程序集创建于 `C:\Windows\Microsoft.NET\Framework\v4.0.30319`。你需要将程序集从该位置复制到你保存的位置。

之后，使用 SQL Server 2008 创建该聚合，并使用以下查询进行聚合。20.12 显示了创建聚合 `Aggregate_Assembly` 和聚合 `MyAgg_Total` 的查询：

列表 20.12：创建 `Aggregate_Assembly` 和 `MyAgg_Total`
```sql
CREATE AGGREGATE Aggregate_Assembly
FROM 'C:\Sharp2012_BlackBook\Chapter_20_Code\SqlSqlServerProjectagg\SqlServerProjectagg\MyAgg_Total.dll'
GO
CREATE AGGREGATE MyAgg_Total (@Value int)
RETURNS int EXTERNAL NAME Aggregate_Assembly.MyAgg_Total
GO
```

现在，让我们在以下查询中使用创建的聚合函数 `MyAgg_Total`：
```sql
select ProductID, OrderID, MyAgg_Total(UnitPrice) AS TotalPrice, MyAgg_Total(Quantity) AS TotalQuantity
FROM OrderDetails
GROUP BY ProductID, OrderID
ORDER BY OrderID
```

前面的查询显示了结果，如图 20.11 所示：![](img/17af90174c48076140624aeed9b30.png)

图 20.11：使用聚合后的结果

接下来，让我们学习如何创建和使用 UDF（用户定义函数）。

## 创建和使用 UDF

在本节中，学习如何在 .NET Framework 中作为 CLR 对象来创建 UDF。要实现这一点，你需要在 SQL Server 项目中添加 UDF CLR 对象。让我们创建一个名为 `SqlProjectUDF` 的 SQL Server 项目，并向其添加一个 UDF：`RectAreaFunction.cs`。

按照以下步骤在 Visual Studio 2012 中创建 `SqlProjectUDF` 项目：

1. 打开 Visual Studio 2012。
2. 创建一个名为 `SqlProjectUDF` 的 SQL Server 数据库项目。`SqlProjectUDF` 项目显示在 Visual Studio 2012 中。
3. 在解决方案管理器中右键点击 `SqlProjectUDF` 项目，选择“添加 -> 新项”。弹出“添加新项-SqlProjectUDF”对话框。
4. 选择 CLR C# 函数模板，并输入默认名称或新名称。在我们的用例中，我们在文本框中命名为 `RectAreaFunction.cs`。
5. 点击“添加”按钮。`RectAreaFunction.cs` 文件被添加到 `SqlProjectUDF` 项目中。
6. 修改 `RectAreaFunction.cs` 的代码，如列表 20.13 所示：

列表 20.13：`RectAreaFunction.cs` 的代码
```cs
using System;
using System.Data;
using System.Data.SqlClient;
using System.Data.SqlDbType;
using Microsoft.SqlServer.Server;
public partial class UserFunctions
{
    [SqlFunction]
    public static decimal RectAreaFunction(decimal rectLength, decimal rectWidth)
    {
        // 将你的代码放在此处
        return new decimal(rectLength * rectWidth);
    }
}
```

在列表 20.13 中，我们正在创建一个包含两个参数 `rectLength` 和 `rectWidth` 的 UDF：`RectAreaFunction`。`RectAreaFunction` 根据提供的参数值返回矩形的面积。注意，部署函数时需要 `SqlFunction` 特性。

现在，打开 Visual Studio 命令提示符并执行以下命令：
`cd C:\Windows\Microsoft.NET\Framework\v4.0.30319`
`regregasm /assembly`
`cd D:\Sharp2012_BlackBook\Chapter_20_Code\SqlServerProjectUDF\SqlServerProjectUDF\bin\RectAreaFunction.dll`

程序集创建于 `C:\Windows\Microsoft.NET\Framework\v4.0.30319`。你需要将此程序集从该位置复制到你保存的位置。

之后，打开 SQL Server 2008 并使用查询创建程序集和用户定义函数。列表 20.14 显示了创建程序集 `SqlProjectUDF` 以及一个用于调用所创建的 CLR 对象的函数 `RectAreaFunction`。

列表 20.14：创建 `SqlProjectUDF` 程序集和 `RectAreaFunction` 函数
```sql
CREATE ASSEMBLY SqlProjectUDF
```
