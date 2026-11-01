

如你所见，UnleashedMetaModel 类的实现很简单。它的构造函数用 UnleashedFilterFactory 类的新实例替换了内置的 FilterFactory，并重写了 CreateTable 方法以返回 UnleashedMetaTable 的新实例。这确保了 Tables 集合中的所有对象都是 UnleashedMetaModel 类型。剩下要做的就是修改 Web 应用程序的 Global.asax 文件，以使用 UnleashedMetaModel 而不是内置的 MetaModel，如清单 13.4 所示。

### 清单 13.4 修改 Global.asax.cs 以使用 UnleashedMetaModel

```
using System;
using System.Web.DynamicData;
using System.Web.Routing;
using DataModel;

namespace WebApplication
{
    public class Global : System.Web.HttpApplication
    {
        public static UnleashedMetaModel DefaultModel = new UnleashedMetaModel();

        void Application_Start(object sender, EventArgs e)
        {
            var modelConfiguration = new ContextConfiguration{ ScaffoldAllTables = true };
            DefaultModel.RegisterContext(typeof(NorthwindEntities), modelConfiguration);

            RouteTable.Routes.Add(new DynamicDataRoute("{table}/{action}.aspx"));
        }
    }
}
```

图 13.3 展示了产品列表页面在扩展筛选器查找算法下的外观。与图 13.2 中的原始版本相比，您现在可以看到它已经为文本和数字属性提供了筛选项，例如 ProductName 和 UnitsInStock。这些控件是由第 5 章开发的文本筛选器模板生成的。尽管其当前功能仅限于简单的相等性检查，但由于基于回退的算法，动态页面可以在您实现新筛选器模板时自动利用它们，而无需对页面模板本身进行额外修改。

![](img/11b373b78859e17d318fd76939a0df9d_449_0.png)

图 13.3 使用扩展筛选器查找算法的产品列表页面。

尽管使用这种基于约定的算法为所有实体属性自动显示合适的筛选器模板与 Dynamic Data 的整体基架功能更为一致，但它确实改变了其默认行为。以前您必须应用 FilterUIHintAttribute 来启用筛选器生成，现在您必须应用 DisplayAttribute 并将其 AutoGenerateFilter 属性设置为 false 来禁用它。以下是如何防止为 Product 实体的 ProductName 属性生成默认筛选器：

```
[MetadataType(typeof(Metadata))]
partial class Product
{
    private abstract class Metadata
    {
        [Display(AutoGenerateFilter = false)]
        public object ProductName { get; set; }
    }
}
```

### 注意

内置的筛选器基架算法更接近“选择加入”模型，而替换实现的是“选择退出”模型。

## 使用自定义属性构建动态 UI

第 11 章讨论了 Dynamic Data 如何通过在运行时基于元数据信息自动生成相当不错的用户界面，从而允许您快速演化实体模型。这种方法有助于推迟展示代码的实现，同时帮助收集业务用户的反馈，这些用户使用的是真实应用程序，而不仅仅是屏幕原型或图表。

Entity Framework 和 LINQ to SQL 都允许您扩展实体类并定义自定义属性，例如计算属性或从相关实体返回数据的属性。自定义属性是一个强大的工具，允许您超越当前 Entity Framework 和 LINQ to SQL 工具所施加的限制来扩展实体模型。例如，您可以使用名为 Country 的自定义属性扩展 Product 实体类，该属性返回供应商的国家/地区：

```
partial class Product
{
    public string Country { get { return this.Supplier.Country; } }
}
```

定义了自定义属性后，您可以轻松地在产品列表页面上自动生成 Country 列。清单 13.5 显示了一个自定义页面的标记，该页面显示一个 GridView 控件，其中包含 Product 类所有公共属性的纯文本列，包括刚刚定义的自定义 Country 属性。唯一需要的特殊步骤是将 EntityDataSource 控件的 ContextTypeName 属性设置为启用延迟加载（该属性依赖于延迟加载），并将 EnableFlattening 属性设置为 false，这可以防止数据源控件为每个实体对象生成特殊的包装器。实体包装器用于 Entity Framework 的初始版本，该版本不支持外键属性。如今，它们不是必需的，并且只会阻止数据绑定控件（如 GridView）访问实体类中定义的自定义属性。

### 清单 13.5 使用纯文本列显示自定义属性的列表页面

```
<%@Page Language="C#" MasterPageFile="~/Site.master" CodeBehind="SamplePage.aspx.cs" Inherits="WebApplication.Samples.Ch13.CustomProperty.SamplePage" %>
<asp:Content ContentPlaceHolderID="main" runat="server">
    <asp:GridView runat="server" DataSourceID="dataSource" />
    <asp:EntityDataSource runat="server" ID="dataSource"
        ContextTypeName="DataModel.NorthwindEntities"
        EntitySetName="Products" EnableFlattening="False" />
</asp:Content>
```

在 Dynamic Data 中使用自定义属性有助于减少在 Web 应用程序项目中过早创建自定义页面的需求。在某些情况下，自定义属性从实体建模的角度来看是有意义的，使高度规范化的实体模型对开发人员更友好。在其他情况下，与创建新的自定义页面相比，在业务模型中创建自定义属性以实现表示逻辑是一种合理的折衷方案，因为创建新页面几乎肯定会在工作量和代码量方面投入更大。

开箱即用地，Dynamic Data 不允许您利用自定义实体属性。下一节讨论如何克服此限制。

## 实现对自定义属性的支持

第 7 章讨论的 Dynamic Data 元数据 API 确实支持自定义属性。特别是，MetaColumn 类有一个名为 IsCustomProperty 的属性，当列表示的实体属性未在 .EDMX 或 .DBML 文件中定义时，该属性返回 true。然而，问题是 Dynamic Data 不会为自定义属性创建 MetaColumn 对象。图 13.4 显示了 Product 实体的元数据页面截图。请注意，尽管 Country 属性已在类中定义，但右侧的列列表中缺少该属性。

![](img/11b373b78859e17d318fd76939a0df9d_451_0.png)

图 13.4 Product 实体的默认元数据不包含自定义属性。

第 7 章简要提到了 Dynamic Data 依赖元数据提供程序从底层框架（例如 Entity Framework 或 LINQ to SQL）中提取有关实体和属性的信息。自定义属性无法通过元模型 API 使用的原因在于内置提供程序不提供这些属性。通过扩展内置的元数据提供程序，您可以帮助 Dynamic Data 识别

```
public class MetaModel
{
    public void RegisterContext(Type contextType);
    public void RegisterContext(DataModelProvider dataModelProvider);
}
```

为了实现对自定义属性的支持，可以应用装饰器设计模式来创建一组提供程序类，这些类包装原始的 Entity Framework 提供程序对象，并在开箱即用的功能之上提供额外的元数据信息。在示例解决方案中，一个名为 UnleashedColumnProvider 的类封装了自定义实体属性。UnleashedTableProvider 类包装 Dynamic Data 提供的内置 TableProvider 对象，并返回一个 Columns 集合，该集合包含表示 EDMX 文件中定义的属性的 ColumnProvider 对象，以及表示实体模型的分部类中定义的自定义属性的 UnleashedColumnProvider 对象。最后，UnleashedModelProvider 包装一个 DataModelProvider，使您能够用支持自定义属性的扩展提供程序替换受限的内置提供程序。

## 创建自定义属性 ColumnProvider

UnleashedColumnProvider 类继承自内置的 ColumnProvider 类，并封装有关单个自定义属性的元数据。很快您就会看到，当本章进入 UnleashedTableProvider 的实现时，它依赖于 TypeDescriptor API 来提取 .NET 运行时提供的属性元数据。您可能还记得第 7 章的讨论，TypeDescriptor API 定义在 System.ComponentModel 命名空间中。Dynamic Data 和验证框架都依赖 TypeDescriptor，而不是它扩展的低级 .NET Reflection API。

UnleashedColumnProvider 的完整源代码如清单 13.6 所示。尽管 ColumnProvider 基类中的大多数成员都是虚拟的，但它们不必被重写。相反，UnleashedColumnProvider 类的构造函数将 PropertyDescriptor 对象作为其第二个参数，并初始化属性，例如 Name 和 ColumnType。构造函数的第一个参数提供 TableProvider 对象，这是 ColumnProvider 基类中唯一可用的构造函数所要求的。

### 清单 13.6 UnleashedColumnProvider 的实现

```
using System.ComponentModel;
using System.Web.DynamicData.ModelProviders;

namespace WebApplication
{
    public sealed class UnleashedColumnProvider: ColumnProvider
    {
        public UnleashedColumnProvider(
            UnleashedTableProvider table, PropertyDescriptor descriptor)
        : base(table)
```
