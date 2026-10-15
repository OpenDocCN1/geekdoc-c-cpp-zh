
前述查询显示结果集；如图 23.18 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1162_0.png)

**图 23.18：显示使用聚合后的结果集**

接下来，让我们学习如何创建和使用作为 CLR 对象的 UDF。

## 创建和使用 UDF

在本节中，您将学习如何在 .NET Framework 中创建作为 CLR 对象的 UDF。为此，您需要在 SQL Server 项目中添加一个 UDF CLR 对象。让我们创建一个名为 `SqlServerProjectUDF`（也可在光盘上找到）的 SQL Server 项目，并向其中添加一个 UDF，即 `RectAreaFunction.cs`。

在 Visual Studio 2010 中执行以下步骤创建 `SqlServerProjectUDF` 项目：

- 1. 打开 `Microsoft Visual Studio 2010`。
- 2. 创建一个名为 `SqlServerProjectUDF` 的 Visual C# SQL CLR 数据库项目。
- 3. 选择现有的数据库连接或创建新的连接。在本例中，我们选择现有的数据库连接 `charu-pc.MyData.dbo`。
- 4. 单击“确定”按钮。`SqlServerProjectUDF` 项目随即显示在 Visual Studio 2010 中。
- 5. 在解决方案资源管理器中右键单击 `SqlServerProjectUDF` 项目，然后选择“添加→用户定义函数”选项。此时会打开“添加新项 - SqlServerProjectUDF”对话框（图 23.19）。
- 6. 选择“用户定义函数”模板，并使用默认名称或输入新名称。在本例中，我们在“名称”文本框中输入名称 `RectAreaFunction.cs`，如图 23.19 所示。

![](img/e073a4882197be4ab61103cbe0bcb394_1162_1.png)

**图 23.19：输入函数名称**

7. 单击“添加”按钮（图 23.19）。`RectAreaFunction.cs` 文件将添加到 `SqlServerProjectUDF` 项目中。

8. 修改 `RectAreaFunction.cs` 文件的代码，如清单 23.12 所示：

### 清单 23.12：显示 `RectAreaFunction.cs` 文件的代码

```
using System;
using System.Data;
using System.Data.SqlClient;
using System.Data.SqlTypes;
using Microsoft.SqlServer.Server;
public partial class UserDefinedFunctions
{
    [Microsoft.SqlServer.Server.SqlFunction]
    public static SqlDecimal RectAreaFunction(decimal RectLength, decimal RectWidth)
    {
        // Put your code here
        return new SqlDecimal(RectLength * RectWidth);
    }
};
```

在清单 23.12 中，我们创建了一个 UDF：`RectAreaFunction`，它带有两个参数 `RectLength` 和 `RectWidth`。参数的数据类型为 `decimal`，函数的返回类型为 `SqlDecimal`。`RectAreaFunction` 函数根据其参数提供的值返回矩形形状的面积。请注意，函数部署需要 `SqlFunction` 特性。

9. 按键盘上的 `Ctrl+Shift+B` 组合键来生成解决方案。

创建作为 CLR 对象的 UDF 之后，您可以直接在 T-SQL 中使用它，也可以在 .NET Framework 4.0 中使用。清单 23.13 显示了创建程序集 `SqlServerProjectUDF` 和函数 `RectAreaFunction` 以调用所创建的 UDF CLR 对象的查询：

### 清单 23.13：创建 `SqlServerProjectUDF` 程序集和 `RectAreaFunction` 函数

```
CREATE ASSEMBLY SqlServerProjectUDF
FROM 'D:\Black Books\C# 2010\Chapter 23\SqlServerProjectUDF\SqlServerProjectUDF\bin\Debug\SqlServerProjectUDF.dll'
GO
Create Function RectAreaFunction
(@RectLength decimal(4,1), @RectWidth decimal(4,1))
RETURNS decimal(8,2)
AS EXTERNAL NAME SqlServerProjectUDF.UserDefinedFunctions.RectAreaFunction
GO
```

在清单 23.13 中，创建了程序集 `SqlServerProjectUDF`。然后，基于 CLR 对象 `RectAreaFunction` 创建了函数 `RectAreaFunction`。

现在，让我们在 SQL 中创建以下 `Papers` 表：

```
CREATE TABLE Papers
(
    PaperID int PRIMARY KEY,
    PaperLength decimal(4,1),
    PaperWidth decimal(4,1),
    PaperArea AS
    (
        dbo.RectAreaFunction(PaperLength, PaperWidth)
    )
)
```

在上面的查询中，您可以看到创建了包含四列（`PaperID`、`PaperLength`、`PaperWidth` 和 `PaperArea`）的 `Papers` 表。`PaperArea` 列存储任何矩形纸张的面积。让我们使用以下查询在 `Papers` 表中插入一些记录：

```
insert Papers values(1,10.0,20.0)
insert Papers values(2,40.0,25.0)
insert Papers values(3,13.0,63.0)
```

在向 `Papers` 表插入值之后，让我们执行以下查询来查看 `Papers` 表的结果集：

```
select * from Papers
```

图 23.20 显示了上述查询的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1164_0.png)

图 23.20：显示 `Papers` 表中存储的数据

接下来，让我们了解如何创建和使用 CLR 对象，即 UDT。

## 创建和使用 UDT

作为 CLR 对象的用户定义对象在 .NET Framework 程序集中作为类实现。该类通过使用 `SqlUserDefinedType` 特性创建，以便将类注册为 UDT。`SqlUserDefinedType` 特性具有以下属性：

- `Format` — 指定类型的格式。它包含两个预定义值：`Format.Native` 和 `Format.UserDefined`。
- `MaxByteSize` — 指定 UDT 的最大大小（以字节为单位）。仅当 `Format` 属性设置为 `UserDefined` 时，才指定此属性。
- `IsByteOrdered` — 指定如何在 SQL 中对 UDT 执行二进制比较。它允许您对绑定此数据类型的列执行各种任务。这些任务的一些示例包括在列上创建索引、创建主键和外键约束，以及将列与 `ORDER BY`、`GROUP BY` 和 `PARTITION BY` 子句一起使用。`IsByteOrdered` 属性的默认值设置为 `false`。
- `ValidationMethodName` — 指定在数据反序列化时验证 UDT 实例的方法名称。
- `IsFixedLength` — 指定 UDT 的所有实例的长度。如果此属性为 `true`，则该数据类型的所有实例的长度（以字节为单位）相同。仅当 `Format` 属性设置为 `UserDefined` 时，才指定此属性。
- `Name` — 表示 UDT 的名称。

让我们学习如何在 .NET Framework 中创建作为 CLR 对象的 UDT。为此，您需要在 SQL Server 项目中添加一个 UDT CLR 对象。让我们创建一个名为 `SqlServerProjectUDT`（也可在光盘上找到）的 SQL Server 项目，并向其中添加一个 UDT，即 `PolygonUDT.cs`。

在 Visual Studio 2010 中执行以下步骤创建 `SqlServerProjectUDT` 项目：

- 1. 打开 `Microsoft Visual Studio 2010`。
- 2. 创建一个名为 `SqlServerProjectUDT` 的 Visual C# SQL CLR 数据库项目。
- 3. 选择现有的数据库连接或创建新的连接。在本例中，我们选择现有的数据库连接 `charu-pc.MyData.dbo`。
- 4. 在解决方案资源管理器中右键单击 `SqlServerProjectUDT` 项目，然后选择“添加→用户定义类型”选项。此时会打开“添加新项 - SqlServerProjectUDT”对话框（图 23.21）。
- 5. 选择“用户定义类型”模板，并使用默认名称或输入新名称。在本例中，我们在“名称”文本框中输入名称 `PolygonUDT.cs`，如图 23.21 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1165_0.png)

# 图 23.21：输入类型名称

6. 单击“添加”按钮。`PolygonUDT.cs` 文件将添加到 `SqlServerProjectUDT` 项目中。

7. 修改 `PolygonUDT.cs` 文件的代码，如清单 23.14 所示：

### 清单 23.14：显示 `PolygonUDT.cs` 文件的代码

```
using System;
using System.Data;
using System.Data.SqlClient;
using System.Data.SqlTypes;
using Microsoft.SqlServer.Server;
[Serializable]
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native)]
public struct PolygonUDT : INullable
{
    private bool isNull;
    private int numberOfSides;
    private double sideLength;
    public override string ToString()
    {
        if (this.isNull)
            return "null";
        else
            return string.Format("{0} sides and the length of each side is {1} units", numberOfSides, sideLength);
    }
    public bool IsNull
    {
        get
        {
            return isNull;
        }
    }
    public static PolygonUDT Null
    {
        get
        {
            PolygonUDT p = new PolygonUDT();
            p.isNull = true;
            return p;
        }
    }
    public static PolygonUDT Parse(SqlString s)
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
this.isNull = false;
}
else
    isNull = true;
}
```

在清单 23.14 中，我们正在创建一个名为 `PolygonUDT` 的 UDT，它被实现为一个结构体，该结构体同时标记有 `Serializable` 属性和 `SqlUserDefinedType` 属性，后者指定了 `Native` 序列化。`PolygonUDT` 类型包含两个私有变量，`numberOfSides` 和 `sideLength`。`NumberOfSides` 和 `SideLength` 属性用于获取和设置这些变量的值。`PolygonUDT` 类型实现了 `INullable` 接口，其 `IsNull()` 方法仅返回一个私有变量 `isNull` 的值，该变量用于跟踪 `PolygonUDT` 类型是否为空。它还实现了 `Null()` 方法，该方法实例化并返回该类型的空实例。接下来，`ToString()` 和 `Parse()` 方法分别用于将多边形的值作为字符串显示以及将字符串转换为 `PolygonUDT` 类型。最后，`PolygonUDT` 类型实现了 `PolygonArea()` 方法用于返回多边形的面积，以及 `UpdateValue()` 方法用于修改多边形的边数和边长的数值。

- 9. 在键盘上按下 `CTRL+SHIFT+B` 键组合来构建解决方案。

在将 UDT 作为 CLR 对象创建之后，您可以直接在 T-SQL 中使用它，也可以在 .NET Framework 4.0 中使用它。清单 23.15 显示了创建程序集 `SqlServerProjectUDT` 和类型 `PolygonUDT` 以调用所创建类型的查询：

## Listing 23.15: Creating the SqlServerProjectUDT Assembly and the PolygonUDT Type

```
CREATE ASSEMBLY SqlServerProjectUDT
FROM 'D:\Black Books\C# 2010\Chapter 23\SqlServerProjectUDT\SqlServerProjectUDT\bin\Debug\SqlServerProjectUDT.dll'
GO
CREATE TYPE PolygonUDT
EXTERNAL NAME SqlServerProjectUDT
```

现在，让我们通过在 SQL Server 2008 中编写以下查询来检查 `PolygonUDT` 类型的使用：

```
DECLARE @plg PolygonUDT
SET @plg = CONVERT(PolygonUDT, '7, 3.1')
PRINT @plg.IsNull
```
