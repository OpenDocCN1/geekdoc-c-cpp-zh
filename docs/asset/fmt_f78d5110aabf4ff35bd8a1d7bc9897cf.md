
+   14. 按键盘上的 `F5` 键执行应用程序。输出显示在图 26.19 中：

![](img/e073a4882197be4ab61103cbe0bcb394_1309_0.png)

### 图 26.19：显示 AccessDataSource 应用程序的输出

# 使用 LinqDataSource 控件

让我们通过执行以下步骤创建一个 LinqDataSource 应用程序以在 Web 页面上显示数据：

+   1. 创建一个 Web 应用程序并将其保存为 LinqDataSourceControl（可在 CD 上获得）。

2. 在解决方案资源管理器中右键单击应用程序名称并从上下文菜单中选择“添加新项”选项。

“添加新项”对话框出现（图 26.20）。

3. 将 LINQ to SQL 类文件（`DataClasses.dbml`）添加到项目中，如图 26.20 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1310_0.png)

图 26.20：添加 LINQ to SQL 类

现在，Microsoft Visual Studio 消息框出现（图 26.21）。

4. 单击“是”按钮以将 LINQ to SQL 类添加到 `App_Code` 文件夹中，如图 26.21 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1310_1.png)

图 26.21：将类添加到 `App_Code` 文件夹

5. 打开服务器资源管理器并右键单击“数据连接”以创建与 `northwind` 数据库的连接（图 26.22）。

6. 从上下文菜单中选择“添加连接”，如图 26.22 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1310_2.png)

图 26.22：创建连接

“添加连接”对话框出现。

7. 通过提供服务器名称和数据库名称，如 `SqlDataSource` 应用程序中完成的那样，创建连接。

现在，`northwnd` 数据库中存在的表将出现在服务器资源管理器的“表”节点中（图 26.23）。

8. 将 `Products` 表拖放到 `DataClasses.dbml` 文件的设计图面上。生成的 `DataClasses.dbml` 如图 26.23 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1311_0.png)

图 26.23：选择 `Products` 表

9. 将 `LinqDataSource` 控件拖放到 Web 页面上，并从其智能标记中选择“配置数据源”选项，如图 26.24 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1311_1.png)

图 26.24：添加 `LinqDataSource` 控件

此时，将显示“配置数据源”向导（图 26.25）。

10. 在“配置数据源”向导的“选择上下文对象”页面中单击“下一步”按钮，如图 26.25 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1312_0.png)

图 26.25：选择上下文对象

此时，向导中将显示“配置数据选择”页面（图 26.26）。

- 11. 选择 `Products` 表中要在 `GridView` 中显示的列。在本应用程序中，我们选择了 `ProductID`、`ProductName`、`QuantityPerUnit`、`UnitPrice` 和 `UnitsInStock`（图 26.26）。
- 12. 单击“完成”按钮，如图 26.26 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1312_1.png)

图 26.26：选择表的列

- 13. 从“生成”主菜单中选择“生成解决方案”选项来生成应用程序。
- 14. 将 `GridView` 控件拖放到 `Default.aspx` 页面的设计视图上（图 26.27）。

## 第 26 章：ASP.NET 应用程序中的数据绑定

15. 在“`GridView` 任务”中，从“选择数据源”下拉列表中选择“`LinqDataSource1`”选项，如图 26.27 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1313_0.png)

图 26.27：选择数据源

配置数据源后，`LinqDataSource` 应用程序的 `Default.aspx` 页面如清单 26.3 所示：

### 清单 26.3：Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">

<head runat="server">
    <title></title>
</head>

<body>
    <form id="form1" runat="server">
        <div>
            <asp:LinqDataSource ID="LinqDataSource1" runat="server" ContextTypeName="DataClassesDataContext" EntityTypeName="" Select="new (ProductID, ProductName, QuantityPerUnit, UnitPrice, TableName=\"Products\")">
            </asp:LinqDataSource>
        </div>
        <asp:GridView ID="GridView1" runat="server" DataSourceID="LinqDataSource1" AutoGenerateColumns="False">
            <Columns>
                <asp:BoundField DataField="ProductID" HeaderText="ProductID" ReadOnly="True" SortExpression="ProductID" />
                <asp:BoundField DataField="ProductName" HeaderText="ProductName" ReadOnly="True" SortExpression="ProductName" />
                <asp:BoundField DataField="QuantityPerUnit" HeaderText="QuantityPerUnit" ReadOnly="True" SortExpression="QuantityPerUnit" />
                <asp:BoundField DataField="UnitPrice" HeaderText="UnitPrice" ReadOnly="True"
```
```
SortExpression="UnitPrice" />
<asp:BoundField DataField="UnitsInStock" HeaderText="UnitsInStock" Readonly="True" SortExpression="UnitsInStock" />
</Columns>
</asp:GridView>
</form>
</body>
</html>
```

16. 按键盘上的 `F5` 键运行应用程序。输出如图 26.28 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1314_0.png)

图 26.28：显示输出

### 使用 ObjectDataSource 控件

现在，让我们通过执行以下步骤来了解如何使用 `ObjectDataSource` 控件：

- 1. 创建一个 Web 应用程序并将其命名为 `ObjectDataSource`（可从随书光盘中获取）。
- 2. 向项目中添加一个类文件，并用清单 26.4 中显示的代码替换 `ClassProduct.cs` 文件的代码：

### 清单 26.4：显示类文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data;
using System.Data.SqlClient;

/// <summary>
/// Summary description for ClassProduct
/// </summary>
public class ClassProduct
{
    public DataSet getinfo()
    {
        SqlConnection con = new SqlConnection ("Data Source=PUNEET-PC\SQLEXPRESS;Initial Catalog=northwnd;Integrated Security=True");
        SqlDataAdapter da = new SqlDataAdapter ("Select * from Products", con);
        DataSet ds = new DataSet();
```

此时，“配置数据源”向导中将显示“定义数据方法”页面（图 26.31）。

6. 从“选择方法”下拉列表中选择方法名称，并单击“完成”按钮，如图 26.31 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1316_0.png)

图 26.31：选择方法

7. 将 `GridView` 控件拖放到 `Default.aspx` 页面的设计视图上（图 26.32）。

8. 从“选择数据源”下拉列表中选择 `ObjectDataSource1`，如图 26.32 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1316_1.png)

图 26.32：选择数据源

配置数据源后，`ObjectDataSource` 应用程序的 `Default.aspx` 页面如清单 26.5 所示：

### 清单 26.5：Default.aspx 页面的代码

```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <asp:ObjectDataSource ID="ObjectDataSource1" runat="server"
            SelectMethod="getinfo" TypeName="ClassProduct"></asp:ObjectDataSource>
        <div>
        </div>
        <asp:GridView ID="GridView1" runat="server" DataSourceID="ObjectDataSource1">
        </asp:GridView>
    </form>
</body>
</html>
```

9. 按键盘上的 `F5` 键运行应用程序。输出如图 26.33 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1317_0.png)

图 26.33：显示输出

### 使用 XmlDataSource 控件

现在，让我们通过执行以下步骤来了解如何使用 `XmlDataSource` 控件将数据绑定到 `GridView` 控件：

- 1. 创建一个 Web 应用程序并将其命名为 `XmlDataSource`（可从随书光盘中获取）。
- 2. 在解决方案资源管理器的 `App_Data` 文件夹中添加一个 XML 文件。在 `XMLFile.xml` 文件中添加以下代码：

```xml
<student>
    <student Name="John" RollNo="A001" Standard="X"/>
    <student Name="David" RollNo="A002" Standard="XI"/>
    <student Name="Lisa" RollNo="A003" Standard="XII"/>
</student>
```

3. 拖放 `XmlDataSource` 控件并单击智能标记（图 26.34）。
4. 单击智能标记并选择“配置数据源”选项，如图 26.34 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1318_0.png)

图 26.34：配置数据源

此时，将显示“配置数据源”向导（图 26.35）。

5. 单击“浏览”按钮添加 XML 文件，如图 26.35 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1318_1.png)

图 26.35：浏览数据源

此时，将显示“选择 XML 文件”对话框（图 26.36）。

6. 从“文件夹内容”窗格中选择 `XMLFile.xml` 文件，并单击“确定”按钮，如图 26.36 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1319_0.png)

图 26.36：选择 XML 文件

此时，XML 文件的路径将出现在“数据文件”文本框中（图 26.37）。

7. 在“配置数据源”向导中单击“确定”按钮，如图 26.37 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1319_1.png)

图 26.37：保存 XML 文件的路径

8. 将 `GridView` 控件拖放到 `Default.aspx` 页面的设计视图上（图 26.38）。

9. 从“选择数据源”下拉列表中选择 `XmlDataSource1`，如图 26.38 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1320_0.png)

配置数据源后，`XmlDataSource` 应用程序的 `Default.aspx` 页面如清单 26.6 所示：

## 清单 26.6：展示 Default.aspx 页面的代码

```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
        </div>
        <asp:XmlDataSource ID="xmldataSource1" runat="server"
            DataFile="~/App_Data/XMLFile.xml"></asp:XmlDataSource>
        <asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False"
            DataSourceID="xmldataSource1">
            <Columns>
                <asp:BoundField DataField="Name" HeaderText="Name" SortExpression="Name" />
                <asp:BoundField DataField="RollNo" HeaderText="RollNo"
                    SortExpression="RollNo" />
                <asp:BoundField DataField="Standard" HeaderText="Standard"
                    SortExpression="Standard" />
            </Columns>
        </asp:GridView>
    </form>
</body>
</html>
```
