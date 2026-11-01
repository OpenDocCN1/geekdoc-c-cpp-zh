
```
RouteTable.Routes.Add(new DynamicDataRoute("Product")
{
    Action = PageAction.Details,
    Table = "Products"
});
```

基于此路由定义，Dynamic Data Web 应用程序可以使用以下 URL：

http://localhost/Product?ProductID=1

而不必使用如下更冗长且不够友好的 URL：

http://localhost/Products/Details.aspx?ProductID=1

## URL 参数与查询参数

URL 参数可替代传统 ASP.NET WebForms 应用程序使用的查询参数。传统的查询参数要求在查询字符串中同时提供名称和值，而 URL 参数允许 Web 应用程序根据值在 URL 中的位置自动确定参数名称。请考虑以下路由，它使用位置型 URL 参数替代 ProductID 查询参数：

```
RouteTable.Routes.Add(new DynamicDataRoute("Product/{ProductID}")
{
    Action = PageAction.Details,
    Table = "Products"
});
```

此路由定义允许 Web 应用程序在不使用查询参数的情况下实现产品目录，并支持类似于下面所示的 URL。这不仅使 URL 更短、更易于用户阅读，也使搜索引擎更容易索引动态页面，这一点对于面向公众的网站非常重要：

http://localhost:49212/Product/3

Dynamic Data 仍然支持传统的查询参数，你可以通过注册一个不包含任何 URL 参数、也不显式指定参数值的路由来启用这些参数：

```
RouteTable.Routes.Add(new DynamicDataRoute("Dynamic"));
```

刚才注册的路由会让 Dynamic Data 改为使用如下形式的 URL：

http://localhost/Dynamic?Table=Products&Action=List

## 动态超链接

路由具有双重用途。除了帮助 ASP.NET 运行时确定哪个 ASPX 页面将用于处理特定的传入请求之外，它们还决定指向动态页面的超链接将如何生成。在 ASP.NET Web 应用程序中，有几种不同的方法可以生成超链接。其中一种方法使用 Dynamic Data 提供的 DynamicHyperLink 控件。该控件继承自 ASP.NET HyperLink 控件，允许你生成指向动态页面的超链接。在以下示例中，显式指定了表名和所需操作。

```aspx
<asp:DynamicHyperLink runat="server"
    ContextTypeName="DataModel.NorthwindEntities"
    TableName="Products" Action="List" Text="Show all" />
```

TableName 属性指定描述目标实体的 MetaTable 的名称，ContextTypeName 指定目标实体所在的上下文类的名称。根据路由配置方式的不同，该控件会生成不同的 URL，而无需你修改其任何标记。表 6.1 展示了不同的路由定义以及该控件基于这些定义生成的 URL 示例。

表 6.1 DynamicHyperLink 生成的 URL 示例

| 路由定义 | URL 示例 |
|---|---|
| `new DynamicDataRoute("{table}/{action}.aspx")` | `http://localhost/Products/List.aspx` |
| `new DynamicDataRoute("{table}/{action}")` | `http://localhost/Products/List` |
| `new DynamicDataRoute("{table}") { Action = PageAction.List };` | `http://localhost/Products` |

DynamicHyperLink 控件还可以数据绑定到实体实例，在这种情况下，它可以自动确定 ContextTypeName 和 TableName，并生成在地址的查询部分中包含主键列名称和值的 URL。前面讨论过的 Details 页面模板利用了这一功能，将 DynamicHyperLink 控件作为 FormView 控件中 ItemTemplate 的一部分，如下面的摘录所示：

```aspx
<asp:FormView runat="server" ID="formView" DataSourceID="dataSource">
    <ItemTemplate>
        <asp:DynamicEntity runat="server" />
        <div class="DDFormActions">
            <asp:DynamicHyperLink runat="server" Action="Edit" Text="Edit" />
            <asp:DynamicHyperLink runat="server" Action="Delete" Text="Delete" />
            <asp:DynamicHyperLink runat="server" Action="List" Text="Show all"/>
```

```html
</div>
</ItemTemplate>
</asp:FormView>
```

请注意，此示例中的 DynamicHyperLink 控件并未指定 ContextTypeName 和 TableName 属性。FormView 控件将其 ItemTemplate 数据绑定到关联的 EntityDataSource 控件提供的实体实例上。这些控件根据实体类型定位 MetaTable 对象，并生成如下所示形式的 URL：

```text
http://localhost/Products/Edit.aspx?ProductID=1
http://localhost/Products/Details.aspx?ProductID=1
http://localhost/Products/List.aspx?ProductID=1
```

借助 RouteUrl 标记表达式，也可以生成动态超链接。这是一种特殊的语法，ASP.NET 解析器会识别它，并根据你指定的参数值生成动态 URL：

```aspx
<asp:HyperLink runat="server" Text="Show all"
    NavigateUrl="<%$RouteUrl:table=Products, action=List%>" />
```

在底层，RouteUrl 标记表达式和 DynamicHyperLink 控件都依赖 ASP.NET 提供的用于路由的底层 API。下一个代码示例演示了它们如何通过编程方式创建动态超链接。它创建一个 RouteValueDictionary 来保存 Table 和 Action 参数值，然后调用全局 Routes 集合的 GetVirtualPath 方法，以虚拟路径的形式生成 URL：

```csharp
HyperLink hyperLink = // ...

RequestContext context =
    DynamicDataRouteHandler.GetRequestContext(HttpContext.Current);

RouteValueDictionary routeValues = new RouteValueDictionary();
routeValues["table"] = "Products";
routeValues["action"] = "List";

VirtualPathData pathData = RouteTable.Routes.GetVirtualPath(
    context, routeValues);

hyperLink.NavigateUrl = pathData.VirtualPath;
```

## 路由评估与约束

虽然你可能永远不需要编写代码以编程方式创建动态超链接，但了解 ASP.NET 运行时如何生成它们仍然很重要。尤其要注意，用于生成动态 URL 的是 Routes 集合，而不是某一个特定的路由对象。这一点很重要，因为 Routes 集合会按照路由注册的顺序逐一评估，查找与所提供参数值集合匹配的路由。一旦找到匹配项，就停止进一步评估，并使用匹配的路由生成 URL。

当 ASP.NET 运行时需要找到用于处理传入 Web 请求的页面模板时，也会发生类似的评估过程。它会从最先注册的路由开始，依次向下查找，直到找到第一个匹配项。在第一个匹配项之后注册的所有其他路由都将被忽略。

考虑到路由评估过程的工作原理，应首先注册最具体的路由，将更一般的路由留到最后。例如，如果你按以下顺序注册了两个路由，那么 Web 应用程序在生成动态超链接时将始终忽略第二个路由：

```csharp
RouteTable.Routes.Add(new DynamicDataRoute("{table}/{action}.aspx"));
RouteTable.Routes.Add(new DynamicDataRoute("{table}")
{
    Action = PageAction.List
});
```

换句话说，指向产品列表的超链接将始终以 http://localhost/Products/List.aspx 形式呈现给用户，而绝不会是 http://localhost/Products。然而，在处理传入请求时，第二个 URL 不会匹配第一个路由，因此会“穿透”（fall through）并仍被第二个路由捕获。

更改路由注册的顺序可以在很大程度上控制 URL 解析过程。然而，当这还不够时，你可以使用路由约束使其更加具体。路由约束在路由对象的 Constraints 字典中定义为两个字符串值的配对，第一个是参数名称，第二个是参数值必须匹配的正则表达式模式。以下示例定义了一个路由，其中 table 参数值既可以是 Products 也可以是 Orders：

```csharp
RouteTable.Routes.Add(new DynamicDataRoute("{table}")
{
    Action = PageAction.List,
    Constraints = new RouteValueDictionary(){{"table","Products|Orders"}}
});
RouteTable.Routes.Add(new DynamicDataRoute("{table}/{action}.aspx"));
```

基于最后一个示例中的路由定义，只有 Products 和 Orders 表的 List URL 会生成为 http://localhost/Products 或 http://localhost/Orders。所有其他表将使用第二个路由，并具有类似于 http://localhost/Suppliers/List.aspx 的 URL。

