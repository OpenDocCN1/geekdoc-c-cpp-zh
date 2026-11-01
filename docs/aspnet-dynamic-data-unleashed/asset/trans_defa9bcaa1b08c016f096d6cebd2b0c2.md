

## 注意

MVC 设计模式不应与 ASP.NET MVC 框架混淆。ASP.NET MVC 框架仅仅是 MVC 模式众多可能实现中的一种。MVC 框架并不比其他实现更优越，也不是利用 MVC 模式好处所必需的。MVC 框架和此处描述的方法只是你可以选择用来解决不同问题的不同工具。

## 摘要

自定义实体模板非常适合在你想为数据模型中的特定实体提供最佳用户界面时实现表单布局。不幸的是，实体模板查找规则与动态实体模板的内置实现相结合，迫使你为每种自定义模板创建至少两个版本，才能在编辑、插入和只读模式下实现特定的表单布局。通过将内置动态实体模板组合到一个多模式的 Default.aspx 模板中，你可以创建支持多种模式的自定义实体模板，并显著减少实现和维护自定义模板所需的工作量。可以创建一个简单的自定义控件 `UnleashedLabel1`，根据元数据信息显示字段标签，避免在自定义实体模板中硬编码这些标签。

自定义字段模板是为特定实体属性（例如 Region 属性，它是存储地址信息的几个属性之一）实现独特展示需求的最佳方式。你可以通过为模板标记中的 DynamicControl 指定自定义属性，以声明方式配置自定义字段模板和通用字段模板的公共属性，也可以编程方式通过处理 DynamicControl 的 Load 事件来配置。

实现字段模板之间交互（例如根据用户输入的国家值筛选地区列表）的最佳位置是在自定义实体模板中。这有助于最大化字段模板的复用，并使长期理解和维护字段模板之间的依赖关系变得更加容易。Dynamic Data 提供的 DynamicControl 和 FieldTemplateUserControl 类的内置实现需要访问各个字段模板的内部实现细节，以确定当前字段值并检测其变化。通过对这些类进行简单扩展，例如示例解决方案中提供的 UnleashedControl 和 UnleashedFieldTemplate，你可以改进字段模板的封装，并更容易地访问字段值。

## 第 11 章：构建动态表单

### 本章内容

- 基本表单布局
- 配置标签外观
- 配置字段模板
- 配置值的外观
- 枚举属性和枚举模板
- 自定义数据类型和 UI 提示
- 指定字段模板参数
- 动态表单中的字段模板交互
- 创建额外的动态实体模板

Dynamic Data 提供的最大优势是极大地减少了应用程序中的代码量。考虑一下，对于 Northwind Traders 示例数据库，一个 Web 应用程序需要多少个 ASPX 文件。如果你使用 WebForms，你可以为每个实体手动创建两个 ASPX 文件——一个用于插入、编辑、显示和删除单行的多用途“表单”页，以及一个用于搜索和浏览所有行的“列表”页。Northwind 数据库中有 11 种不同的实体类型，这意味着必须创建 22 个单独的 ASPX 页面。使用 ASP.NET MVC，你通常会有独立的单一用途视图，每个实体需要五个 ASPX 文件，使 ASPX 文件总数增加到 55 个，比使用 WebForms 手写 ASPX 页面的数量多出一倍以上。而使用 Dynamic Data，它在运行时生成代码，无论实体类型的数量是多少，应用程序只需四个 ASPX 文件（页面模板）即可构建。

只要实体/数据模型的初始版本可用，Dynamic Data 就能为你提供一个可运行的应用程序。你可以立即开始与业务方共享，并收集关于可用网页的反馈，而不是 UML 图或屏幕原型。借助一套良好的动态模板，你可以在快速连续的迭代中细化实体模型并征求更多反馈，而无需维护表示逻辑的负担。如果某个特定实体需要无法动态生成的自定义用户界面，当实体模型稳定后，你可以使用 WebForms 或 MVC 框架手动编写代码。

通过帮助推迟用户界面的手写编码并缩小应用程序的规模，Dynamic Data 帮助你的项目保持敏捷，减少浪费，并使你能够专注于信息系统最重要的方面——其领域模型。毕竟，任何开发项目最大的风险是构建错误的东西。如果你的领域模型是错误的，你的应用程序将是错误的，不管它看起来有多漂亮。这是你可能想要掌握使用 Dynamic Data 进行元数据驱动的 Web 应用程序开发的最重要原因。本章重点介绍如何有效地做到这一点，指出你可能会遇到的一些陷阱和缺陷，并讨论如何解决它们。

### 基本表单布局

创建自定义表单时，你可以通过显式创建表格或其他 HTML 元素来控制其布局。通过为每个属性创建一个 DynamicControl 并将其放置在所需位置，你可以决定哪些实体属性出现在表单上以及它们显示在哪里。

使用默认实体模板时，Dynamic Data 会为任何实体类型生成单列表单，左侧是标签，右侧是数据输入字段。除非你另有指定，否则 Dynamic Data 使用启发式算法来显示它支持的所有合适的属性。具体来说，此列表不包括生成的、自定义的和外键属性。生成的属性（例如映射到 Microsoft SQL Server 数据库中标识列的属性）通常包含不适合向最终用户显示的信息。自定义属性（例如可以在联系人实体类中定义的 FullName 属性，用于连接 FirstName、LastName 和 MiddleInitial 属性）不能用于使用实体框架的 LINQ 筛选，并且会破坏列表页。外键属性（例如 CustomerId）不仅不适合用户直接查看或编辑，而且是导航属性（如 Customer）的一部分，导航属性通常已通过 ForeignKey 字段模板显示。

如果 Dynamic Data 默认选择的显示属性集不满足你的要求，你可以借助 DisplayAttribute 显式显示或隐藏特定属性。下面的代码片段说明了如何显示 Employee 实体的 EmployeeID 属性并隐藏 Orders 属性：

```
[MetadataType(typeof(Metadata))]
partial class Employee
{
    private abstract class Metadata
    {
        [Display(AutoGenerateField = true)]
        public object EmployeeID { get; set; }

        [Display(AutoGenerateField = false)]
        public object Orders { get; set; }
    }
}
```

AutoGenerateField 属性影响 Dynamic Data 生成的单项目表单和列表页。对于列表页，你还可以在 DisplayAttribute 中设置 AutoGenerateFilter 属性，以显式指定 QueryableFilterRepeater 控件是否会为此属性生成 DynamicFilter 控件实例。

### 注意

DisplayAttribute 是你用来控制 ASP.NET Dynamic Data 4.0 或更高版本中动态表单布局和外观的主要数据注解属性。它旨在取代 ASP.NET 3.5 SP1 随附的原始 Dynamic Data 版本使用的多个其他数据注解属性，包括 DisplayNameAttribute、DescriptionAttribute、ScaffoldColumnAttribute 和 ReadOnlyAttribute。这些属性仍然受支持；然而，除了极少数例外，你应该考虑使用 DisplayAttribute，因为它将多个注解合并到一个易于发现的属性类中。

默认情况下，动态表单上属性的显示顺序遵循它们在实体模型中的定义顺序。如果这不符合你的需求，理想情况下你会希望更改实体模型中属性的顺序。如果你使用代码优先方法配合实体框架，这很容易做到。如果你使用模型优先方法，可以通过在文本编辑器中编辑 EDMX 文件中的原始 XML 来完成此操作。如果你使用数据库优先方法，则需要重新排序列在数据库表中的顺序并重新生成模型。通过重新排序实体模型中的属性来控制动态表单上数据输入控件的顺序是理想的做法，因为它消除了歧义并保持了模型的简单性。毕竟，如果你有一个用 HTML 表格布局的自定义表单，你希望将某一行移动到其新位置，使标记中元素的顺序与它们在屏幕上的出现顺序保持同步。同样的想法也适用于控制动态生成表单中控件的顺序。

然而，在现实世界中，你必须处理不太理想的工具和大于理想状态的数据库。当更改实体模型中属性的顺序变得不切实际时，你可以通过设置 DisplayAttribute 的 Order 属性来显式指定。下面是一个示例，演示如何为 Employee 实体的 FirstName 和 LastName 属性执行此操作：

```
[MetadataType(typeof(Metadata))]
partial class Employee
{
    private abstract class Metadata
    {
        [Display(Order = 110)]
        public object FirstName { get; set; }

        [Display(Order = 120)]
        public object LastName { get; set; }
    }
}
```

