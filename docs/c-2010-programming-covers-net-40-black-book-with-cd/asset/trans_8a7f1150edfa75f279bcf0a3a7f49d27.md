

## 表 26.13：FormView 控件的模板

| 模板类型 | 描述 |
|---|---|
| EmptyDataTemplate | 描述当 FormView 控件绑定到不包含任何记录的数据源时显示的空数据行的内容。此模板通常包含用于提醒用户数据源不包含任何记录的内容。 |
| FooterTemplate | 描述页脚行的内容。此模板通常包含您希望在页脚行中显示的任何附加内容。 |
| HeaderTemplate | 描述页眉行的内容。此模板通常包含您希望在页眉行中显示的任何附加内容。 |
| ItemTemplate | 描述 FormView 控件处于只读模式时的数据行内容。此模板通常包含用于显示现有记录的值的内容。 |
| InsertItemTemplate | 描述 FormView 控件处于插入模式时的数据行内容。此模板通常包含输入控件和命令按钮，用户可通过它们添加新记录。 |
| PagerTemplate | 描述分页功能启用时显示的分页行的内容，即当 AllowPaging 属性设置为 true 时。此模板通常包含控件，用户可借助这些控件导航到另一条记录。 |

### 注意

> 我们必须手动添加用于更新、删除或插入操作的命令按钮，因为 FormView 控件没有自动生成命令按钮的方式。

FormView 类的注目属性在表 26.14 中列出：

## 表 26.14：FormView 类的注目属性

| 属性 | 描述 |
|---|---|
| AllowPaging | 获取或设置指示是否启用分页功能的值。 |
| BackImageUrl | 获取或设置要在 FormView 控件背景中显示的图像的 URL。 |
| BottomPagerRow | 获取表示 FormView 控件底部显示的分页行的 FormViewRow 对象。 |
| Caption | 获取或设置要在 FormView 控件中的 HTML caption 元素中呈现的文本。此属性用于使控件对辅助技术设备用户更易访问。 |
| CaptionAlign | 获取或设置 FormView 控件中 HTML caption 元素的水平或垂直位置。 |
| CellPadding | 获取或设置单元格内容与其边框之间的空间量。 |
| CellSpacing | 获取或设置单元格之间的空间量。 |
| CurrentMode | 获取 FormView 控件当前的数据输入模式。 |
| DataItem | 获取绑定到 FormView 控件的数据项。 |
| DataItemCount | 获取数据源中的数据项数。 |
| DataItemIndex | 获取从数据源中绑定到 FormView 控件的数据项的索引。 |
| DataKey | 获取表示显示记录主键的 DataKey 对象。 |
| DataKeyNames | 获取或设置包含数据源键字段名称的数组。 |
| DefaultMode | 获取或设置 FormView 控件在更新、插入或取消操作后返回的数据输入模式。 |
| EditItemTemplate | 获取或设置编辑模式下项目的自定义内容。 |
| EditRowStyle | 获取对 TableItemStyle 对象的引用，允许您设置 FormView 控件处于编辑模式时数据行的外观。 |
| EmptyDataRowStyle | 获取对 TableItemStyle 对象的引用，允许您设置当绑定到 FormView 控件的数据源不包含任何记录时显示的空数据行的外观。 |
| EmptyDataTemplate | 获取或设置当 FormView 控件绑定到不包含任何记录的数据源时呈现的空数据行的用户定义内容。 |
| EmptyDataText | 获取或设置当 FormView 控件绑定到不包含任何记录的数据源时在空数据行中显示的文本。 |
| EnableModelValidation | 获取或设置指示验证器控件是否将在插入或更新操作期间发生的异常时处理的 value。 |
| FooterRow | 获取表示 FormView 控件中页脚行的 FormViewRow 对象。 |
| FooterStyle | 获取对 TableItemStyle 对象的引用，允许您设置 FormView 控件中页脚行的外观。 |
| FooterTemplate | 获取或设置 FormView 控件中页脚行的用户定义内容。 |
| FooterText | 获取或设置要在 FormView 控件的页脚行中显示的文本。 |
| GridLines | 获取或设置 FormView 控件的网格线样式。 |
| HeaderRow | 获取表示 FormView 控件中页眉行的 FormViewRow 对象。 |
| HeaderStyle | 获取对 TableItemStyle 对象的引用，允许您设置 FormView 控件中页眉行的外观。 |
| HeaderTemplate | 获取或设置 FormView 控件中页眉行的用户定义内容。 |
| HeaderText | 获取或设置要在 FormView 控件的页眉行中显示的文本。 |
| HorizontalAlign | 获取或设置页面上 FormView 控件的水平对齐方式。 |
| InsertItemTemplate | 获取或设置插入模式下项目的自定义内容。 |
| InsertRowStyle | 获取对 TableItemStyle 对象的引用，允许您设置 FormView 控件处于插入模式时数据行的外观。 |
| ItemTemplate | 获取或设置 FormView 控件处于只读模式时数据行的自定义内容。 |
| PageCount | 获取显示数据源中每条记录所需的总页数。 |
| PageIndex | 获取或设置显示页的索引。 |
| PagerSettings | 获取对 PagerSettings 对象的引用，允许您设置 FormView 控件中分页按钮的属性。 |
| PagerStyle | 获取对 TableItemStyle 对象的引用，允许您设置 FormView 控件中分页行的外观。 |
| PagerTemplate | 获取或设置 FormView 控件中分页行的自定义内容。 |
| Row | 获取表示 FormView 控件中数据行的 FormViewRow 对象。 |
| RowStyle | 获取对 TableItemStyle 对象的引用，允许您设置 FormView 控件处于只读模式时数据行的外观。 |
| SelectedValue | 获取 FormView 控件中当前记录的数据键值。 |
| TopPagerRow | 获取表示 FormView 控件顶部显示的分页行的 FormViewRow 对象。 |

FormView 类的注目方法在表 26.15 中列出：

## 表 26.15：FormView 类的注目方法

| 方法 | 描述 |
|---|---|
| ChangeMode() | 用于将 DetailsView 控件切换到指定模式 |
| DataBind() | 用于将数据源中的数据绑定到控件 |
| DeleteItem() | 用于从数据源中删除当前记录 |
| InsertItem() | 用于在数据源中插入当前记录 |
| IsBindableType() | 用于确定指定的数据类型是否可以绑定到 DetailsView 控件中的字段 |
| UpdateItem() | 用于更新数据源中的当前记录 |

FormView 类的注目事件在表 26.16 中列出：

## 表 26.16：FormView 类的注目事件

| 事件 | 描述 |
|---|---|
| ItemCommand | 当 FormView 控件内的按钮被点击时调用 |
| ItemCreated | 在 FormView 控件中的所有行创建后调用 |
| ItemDeleted | 当 FormView 控件内的 Delete 按钮被点击时调用，但在删除操作之后 |
| ItemDeleting | 当 FormView 控件内的 Delete 按钮被点击时调用，但在删除操作之前 |
| ItemInserted | 当 FormView 控件内的 Insert 按钮被点击时调用，但在插入操作之后 |
| ItemInserting | 当 FormView 控件内的 Insert 按钮被点击时调用，但在插入操作之前 |
| ItemUpdated | 当 FormView 控件内的 Update 按钮被点击时调用，但在更新操作之后 |
| ItemUpdating | 当 FormView 控件内的 Update 按钮被点击时调用，但在更新操作之前。 |
| ModeChanged | 当 FormView 控件在编辑、插入和只读模式之间切换时调用，但在模式更改后 |
| ModeChanging | 当 FormView 控件在编辑、插入和只读模式之间切换时调用，但在模式更改之前 |

