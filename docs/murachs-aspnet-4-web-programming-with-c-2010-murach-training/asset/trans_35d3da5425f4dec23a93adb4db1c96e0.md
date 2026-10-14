

# 对象数据源简介

以下主题将向你介绍对象数据源及其支持实现的三层架构。

## 三层应用程序在 ASP.NET 中的工作原理

你可能知道，大多数开发专家建议 Web 应用程序采用三层架构，将应用程序的表示层、业务规则和数据访问组件分开。表示层包含定义用户界面的网页。中间层包括管理这些页面的数据访问的类，也可能包含实现业务规则（如数据验证要求或折扣策略）的类。数据库层由数据库本身组成。

在本章中，你将学习如何使用对象数据源来实现三层架构。图 17-1 展示了它的工作方式。此处可以看到，ObjectDataSource 控件充当表示层中数据绑定控件与中间层中数据访问类之间的接口。

使用 ObjectDataSource 控件时，必须创建一个数据访问类来处理该控件的数据访问。此类至少提供一个方法，用于从数据库检索数据并以 ObjectDataSource 控件可以处理的形式返回。它还可以提供插入、更新和删除数据的方法。数据访问类应放在应用程序的 App_Code 文件夹中。

在编写数据访问类时，你可以使用任何想要的技术来访问数据库。例如，在本章中，你将看到使用 ADO.NET 的数据访问类。这些类可用于从 SQL Server 数据库、其他类型的数据库（如 Oracle 或 MySQL 数据库）或其他数据源（如 XML 或纯文本文件）获取数据。

如果你已经为应用程序使用的数据库开发了数据访问类，或许可以将这些类用于对象数据源。不过，通常最好是针对你将要使用的 ObjectDataSource 控件专门开发数据访问类。这样，你可以设计每个类，使其尽可能高效地工作。

顺便提一下，Microsoft 使用“业务对象类”和“数据对象类”这两个术语来指代为对象数据源提供数据访问的类。不过，在本章中，我使用“数据访问类”这一术语来指代此类，因为如果你使用静态方法提供数据访问功能，则永远不会从该类实例化对象。

## ASP.NET 中的三层架构

![](img/c024ccf88e28c30c07dd410d4342288f_586_0.png)

### 三层

- **表示层**由管理应用程序外观的 ASP.NET 页面组成。此层可以包含绑定数据控件和 ObjectDataSource 对象，这些控件和对象将数据控件绑定到数据。
- **中间层**包含管理应用程序数据访问的*数据访问类*。此层还可以包含业务对象，这些对象表示客户、产品或员工等业务实体，并实现信用和折扣策略等业务规则。
- **数据库层**由包含应用程序数据的数据库组成。理想情况下，执行数据库访问的 SQL 语句应保存在数据库内的存储过程中，但 SQL 语句通常存储在数据访问类中。

### 说明

- *对象数据源*由 ObjectDataSource 控件实现，它允许你在数据库应用程序中使用*三层架构*进行数据绑定。
- 对象数据源与 SQL 数据源类似。但是，对象数据源不是直接访问数据库，而是通过处理数据库访问细节的数据访问类获取数据。

另外，你可能习惯于用*三层体系结构*来指代图 17-1 中描述的*三层架构*。不过，因为有些人使用*三层体系结构*来指代将三个层分别放在三台不同物理设备上的架构，所以我在本章中使用了*三层架构*这一术语。虽然你可以将三个层分别放置在三台设备上，但并非必须如此。

## 如何使用 ObjectDataSource 控件

图 17-2 介绍了使用 ObjectDataSource 控件的基础知识。此图顶部的图像显示了绑定到下拉列表的 ObjectDataSource 控件在 Web Forms 设计器中的外观。然后，第一个代码示例显示了下拉列表及其所绑定对象数据源的 aspx 代码。与任何其他数据源一样，你可以通过从工具箱中拖动对象数据源，或从可绑定控件中选择“选择数据源”命令，将对象数据源添加到网页中。

在第一个代码示例中，你可以看到下拉列表绑定到对象数据源的方式与绑定到 SQL 数据源的方式完全相同。唯一的区别是 DataSourceID 属性提供的是对象数据源的 ID，而不是 SQL 数据源的 ID。你还可以看到，ObjectDataSource 控件的代码除了必需的 ID 和 runat 属性之外，只有两个属性。TypeName 属性提供数据访问类的名称，SelectMethod 属性提供用于检索数据的方法名称。在本例中，数据访问类是 ProductDB，选择方法是 GetAllCategories。

此图中的第二个代码示例展示了 ProductDB 类的 GetAllCategories 方法。该方法使用直接的 ADO.NET 代码从 Categories 表检索类别行，并返回一个可用于读取这些类别行的数据读取器。但请注意，此方法的返回类型是 IEnumerable。因为 SqlDataReader 类实现了 IEnumerable 接口，所以数据读取器是该方法的有效返回对象。（你将在图 17-8 中详细了解 select 方法可接受的返回类型。）

### 绑定到 ObjectDataSource 控件的下拉列表

![](img/c024ccf88e28c30c07dd410d4342288f_588_0.png)

### 下拉列表和 ObjectDataSource 控件的代码

```
<asp:DropDownList ID="ddlCategories" runat="server" AutoPostBack="True"
    DataSourceID="ObjectDataSource1"
    DataTextField="ShortName"
    DataValueField="CategoryID">
</asp:DropDownList>
<asp:ObjectDataSource ID="ObjectDataSource1" runat="server"
    TypeName="ProductDB"
    SelectMethod="GetAllCategories">
</asp:ObjectDataSource>
```

### ProductDB 类的 GetAllCategories 方法

```
[DataObjectMethod(DataObjectMethodType.Select)]
public static IEnumerable GetAllCategories()
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string sel = "SELECT CategoryID, LongName "
        + "FROM Categories ORDER BY LongName";
    SqlCommand cmd = new SqlCommand(sel, con);
    con.Open();
    SqlDataReader dr = cmd.ExecuteReader(CommandBehavior.CloseConnection);
    return dr;
}
```

### ObjectDataSource 控件的基本属性

| 属性 | 描述 |
|---|---|
| ID | 控件的 ID。 |
| Runat | 必须指定为 "server"。 |
| TypeName | 数据访问类的名称。 |
| SelectMethod | 检索数据的方法的名称。 |
| UpdateMethod | 更新数据的方法的名称。 |
| DeleteMethod | 删除数据的方法的名称。 |
| InsertMethod | 插入数据的方法的名称。 |
| DataObjectTypeName | 提供属性以用于传递参数值的类的名称。 |
| ConflictDetection | 指定如何检测并发冲突。CompareAllValues 使用乐观并发检查。OverwriteValues（默认值）不执行并发检查。 |

### 说明

- ObjectDataSource 控件指定数据访问类的名称以及用于选择、更新、删除和插入数据的方法。

