
与其动态等价物。

```csharp
IQueryable query = // ...
query = query.Where("City == @0", "London");
```

动态 Where 方法解析字符串并创建一个强类型的 LINQ 表达式树，该表达式树可被 LINQ 启用数据访问框架使用，例如本示例中的 ADO.NET Entity Framework。以下是使用 LINQ 表达式类实现相同结果的等效代码：

```csharp
IQueryable query = // ...
```

```csharp
ParameterExpression parameter = Expression.Parameter(
    query.ElementType, string.Empty);
Expression property = Expression.PropertyOrField(parameter, "City");
Expression comparison = Expression.Equal(
    property, Expression.Constant("London"));
LambdaExpression lambda = Expression.Lambda(
    comparison, new ParameterExpression[] { parameter });

MethodCallExpression where = Expression.Call(
    typeof(Queryable), "Where",
    new Type[] { query.ElementType },
    new Expression[] { query.Expression, Expression.Quote(lambda) });

query = query.Provider.CreateQuery(where);
```

与原始表达式相比，动态 LINQ 扩展使实现筛选器模板变得容易得多、得多。然而，解析字符串需要在 Web 服务器上消耗额外的 CPU 资源，你可能需要考虑使用 LINQ 表达式实现筛选器模板作为优化。你可能还需要使用 LINQ 表达式，如果动态扩展不支持筛选器模板中需要的 LINQ 功能，例如连接。然而，这个主题过于庞大和复杂，无法在此涵盖；它将在第 12 章“Building Custom Search Pages.”中重新讨论。

## 使用筛选器模板构建搜索页面

现在你已经实现了筛选器模板 Text.ascx，并将其保存在此 Web 项目的 DynamicData/Filters 文件夹中，你可以重写示例搜索页面以利用其功能。将显示此页面新版本的标记的清单 5.5 与显示原始版本的清单 5.1 进行比较。

**清单 5.5** 使用 DynamicFilter 控件的简单搜索页面（标记）

```aspx
<%@ Page Title="" Language="C#"
    MasterPageFile="~/Site.master" CodeBehind="SamplePage.aspx.cs"
    Inherits="WebApplication.Samples.Ch05.DynamicFilter.SamplePage" %>

<asp:Content ContentPlaceHolderID="main" runat="server">
    Customer City:
    <asp:DynamicFilter runat="server" ID="cityFilter"
        DataField="City" FilterUIHint="Text" />
    Title:
    <asp:DynamicFilter runat="server" ID="titleFilter"
        DataField="ContactTitle" FilterUIHint="Text" />
    <asp:Button runat="server" Text="Find" />
    <asp:GridView ID="gridView" runat="server" DataSourceID="dataSource" />
    <asp:EntityDataSource runat="server" ID="dataSource"
        ConnectionString="name=NorthwindEntities"
        DefaultContainerName="NorthwindEntities" EntitySetName="Customers" />
    <asp:QueryExtender runat="server" TargetControlID="dataSource">
        <asp:DynamicFilterExpression ControlID="cityFilter" />
        <asp:DynamicFilterExpression ControlID="titleFilter" />
    </asp:QueryExtender>
</asp:Content>
```

在运行时，此页面的新版本看起来与图 5.1 中显示的原始版本相同。但是，请注意，使用 DynamicFilter 控件代替文本框。DynamicFilter 是 Dynamic Data 提供的新的 ASP.NET 控件。在运行时，它会为 DataField 属性指定的列动态加载适当的筛选器模板。在此页面上，你有两个 DynamicFilter 控件实例，一个用于 City 列，一个用于 ContactTitle。

每个 DynamicFilter 控件最终必须连接到一个基于 LINQ 的数据源控件，该控件查询数据库。在本示例中，使用了 Entity Framework，此页面上有一个 EntityDataSource 控件，已配置为从 Customers 表检索行。EntityDataSource 类从其基类 QueryableDataSource 继承 QueryCreated 事件。控件在创建初始 LINQ 查询（IQueryable 实例）后，但在查询转换为 SQL 并发送到数据库服务器执行之前触发此事件。在此事件期间，查询可以由 DynamicFilter 控件修改。

除了数据源控件之外，页面上还有一个 QueryExtender 控件。此控件通过在查询扩展器的 TargetControlID 属性中指定其 ID 与 QueryableDataSource 关联。在运行时，查询扩展器处理数据源控件的 QueryCreated 并将 IQueryable 实例传递给其每个数据源表达式。此页面使用两个 DynamicFilterExpression 实例将两个 DynamicFilter 控件都与 QueryExtender 关联。每个

代码隐藏只需要将所需的 `MetaTable` 对象与 `GridView` 控件关联。这允许 `DynamicFilter` 控件根据其 `DataField` 属性中指定的列名定位 `MetaColumn` 对象。

### QueryableFilterRepeater 控件

如果需要构建具有特定搜索条件的自定义搜索页面，DynamicFilter 控件是实现筛选功能的正确选择。但是，如果需要构建高级搜索页面，让用户可以使用任何受支持的列搜索数据，或构建可用于不同表的动态搜索页面，你也可以使用 QueryableFilterRepeater 控件。清单 5.7 显示了如何修改搜索页面以利用它。

**清单 5.7** 使用 QueryableFilterRepeater 控件的搜索页面（标记）

```aspx
<%@ Page Title="" Language="C#"
    MasterPageFile="~/Site.master" CodeBehind="SamplePage.aspx.cs"
    Inherits="WebApplication.Samples.Ch05.QueryableFilterRepeater.SamplePage" %>

<asp:Content ContentPlaceHolderID="main" runat="server">
    <asp:QueryableFilterRepeater runat="server" ID="filterRepeater">
        <ItemTemplate>
            <%# Eval("DisplayName") %>:
            <asp:DynamicFilter ID="DynamicFilter" runat="server" />
        </ItemTemplate>
    </asp:QueryableFilterRepeater>
    <asp:Button runat="server" Text="Find" />
    <asp:GridView ID="gridView" runat="server" DataSourceID="dataSource" />
    <asp:EntityDataSource runat="server" ID="dataSource"
        ConnectionString="name=NorthwindEntities"
        DefaultContainerName="NorthwindEntities" EntitySetName="Customers" />
    <asp:QueryExtender runat="server" TargetControlID="dataSource">
        <asp:DynamicFilterExpression ControlID="filterRepeater" />
    </asp:QueryExtender>
</asp:Content>
```

与常规 Repeater 控件类似，QueryableFilterRepeater 使你能够定义一个标记模板，它将使用该模板为表中每个受支持的列生成筛选控件。它定义的每个 ItemTemplate 实例都绑定到一个 MetaColumn 对象，该对象描述了可由 Dynamic Data 筛选的列。这允许你使用 ASP.NET 数据绑定语法 `<%# Eval("DisplayName") %>` 为每个列生成文本标签。在 ItemTemplate 内部，你还需要有一个 ID 属性设置为 "DynamicFilter" 的 DynamicFilter 控件实例。这允许 QueryableFilterRepeater 在每个 ItemTemplate 实例内部找到 DynamicFilter 控件并根据当前 MetaColumn 配置它；QueryableFilterRepeater 将在运行时初始化筛选控件。

**清单 5.8 继续**

```csharp
[FilterUIHint("Text")]
public object City { get; set; }

[FilterUIHint("Text")]
public object ContactTitle { get; set; }
}
}
```

### 筛选器模板查找规则

与字段模板的查找规则相比，筛选器模板的查找规则很简单。Dynamic Data 仅使用与列关联的 FilterUIHint，并对几种列类型具有固有知识。如果在数据模型中未指定 FilterUIHint，并且列是外键（表示子实体中多对一或一对一关联的父导航属性的列）、布尔值或枚举，Dynamic Data 会分别选择预定义的 FilterUIHint 值 ForeignKey、Boolean 或 Enumeration。拥有 FilterUIHint 值后，Dynamic Data 会尝试在 Web 应用程序项目的 DynamicData\Filters 目录中查找名称匹配的用户控件。如果用户控件不存在，查找过程结束，并且认为此列不支持筛选。图 5.4 说明了 Dynamic Data 用于筛选器模板查找的算法。

![](img/11b373b78859e17d318fd76939a0df9d_168_0.png)

**图 5.4** 筛选器模板查找算法。
