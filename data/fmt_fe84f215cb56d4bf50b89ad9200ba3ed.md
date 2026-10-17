
`DataPager` 控件的继承层次结构如下：

```
System.Object
System.Web.UI.Control
System.Web.UI.WebControls.DataPager
```

`DataPager` 类的显著属性列于表 26.23 中：

### 表 26.23：DataPager 类的显著属性

| 属性 | 描述 |
|---|---|
| `Attributes` | 检索 `DataPager` 控件的自定义属性名称/值对列表。 |
| `BindingContainer` | 获取包含此控件数据绑定的控件。 （继承自 `Control`。） |
| `ChildControlsCreated` | 获取指示服务器控件的子控件是否已创建的值。 （继承自 `Control`。） |
| `ClientID` | 获取 ASP.NET 生成的服务器控件标识符。 （继承自 `Control`。） |
| `ClientIDSeparator` | 获取表示 `ClientID` 属性中使用的分隔符字符的字符值。 （继承自 `Control`。） |
| `Context` | 获取与当前 Web 请求关联的服务器控件的 `HttpContext` 对象。 （继承自 `Control`。） |
| `Controls` | 获取表示 `DataPager` 控件在 UI 层次结构中的子控件的 `ControlCollection` 对象。 |
| `DesignMode` | 获取指示控件是否正在设计表面上使用的值。 （继承自 `Control`。） |
| `EnableTheming` | 获取或设置指示主题是否适用于此控件的值。 （继承自 `Control`。） |
| `EnableViewState` | 获取或设置指示服务器控件是否将其视图状态以及其包含的任何子控件的视图状态持久保存到请求客户端的值。 （继承自 `Control`。） |
| `Events` | 获取控件的事件处理程序委托列表。 此属性为只读。 （继承自 `Control`。） |
| `Fields` | 获取表示 `DataPager` 控件中指定的分页字段的 `DataPagerField` 对象集合。 |
| `HasChildViewState` | 获取指示当前服务器控件的子控件是否有任何已保存的视图状态设置的值。 （继承自 `Control`。） |
| `ID` | 获取或设置分配给服务器控件的程序标识符。 （继承自 `Control`。） |
| `IdSeparator` | 基础结构。 获取用于分隔控件标识符的字符。 （继承自 `Control`。） |
| `IsChildControlStateCleared` | 获取指示此控件中包含的控件是否有控件状态的值。 |
| `IsTrackingViewState` | 获取指示服务器控件是否正在保存其视图状态更改的值。 （继承自 `Control`。） |
| `IsViewStateEnabled` | 获取指示此控件是否启用视图状态的值。 （继承自 `Control`。） |
| `LoadViewStateByID` | 获取指示控件是否参与通过 `ID` 而不是索引加载其视图状态的值。 （继承自 `Control`。） |
| `MaximumRows` | 获取为每页数据显示的记录的最大数量。 |
| `Page` | 获取包含服务器控件的 `Page` 实例的引用。 （继承自 `Control`。） |
| `PagedControlID` | 获取或设置将由 `DataPager` 控件分页的控件的 `ID`。 |
| `PageSize` | 获取或设置为每页数据显示的记录数。 |
| `Parent` | 获取对页面控件层次结构中服务器控件父控件的引用。 （继承自 `Control`。） |
| `QueryStringField` | 获取或设置查询字符串字段的名称。 |
| `Site` | 获取有关在设计表面上呈现时承载当前控件的容器的信息。 （继承自 `Control`。） |
| `SkinID` | 获取或设置要应用于控件的皮肤。 （继承自 `Control`。） |
| `StartRowIndex` | 获取在数据页上显示的第一条记录的索引。 |
| `TagKey` | 获取用于呈现 `DataPager` 控件的 HTML 元素。 |
| `TemplateControl` | 获取或设置包含此控件的模板的引用。 （继承自 `Control`。） |
| `TemplateSourceDirectory` | 获取包含当前服务器控件的 `Page` 或 `UserControl` 的虚拟目录。 （继承自 `Control`。） |
| `TotalRowCount` | 获取底层数据源对象检索的总记录数。 此数据源对象由关联的数据绑定控件引用。 |

`DataPager` 类的显著方法列于表 26.24 中：

### 表 26.24：DataPager 类的显著方法

| 方法 | 描述 |
|---|---|
| `DataBind()` | 用于将 `DataPager` 控件及其所有子控件绑定到数据源 |
| `RenderBeginTag()` | 用于将 `DataPager` 控件的 HTML 开启标签呈现到指定的写入器 |
| `SetPageProperties()` | 用于设置 `DataPager` 控件中的分页相关属性 |

## `Chart` 控件

`Chart` 控件使您能够以更简单的方式呈现复杂数据。 它帮助您以图表的方式更轻松地分析数据。 当您将 `Chart` 控件拖到页面上时，以下代码会出现在页面的源视图中：

```
<asp:Chart ID="Chart1" runat="server">
  <series>
    <asp:Series Name="Series1">
    </asp:Series>
  </series>
  <chartareas>
    <asp:ChartArea Name="ChartArea1">
    </asp:ChartArea>
  </chartareas>
</asp:Chart>
```

`Chart` 控件的继承层次结构如下：

```
System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.WebControl
    System.Web.UI.WebControls.BaseDataBoundControl
    System.Web.UI.WebControls.DataBoundControl
    System.Web.UI.DataVisualization.Charting.Chart
```

`Chart` 类的显著属性列于表 26.25 中：

### 表 26.25：Chart 类的显著属性

| 属性 | 描述 |
|---|---|
| `AlternateText` | 在未显示图表图像时显示替代文本 |
| `AccessKey` | 存储键盘快捷键 （继承自控件） |
| `BackImage` | 获取或设置背景图像路径 |
| `BackImageAlignment` | 获取或设置背景图像的对齐方式 |
| `ClientIDMode` | 为控件生成 `ClientID` 属性 （继承自控件） |
| `Compression` | 存储压缩值 |
| `DataSourceID` | 存储数据源控件的 `ID` |
| `ViewStateContent` | 在 `ViewState` 中保存图表内容 |
| `ViewStateMode` | 确定是否启用图表控件的视图状态 （继承自控件） |
| `Visible` | 决定控件是否应可见 |

`Chart` 类的显著方法列于表 26.26 中：

### 表 26.26：Chart 类的显著方法

| 方法 | 描述 |
|---|---|
| `CopyBaseAttributes()` | 允许您仅复制未由 `Style` 对象封装的属性，从定义的 Web 服务器控件复制到调用此方法的 Web 服务器控件。 |
| `MergeStyle()` | 允许您将定义样式的非空白元素复制到 Web 控件，并且不会覆盖控件的任何现有元素。 |
| `Paint()` | 允许您在图形中绘制图表图像。 |
| `RenderBeginTag()` | 将指定标记元素的开始标签写入输出流。 |
| `RenderEndTag()` | 将标记元素的结束标签写入输出流 （继承自控件）。 |

`Chart` 类的显著事件列于表 26.27 中：

### 表 26.27：Chart 类的显著事件

| 事件 | 描述 |
|---|---|
| `Click` | 在控件被单击时调用 |
| `Customize` | 在绘制图表图像之前调用 |
| `DataBound` | 在控件被 `DataBound` 时调用 （继承自控件） |
| `Disposed` | 在控件被释放时调用 |
| `PostPaint` | 在图表元素被绘制时调用 |

## `QueryExtender` 控件

`QueryExtender` 控件是一个数据源控件，有助于从数据库中检索仅满足特定条件或换句话说，过滤记录的记录。 记录过滤有助于显示在不影响数据集的情况下以各种方式在网页上记录。当你将 `QueryExtender` 控件拖到页面上时，页面的源视图中会出现以下代码：

```
<asp:QueryExtender ID="QueryExtender1" runat="server"></asp:QueryExtender>
```

`QueryExtender` 控件的继承层次结构如下：

```
System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.QueryExtender
```

`QueryExtender` 类的 noteworthy 属性在表 26.28 中列出：

### Table 26.28: Noteworthy Properties of the QueryExtender Class

| Property | Description |
|---|---|
| `ClientIDMode` | 为控件生成 `ClientID` 属性（继承自 control） |
| `EnableViewState` | 决定控件是否自动保存其视图状态（继承自 control） |
| `TargetControlID` | 保存目标控件的 `id` |
| `ViewStateMode` | 确定视图状态是否对图表控件启用 |
| `Visible` | 决定控件是否应可见 |

`QueryExtender` 类的 noteworthy 事件在表 26.29 中列出：

### Table 26.29: Noteworthy Events of the QueryExtender Class

| Event | Description |
|---|---|
| `Disposed` | 在控件被释放时调用 |
| `Init` | 在网页初始化时调用 |
| `Load` | 在网页加载时调用 |
| `Unload` | 在网页卸载时调用 |

`QueryExtender` 类的 noteworthy 方法在表 26.30 中列出：

### Table 26.30: Noteworthy Methods of the QueryExtender Class

| Method | Description |
|---|---|
| `ApplyStyleSheetSkin()` | 将样式表中定义的样式应用到控件 |
| `DataBind()` | 将数据源控件与数据库绑定 |
| `Dispose()` | 使控件在从内存中释放之前完成最后步骤 |
| `FindControl()` | 借助其 `id` 搜索服务器控件 |
| `Focus()` | 将焦点设置到控件上 |
| `HasControls()` | 确定父服务器控件中的子服务器控件 |

`QueryExtender` 类的 noteworthy 表达式在表 26.31 中列出：

### Table 26.31: Noteworthy Expressions of the QueryExtender Class

| Expressions | Description |
|---|---|
| `SearchExpression` | 搜索字符串值并与给定字符串值进行比较 |
| `RangeExpression` | 使用一对值定义范围 |
| `PropertyExpression` | 将表中列的值与给定的字符串值进行比较 |
| `OrderByExpression` | 按特定列对数据进行排序 |
| `CustomExpression` | 提供可自定义的 LINQ 表达式 |
| `DynamicFilterExpression` | 在动态数据网站中动态过滤数据 |
| `ControlFilterExpression` | 在动态数据网站中过滤控件 |

## The `SqlDataSource` Control

`SqlDataSource` 控件是一个数据源控件，允许服务器控件（如 `GridView` 控件）访问位于关系数据库（如 Microsoft SQL Server 和 Oracle）中的数据。该控件还生成连接字符串以与 ASP.NET 页面中的数据进行交互。这些连接字符串是通过 Configure Data Source 向导生成的。连接字符串包含有关你在应用程序中使用的服务器、数据库和安全性的信息，例如：

```
Data Source=.\sqlexpress; Initial Catalog=Northwnd; Integrated Security=True
```

### NOTE

要详细了解 Configure Data Source Wizard，请参阅本章的 Immediate Solutions 部分。

`SqlDataSource` 控件自动打开数据库连接，该连接在连接字符串中提供，执行 SQL 查询，然后关闭连接。当你向 ASP.NET 页面添加 `SqlDataSource` 控件时，以下代码会出现在页面的源视图中：

```
<asp:SqlDataSource ID="SqlDataSource1" runat="server"></asp:SqlDataSource>
```

`SqlDataSource` 控件的继承层次结构如下：

```
System.Object

  System.Web.UI.Control

    System.Web.UI.DataSourceControl

      System.Web.UI.WebControls.SqlDataSource
```
