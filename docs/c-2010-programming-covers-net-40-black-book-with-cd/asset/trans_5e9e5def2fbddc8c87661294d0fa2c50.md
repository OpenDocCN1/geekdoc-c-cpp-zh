

表 26.20 列出了 `ListView` 类支持的模板：

| Template Type | Description |
|---|---|
| `LayoutTemplate` | 定义一个容器对象，例如表格行 (tr)、div 或 span 元素。这些对象包含在 ItemTemplate 或 GroupTemplate 模板中定义的内容。它还可能包含一个 DataPager 对象。它用于为 ListView 控件的根容器定义自定义 UI。 |
| `ItemTemplate` | 描述用于显示单个项目的绑定数据的外观。 |
| `ItemSeparatorTemplate` | 描述在单个项目之间呈现的内容。 |
| `GroupTemplate` | 描述一个容器对象，例如表格单元格 (td)、div 或 span 元素，其中包含在 ItemTemplate 或 ItemTemplate 模板中定义的内容。在一个组中显示的项目数量由 GroupItemCount 属性指定。它用于在 ListView 控件中创建平铺布局。 |
| `GroupSeparatorTemplate` | 描述在项目组之间呈现的内容。 |
| `EmptyItemTemplate` | 描述在使用 GroupTemplate 模板时为空项目呈现的内容。例如，如果 GroupItemCount 属性设置为 5，并且从数据源返回的总项目数为 8，则 ListView 控件显示的最后一组数据将包含由 ItemTemplate 模板指定的三个项目，以及由 EmptyItemTemplate 模板指定的两个项目。 |
| `EmptyDataTemplate` | 描述如果数据源未返回数据时要呈现的内容。 |
| `SelectedItemTemplate` | 描述为所选数据项呈现的内容，以将其与其它项目区分开。 |
| `AlternatingItemTemplate` | 描述为交替项目呈现的内容，以便更轻松地区分连续项目。 |
| `EditItemTemplate` | 描述在项目正在被编辑时要呈现的内容。EditItemTemplate 模板将替代正在编辑的数据项的 ItemTemplate 模板进行呈现。 |
| `InsertItemTemplate` | 描述插入项目时要呈现的内容。InsertItemTemplate 模板将替代 ListView 控件显示的项目开头或结尾处的 ItemTemplate 模板进行呈现。您可以使用 ListView 控件的 InsertItemPosition 属性指定 InsertItemTemplate 模板的呈现位置。 |

现在，让我们探索 Repeater 控件。

## The Repeater Control

Repeater 控件是一个数据绑定控件，用于从关联的数据源显示重复的项目列表。它是一个单一的 Web 控件，允许在模板之间拆分标记标签。Repeater 控件不提供内置布局或样式支持。因此，在使用 Repeater 控件时，您必须显式声明所有布局、格式和样式。换句话说，Repeater 控件不支持内置的选取或编辑功能。

> **NOTE**
> 
> Repeater 控件与 DataList 控件之间的基本区别在于，后者显式地将项目放置在 HTML 表格中，而前者则不会显式地将项目放置在 HTML 表格中。

Repeater 控件存在于 `System.Web.UI.WebControls` 命名空间中。Repeater 控件的继承层次结构如下：

System.Object
System.Web.UI.Control
System.Web.UI.WebControls.Repeater

Repeater 类的注目属性在表 26.21 中列出：

### Table 26.21: Noteworthy Properties of the Repeater Class

| Property | Description |
|---|---|
| AlternatingItemTemplate | 获取或设置实现 System.Web.UI.ITemplate 命名空间的对象，该对象定义控件中交替项目如何显示 |
| AppRelativeTemplateSourceDirectory | 获取或设置包含此控件的 Page 或 UserControl 对象的应用程序相对虚拟目录。(继承自 Control。) |
| BindingContainer | 基础结构。获取包含此控件数据绑定的控件。(继承自 Control。) |
| ChildControlsCreated | 获取一个值，该值指示服务器控件的子控件是否已创建。(继承自 Control。) |
| ClientID | 获取 ASP.NET 生成的服务器控件标识符。(继承自 Control。) |
| ClientIDSeparator | 获取表示 ClientID 属性中使用的分隔符字符的字符值。(继承自 Control。) |
| Context | 获取与当前 Web 请求关联的服务器控件的 HttpContext 对象。(继承自 Control。) |
| Controls | 获取包含 Repeater 控件子控件的 System.Web.UI.ControlCollection 命名空间 |
| DataMember | 获取或设置在 DataSource 中绑定到 Repeater 控件的特定表 |
| DataSource | 获取或设置提供用于填充列表的数据的数据源 |
| DataSourceID | 获取或设置 Repeater 控件应用于检索其数据源的数据源控件的 ID 属性 |
| DesignMode | 获取一个值，该值指示控件是否正在设计表面上使用。(继承自 Control。) |
| EnableTheming | 获取或设置一个值，该值指示是否将主题应用于此控件。 |
| EnableViewState | 获取或设置一个值，该值指示服务器控件是否将其视图状态以及其包含的任何子控件的视图状态持久保存到请求客户端。(继承自 Control。) |
| Events | 获取控件的事件处理程序委托列表。此属性为只读。(继承自 Control。) |
| FooterTemplate | 获取或设置 System.Web.UI.ITemplate 命名空间，该命名空间定义 Repeater 控件的页脚部分如何显示 |
| HasChildViewState | 获取一个值，该值指示当前服务器控件的子控件是否有任何已保存的视图状态设置。(继承自 Control。) |
| HeaderTemplate | 获取或设置 System.Web.UI.ITemplate，该模板定义 Repeater 控件的页眉部分如何显示 |
| ID | 获取或设置分配给服务器控件的程序标识符。(继承自 Control。) |
| IdSeparator | 获取用于分隔控件标识符的字符。(继承自 Control。) |
| Initialized | 返回一个值，该值指示控件是否已初始化。 |
| IsBoundUsingDataSourceID | 获取一个值，该值指示 DataSourceID 属性是否已设置。 |
| IsChildControlStateCleared | 获取一个值，该值指示此控件中包含的控件是否有控件状态。(继承自 Control。) |
| IsTrackingViewState | 获取一个值，该值指示服务器控件是否正在保存其视图状态的更改。(继承自 Control。) |
| IsViewStateEnabled | 获取一个值，该值指示此控件是否启用了视图状态。(继承自 Control。) |
| Items | 获取 Repeater 控件中 RepeaterItem 对象的集合 |
| ItemTemplate | 获取或设置 System.Web.UI.ITemplate 命名空间，该命名空间定义 Repeater 控件中项目如何显示 |
| LoadViewStateByID | 获取一个值，该值指示控件是否参与通过 ID 而不是索引加载其视图状态。(继承自 Control。) |
| Page | 获取包含服务器控件的 Page 实例的引用。(继承自 Control。) |
| Parent | 获取对页面控件层次结构中服务器控件父控件的引用。(继承自 Control。) |
| RequiresDataBinding | 获取或设置一个值，该值指示 Repeater 控件是否需要绑定到其指定的数据源。 |
| SelectArguments | 获取 DataSourceSelectArguments 对象，Repeater 控件在从数据源控件检索数据时使用该对象。 |
| SeparatorTemplate | 获取或设置 System.Web.UI.ITemplate 命名空间，该命名空间定义项目之间分隔符如何显示 |

Repeater 类的注目事件在表 26.22 中列出：

### Table 26.22: Noteworthy Events of the Repeater Class

| Event | Description |
|---|---|
| ItemCommand | 在 Repeater 控件中单击按钮时调用 |
| ItemCreated | 在 Repeater 控件中创建项目时调用 |
| ItemDataBound | 在 Repeater 控件中的项目数据绑定后，但在页面上呈现之前调用 |

现在，让我们了解 DataPager 控件。

## The DataPager Control

DataPager 控件用于为数据绑定控件（例如 ListView 控件）提供分页功能。当您将 DataPager 控件拖到页面上时，以下代码会出现在页面的源视图中：

```
<asp:DataPager ID="DataPager1" runat="server"> </asp:DataPager>
```

DataPager 控件的继承层次结构如下：

