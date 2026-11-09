
### 表6.22：FormView 类的重要属性

| 属性 | 描述 |
|---|---|
| `CellPadding` | 获取或设置单元格内容与单元格边框之间的空间量。 |
| `CellSpacing` | 获取或设置单元格之间的空间量。 |
| `CurrentMode` | 获取 FormView 控件当前的数据输入模式。 |
| `DataItem` | 获取绑定到 FormView 控件的数据项。 |
| `DataItemCount` | 获取数据源中的数据项数。 |
| `DataItemIndex` | 获取从数据源绑定到 FormView 控件的数据项的索引。 |
| `DataKey` | 获取一个 DataKey 对象，该对象表示所显示记录的主键。 |
| `DataKeyNames` | 获取或设置一个数组，该数组包含数据源的键字段名称。 |
| `DefaultMode` | 获取或设置 FormView 控件在更新、插入或取消操作后返回的数据输入模式。 |
| `EditItemTemplate` | 获取或设置编辑模式下项的自定义内容。 |
| `EditRowStyle` | 获取一个引用，该引用允许您设置 FormView 控件处于编辑模式时数据行的外观。 |
| `EmptyDataRowStyle` | 获取一个引用，该引用允许您设置当绑定到 FormView 控件的数据源不包含任何记录时显示的空数据行的外观。 |
| `EmptyDataTemplate` | 获取或设置当 FormView 控件绑定到不包含任何记录的数据源时呈现的空数据行的用户定义内容。 |
| `EmptyDataText` | 获取或设置当 FormView 控件绑定到不包含任何记录的数据源时在空数据行中显示的文本。 |
| `EnableModelValidation` | 获取或设置一个值，该值指示验证器控件是否将处理插入或更新操作期间发生的异常。 |
| `FooterRow` | 获取表示 FormView 控件中页脚行的 FormViewRow 对象。 |
| `FooterStyle` | 获取对 TableItemStyle 对象的引用，该对象允许您设置 FormView 控件中页脚行的外观。 |
| `FooterTemplate` | 获取或设置 FormView 控件中页脚行的用户定义内容。 |
| `FooterText` | 获取或设置要在 FormView 控件的页脚行中显示的文本。 |
| `GridLines` | 获取或设置 FormView 控件的网格线样式。 |
| `HeaderRow` | 获取表示 FormView 控件中标题行的 FormViewRow 对象。 |
| `HeaderStyle` | 获取一个引用，该引用允许您设置 FormView 控件中标题行的外观。 |
| `HeaderTemplate` | 获取或设置 FormView 控件中标题行的用户定义内容。 |
| `HeaderText` | 获取或设置要在 FormView 控件的标题行中显示的文本。 |
| `HorizontalAlign` | 获取或设置 FormView 控件在页面上的水平对齐方式。 |
| `InsertItemTemplate` | 获取或设置插入模式下项的自定义内容。 |
| `InsertRowStyle` | 获取一个引用，该引用允许您设置 FormView 控件处于插入模式时数据行的外观。 |
| `ItemTemplate` | 获取或设置 FormView 控件处于只读模式时数据行的自定义内容。 |
| `PageCount` | 获取显示数据源中每条记录所需的总页数。 |
| `PageIndex` | 获取或设置所显示页面的索引。 |

### 表6.23：FormView 类的重要方法

| 方法 | 描述 |
| --- | --- |
| ChangeMode | 使您能够将 DetailsView 控件切换到指定模式。 |
| DataBind | 使您能够将数据源中的数据绑定到控件。 |
| DeleteItem | 使您能够从数据源中删除当前记录。 |
| InsertItem | 使您能够将当前记录插入数据源中。 |
| IsBindableType | 使您能够确定指定的数据类型是否可以绑定到 DetailsView 控件中的字段。 |
| UpdateItem | 使您能够更新数据源中的当前记录。 |

让我们通过执行以下步骤来学习在 Web 应用程序中使用 FormView 控件：

- 1. 单击**开始→所有程序→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010。**
- 2. 从菜单栏中选择**文件→新建→网站**。  
  将出现“新建网站”对话框。
- 3. 从中间模板窗格中选择**Visual C#→ASP.NET 网站**。
- 4. 将网站名称设置为 **FormViewControl**。
- 5. 单击**确定**按钮。  
  FormViewControl 应用程序已创建。
- 6. 从工具箱中将 FormView 控件拖放到 **Default.aspx** 页面上。
- 7. 单击 FormView 控件的智能标记，并像之前一样创建与数据库的连接。
- 8. 像之前一样使用“自动套用格式”对话框更改 FormView 控件的外观。
- 9. 像之前一样将 Default.aspx 页面设置为起始页。
- 10. 按 F5 键执行应用程序。应用程序的输出会显示出来，如图 ASP-6.38 所示：  
  ![](img/9862a98a1a2d3bb14334137965a1ec60_608_0.png)

图 ASP-6.38

了解 FormView 控件后，让我们学习 ListView 和 DataPager 控件。

## 使用 ListView 和 DataPager 控件

ListView 控件是一种数据绑定控件，用于显示关联数据源中的数据。它使您能够通过使用模板和样式以任意格式显示数据。您可以在 ListView 控件中选择、排序、删除和插入记录。此控件类似于 GridView 控件，不同之处在于它使用模板而不是字段来显示数据。您创建模板，以便更灵活地控制希望数据在 ListView 控件中的显示方式。

ListView 类定义了若干属性和方法，ListView 控件由于继承自该类而支持这些属性和方法。ListView 类的一些重要属性在表6.24中给出：

### 表6.24：ListView 类的重要属性

| 属性 | 描述 |
|---|---|
| EditItem | 检索 ListView 控件中处于编辑模式的项。 |
| EditItemTemplate | 检索或设置编辑模式下项的自定义内容。 |
| EmptyDataTemplate | 检索或设置当 ListView 控件绑定到不包含任何记录的数据源时呈现的空模板的用户定义内容。 |
| EmptyItemTemplate | 检索或设置当当前数据页的最后一行没有更多数据项可显示时，在 ListView 控件中呈现的空项的用户定义内容。 |
| GroupItemCount | 检索或设置 ListView 控件中每组要显示的项数。 |
| GroupPlaceholderID | 检索或设置 ListView 控件中组占位符的 ID。 |
| GroupSeparatorTemplate | 检索或设置 ListView 控件中组之间分隔符的用户定义内容。 |
| GroupTemplate | 检索或设置 ListView 控件中组容器的用户定义内容。 |
| ItemTemplate | 检索或设置 ListView 控件中数据项的自定义内容。 |

让我们通过执行以下步骤来学习如何在 Web 应用程序中使用 ListView 和 DataPager 控件：

- 1. *单击* **开始→所有程序→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010。**
- 2. 从菜单栏中*选择* **文件→新建→网站**。  
  将出现“新建网站”对话框。
- 3. 从中间模板窗格中*选择* **Visual C#→ASP.NET 网站**。
- 4. 将 Web 应用程序的名称*设置*为 **ListviewandDatapagerControl。**
- 5. *单击* **确定**按钮。  
  **ListviewandDatapagerControl** 应用程序已创建。
- 6. 将 ListView 控件*拖放*到 **Default.aspx** 页面上，并像之前一样创建与数据库的连接。
- 7. *单击*智能标记，并从“ListView 任务”菜单中选择“配置 ListView”选项。  
  将出现“配置 ListView”对话框（图 ASP-6.39）。
- 8. 从**选择布局**窗格中*选择* **项目符号列表**选项，并从**选择样式**窗格中*选择* **彩色**选项（图 ASP-6.39）。
- 9. *单击* **确定**按钮，如图 ASP-6.39 所示：  
  ![](img/9862a98a1a2d3bb14334137965a1ec60_610_0.png)
- 10. 将 **DataPager** 控件*拖放*到 **Default.aspx** 页面上。
- 11. *打开*“DataPager 任务”菜单，并将页导航样式设置为**数字页导航**。
- 12. *打开* **DataPager** 控件的**属性**窗口，并将 **PageControlID** 属性设置为 **ListView1**，如图 ASP-6.40 所示：  
  ![](img/9862a98a1a2d3bb14334137965a1ec60_610_1.png)
