
| 使用 ListView 和 DataPager 控件 | 164 |
| 使用 Chart 控件 | 169 |
| 使用 Query/Extender 控件 | 171 |

# 第22章：ASP.NET 中的数据绑定

## 深入解析

数据库是记录或信息的集合，以系统化的方式以表格的形式存储，以便计算机程序轻松访问所需的信息。结构化查询语言 (`SQL`) 用于检索、存储和更新记录。应用程序可能需要使用数据库来执行某些功能，例如：

- 从数据库检索记录并以表格格式显示数据
- 在处理数据库的记录后显示数据，例如计算每条记录的持续时间然后显示记录
- 处理检索到的数据并在数据库中更新
- 根据用户指定的选择从数据库中删除记录

在本章中，你将学习 `ASP.NET` 支持的各种数据源和绑定控件。绑定控件是复合控件。如下：

- `GridView` 控件
- `DataList` 控件
- `DetailsView` 控件
- `FormView` 控件
- `Repeater` 控件
- `DataPager` 控件
- `Chart` 控件
- `Query/Extender` 控件
- `SqlDataSource` 控件
- `LinkDataSource` 控件
- `ObjectDataSource` 控件
- `XmlDataDataSource` 控件
- `EntityDataSource` 控件

`ASP.NET` 支持

数据库是记录或信息的集合，以系统化的方式以表格的形式存储，以便计算机程序轻松访问所需的信息。结构化查询语言 (`SQL`) 用于检索、存储和更新记录。应用程序可能需要使用数据库来执行某些功能，例如：

- 从数据库检索记录并以表格格式显示数据
- 在处理数据库的记录后显示数据，例如计算每条记录的持续时间然后显示记录
- 处理检索到的数据并在数据库中更新
- 根据用户指定的选择从数据库中删除记录

在本章中，你将学习 `ASP.NET` 支持的各种数据源和绑定控件。绑定控件是复合控件。如下：

- `GridView` 控件
- `DataList` 控件
- `DetailsView` 控件
- `FormView` 控件
- `Repeater` 控件
- `DataPager` 控件
- `Chart` 控件
- `Query/Extender` 控件
- `SqlDataSource` 控件
- `LinkDataSource` 控件
- `ObjectDataSource` 控件
- `XmlDataDataSource` 控件
- `EntityDataSource` 控件

## WPF 数据绑定概念

本章还解释了 `WPF` 的数据绑定概念。接着，你学习了不同的数据绑定源、数据绑定声明以及向集合绑定数据。最后，你学习了如何使用 `WCF` 数据服务绑定 `SQL` 数据。这些概念的实际实现涵盖在本章的“瞬时解决方案”部分。

在下一章中，你将学习 `ASP.NET` 中的数据绑定。

## ASP.NET 中的数据绑定

| 如果你需要针对以下内容的瞬时解决方案： | 参见页码： |
| :--- | :--- |
| 使用 `SqlDataSource` 控件 | 129 |
| 使用 `LinqDataSource` 控件 | 135 |
| 使用 `ObjectDataSource` 控件 | 139 |
| 使用 `XmlDataDataSource` 控件 | 142 |
| 使用 `EntityDataSource` 控件 | 145 |
| 使用 `GridView` 控件 | 150 |
| 使用 `DataList` 控件 | 154 |
| 使用 `DetailsView` 控件 | 157 |
| 使用 `FormView` 控件 | 159 |
| 使用 `Repeater` 控件 | 162 |
| 使用 `ListView` 和 `DataPager` 控件 | 164 |
| 使用 `Chart` 控件 | 169 |
| 使用 `Query/Extender` 控件 | 171 |

# 第22章：ASP.NET 中的数据绑定

## 深入解析

数据库是记录或信息的集合，以系统化的方式以表格的形式存储，以便计算机程序轻松访问所需的信息。结构化查询语言 (`SQL`) 用于检索、存储和更新记录。应用程序可能需要使用数据库来执行某些功能，例如：

- 从数据库检索记录并以表格格式显示数据
- 在处理数据库的记录后显示数据，例如计算每条记录的持续时间然后显示记录
- 处理检索到的数据并在数据库中更新
- 根据用户指定的选择从数据库中删除记录

# 第22章：ASP.NET 中的数据绑定

| 表 22.3：`GridView` 类的重要属性 |
| 属性 | 描述 |
| --- | --- |
| `AutoGenerateEditButton` | 获取或设置一个值，指示是否自动为 `GridView` 控件添加一个每行都有编辑按钮的 `CommandField` 列。 |
| `AutoGenerateSelectButton` | 获取或设置一个值，指示是否自动为 `GridView` 控件添加一个每行都有选择按钮的 `CommandField` 列。 |
| `BackImageUrl` | 获取或设置显示在 `GridView` 控件背景中的 URL。 |
| `BottomPagerRow` | 获取一个表示 `GridView` 控件中底部分页器行的行的 `GridViewRow` 对象。 |
| `Caption` | 获取或设置 `GridView` 控件中 HTML `caption` 元素中的文本。提供此属性是为了让辅助技术设备的用户更方便地访问该控件。 |
| `CaptionAlign` | 获取或设置 `GridView` 控件中 HTML `caption` 元素的水平或垂直位置。提供此属性是为了让辅助技术设备的用户更方便地访问该控件。 |
| `CellPadding` | 获取或设置单元格内容与单元格边界之间的空间量。 |
| `CellSpacing` | 获取或设置单元格之间的空间量。 |
| `Columns` | 获取一个 `DataColumn` 对象集合，代表 `GridView` 控件中的列字段。 |
| `DataKeys` | 获取或设置一个数组，该数组包含 `GridView` 控件中显示的数据项的主键字段。 |
| `DataKeys` | 获取一个 `DataKey` 对象集合，代表 `GridView` 控件中每行的数据值。 |
| `EditIndex` | 获取或设置要编辑的行的索引。 |
| `EditStyle` | 获取 `TableItem` 对象的引用，使我们能够设置 `GridView` 控件中被选中用于编辑的外观。 |
| `EmptyDataRow` | 获取或设置 `TableItem` 对象，使我们能够设置当 `GridView` 绑定到不包含任何行的数据源时渲染的空行的外观。 |
| `EmptyDataTemplate` | 获取或设置用户定义的内容，用于 `GridView` 绑定到不包含任何行的数据源时渲染的空行显示。 |
| `EmptyDataText` | 获取或设置文本，在 `GridView` 绑定到不包含任何行的数据源时渲染的空行中显示。 |
| `EnablingSortingAndPagination` | 获取或设置一个值，指示是否使用客户端控件进行排序和分页操作。 |
| `FooterRow` | 获取一个表示 `GridView` 控件中页脚行的 `GridViewRow` 对象。 |
| `FooterStyle` | 获取 `TableItem` 对象的引用，使我们能够设置 `GridView` 控件中页脚的外观。 |
| `GridLines` | 获取或设置 `GridView` 控件的网格样式。 |
| `HeaderRow` | 获取一个表示 `GridView` 控件中头部行的 `GridViewRow` 对象。 |
| `HeaderStyle` | 获取 `TableItem` 对象的引用，使我们能够设置 `GridView` 控件中头部行的外观。 |
| `HorizontalAlign` | 获取或设置 `GridView` 控件在页面上的水平对齐方式。 |
| `PageCount` | 获取显示 `GridView` 控件中源数据所需的页数。 |
| `PageIndex` | 获取或设置当前显示页的索引。 |
| `PageSettings` | 获取 `PageSettings` 对象的引用，使我们能够设置 `GridView` 控件中分页按钮的属性。 |
| `PageStyle` | 获取 `TableStyle` 对象的引用，使我们能够设置 `GridView` 控件中分页行的外观。 |
| `PageTemplate` | 获取或设置 `GridView` 控件分页行的自定义内容。 |
| `PageSize` | 获取或设置 `GridView` 控件中每页显示的行数。 |
| `RowHeaderColumn` | 获取或设置用作 `GridView` 控件头部的列名；提供此属性是为了让辅助技术设备的用户更方便地访问该控件。 |
| `Rows` | 获取一个 `GridRow` 对象集合，代表 `GridView` 中的数据行。 |
| `RowStyle` | 获取 `TableStyle` 对象的引用，使我们能够设置 `GridView` 控件中数据行的外观。 |
| `SelectedDataKey` | 获取 `DataKey` 对象，该对象包含 `GridView` 控件中选中行的数据值。 |
| `SelectedIndex` | 获取或设置 `GridView` 控件中选中行的索引。 |
| `SelectedRow` | 获取一个 `GridRow` 对象的引用，代表控件中的被选中行。 |
| `SelectedRowStyle` | 获取 `TableStyle` 对象的引用，使我们能够设置 `GridView` 控件中选中行的外观。 |
| `SelectedValue` | 获取 `GridView` 控件中选中行的数据值。 |
| `ShowFooter` | 获取或设置一个值，显示 `GridView` 控件中是否显示页脚行。 |
| `ShowHeader` | 获取或设置一个值，显示 `GridView` 控件中是否显示头部行。 |
| `SortDirection` | 获取正在排序列的排序方向。 |
| `SortExpression` | 获取与正在排序的列或列相关的排序表达式。 |
| `TopPagerRow` | 获取一个表示 `GridView` 控件中顶部分页器行的 `GridRow` 对象。 |
| `UseAccessibleHeader` | 获取或设置一个值，指示头部行是否渲染为可访问。 |

`GridView` 的重要方法列在表 22.4 中：

| 方法 | 描述 |
| --- | --- |
| `DataBind` | 从源绑定数据 |
| `Delete` | 删除指定索引的记录 |
| `IsBindableType` | 判断特定类型是否可以绑定到 `GridView` |
| `Sort` | 根据表达式对 `GridView` 进行排序 |
| `UpdateRow` | 更新数据 |

`GridView` 的重要事件列在表 22.5 中：

| 事件 | 描述 |
|--- |--- |
| `PageIndexChanged` | 当分页按钮被点击时，`GridView` 处理分页操作后 |
| `PageIndexChanging` | 当分页按钮被点击时，`GridView` 处理分页操作前 |
| `RowCancelingEdit` | 当编辑模式下的取消按钮被点击时，退出编辑模式 |
| `RowCommand` | 当 `GridView` 中的按钮被点击时 |
| `RowCreated` | 当行创建时 |
| `RowDataBound` | 当数据行绑定到 `GridView` 时 |
| `RowDeleted` | 当删除按钮被点击时，`GridView` 删除了该行后 |
| `RowDeleting` | 当删除按钮被点击时，`GridView` 删除该行前 |
| `RowEditing` | 当编辑按钮被点击时，`GridView` 进入编辑模式 |
| `RowUpdated` | 当更新按钮被点击时，`GridView` 更新该行后 |
| `RowUpdating` | 当更新按钮被点击时，`GridView` 更新该行前 |
| `SelectedIndexChanged` | 当选择按钮被点击时，`GridView` 处理选择后 |
| `SelectedIndexChanging` | 当选择按钮被点击时，`GridView` 处理选择前 |
| `Sorted` | 当排序链接被点击时，`GridView` 处理排序操作后 |
| `Sorting` | 当排序链接被点击时，`GridView` 处理排序操作前 |

现在，让我们学习一下 `DataList` 控件。

# DataList 控件

`DataList` 是一种通过模板显示数据的数据控件。这些模板定义了要在项目中显示的控件和 HTML 元素。`DataList` 类存在于 `System.Web.UI.WebControls` 命名空间。`DataList` 类的继承层次如下：

```
System.Object
System.Web.UI.WebControls.Control
System.Web.UI.WebControls.BaseList
System.Web.UI.WebControls.DataList
```

你可以使用表 22.6 中描述的模板更改 `DataList` 控件的内容：

| 模板名称 | 描述 |
|--- |--- |
| `AlternatingItemTemplate` | 为 `DataList` 控件中交替的项目提供格式和内容 |
| `EditItemTemplate` | 为 `DataList` 控件中待编辑的项目提供格式和内容 |
| `FooterTemplate` | 为 `DataList` 控件页脚部分的格式和内容，如果定义了，页脚部分将不会显示。 |

## 深入解析

| 表 22.6: `DataList` 类的模板 |
| :--- | :--- |
| 模板名称 | 描述 |
| `HeaderTemplate` | 为 `DataList` 控制的头部部分提供格式和内容，确保头部部分出现。 |
| `ItemTemplate` | 为 `DataList` 控制中的项提供格式和内容。这是一个必选模板。 |
| `SelectedItemTemplate` | 为 `DataList` 控制中当前选中项提供格式和内容。 |
| `SeparatorTemplate` | 为 `DataList` 控制中的分隔项提供格式和内容，确保分隔符不出现。 |

我们还可以配置 `DataList` 控制，允许用户在表格中编辑或删除记录，并且它可以以水平或垂直方向渲染其项。

`DataList` 类的重要属性列如表 22.7 所示：

| 表 22.7: `DataList` 类的重要属性 |
| :--- | :--- |
| 属性 | 描述 |
| `AlternatingItemStyle` | 设置 `DataList` 控制中交替项的属性 |
| `AlternatingItemTemplate` | 或设置 `DataList` 控制中交替项的模板 |
| `EditItemIndex` | 或设置要编辑的 `DataList` 控制中选中项的索引号 |
| `EditStyle` | 或设置 `DataList` 控制中被选中编辑的项的属性 |
| `EditTemplate` | 或设置 `DataList` 控制中被选中编辑的项的模板 |
| `ExtractRows` | 或设置值，指示 `DataList` 控制每个模板中定义的 Table 行是否被提取并显示 |
| `FooterStyle` | 或设置 `DataList` 控制底部部分的属性 |
| `FooterTemplate` | 或设置 `DataList` 控制底部部分的模板 |
| `GridLines` | 在启用 `RepeatLayout` 时，设置 `DataList` 控制的网格线样式 |
| `HeaderStyle` | 或设置 `DataList` 控制头部部分的属性 |
| `HeaderTemplate` | 或设置 `DataList` 控制头部部分的模板 |
| `Items` | 获取表示控制内单个项的 `DataItems` 对象的集合 |
| `ItemStyle` | 或设置 `DataList` 控制中项的属性，例如 `BackColor` |
| `ItemTemplate` | 或设置 `DataList` 控制中项的模板 |
