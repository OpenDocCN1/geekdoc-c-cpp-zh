
| IsControlStateCleared | 获取一个值，指示此控件包含的控件是否已清除。（继承自 `Control`。） |

| IsTrackingViewState | 获取一个值，指示服务器控件是否正在保存其视图状态的更改。（继承自 `Control`。） |

| IsViewStateEnabled | 获取一个值，指示此控件是否启用了视图状态。（继承自 `Control`。） |

| Items | 获取 `Repeater` 控件中 `RepeaterItem` 对象的集合 |

| ItemTemplate | 获取或设置定义 `Repeater` 中的项目如何显示的 `System.Web.UI.ITemplate` |

| LoadStateByID | 获取一个值，指示控件是否通过 ID 而不是索引参与加载其状态。（继承自 `Control`。） |

| Page | 获取包含服务器控件的 `Page` 实例引用。（继承自 `Control`。） |

| Parent | 获取页面控件层次结构中服务器控件父级的引用。（继承自 `Control`。） |

# 第 22 章：ASP.NET 中的数据绑定

| 属性 | 描述 |

| :--- | :--- |

| RequiresDataBinding | 获取或设置一个值，指示 `Repeater` 控件是否需要绑定到指定的数据源 |

| SelectArguments | 获取 `Repeater` 控件在从数据源控件检索数据时使用的 `DataSourceSelectArguments` 对象 |

| SeparatorTemplate | 获取或设置定义项目之间分隔符显示方式的 `System.Web.ITemplate` 接口 |

`Repeater` 的重要事件列表 22.22。

## 表 22.22: Repeater 类的重要事件

| 事件 | 描述 |

| :--- | :--- |

| ItemCommand | 当点击 `Repeater` 控件中的按钮时触发 |

| ItemCreated | 当 `Repeater` 控件中创建项目时触发 |

| ItemDataBound | 在 `Repeater` 中的项目数据绑定之后但在在页面上渲染之前触发 |

现在，让我们来学习 `DataPager` 控件。

## DataPager 控件

`DataPager` 控件用于为数据控件（如 `ListView` 控件）提供分页功能。当你使用 `DataPager` 进行控制时，页面的 Source 视图中会出现以下代码：

```
<asp:DataPager Id="DataPager1" runat="server" /> </asp:DataPager>
```

`DataPager` 的继承关系如下：

```
System.Object
System.Web
System.Web.UIControls.DataPager
```

`DataPager` 类的重要属性列在表 22.23 中。

## 表 22.23: DataPager 类的重要属性

| 属性 | 描述 |

| :--- | :--- |

| Attributes | 获取或设置一个属性名称/值对集合 |

| BindingContainer | 获取包含数据绑定控件的控件 |

| ChildControlsCreated | 获取一个值，指示服务器控件的子控件是否已创建。（继承自 `Control`。） |

| ClientID | 获取服务器标识符。 |

| ClientIDSeparator | 获取或设置分隔符字符。 |

| Context | 获取与当前 Web 请求的服务器控件关联的 `HttpContext`。（继承自 `Control`。） |

| Controls | 获取包含子控件的 `ControlCollection` |

| DesignMode | 获取一个值，指示控件是否正在设计表面上使用。（继承自 `Control`。） |

| EnableTheming | 获取或设置一个值，指示是否将主题应用到此控件。（继承自 `Control`。） |

| EnableViewState | 获取或设置一个值，指示控件是否将其状态及其任何子控件的视图持久化到请求客户端。（继承自 `Control`。） |

| Events | 获取控件的事件处理程序列表。此属性为只读。（继承自 `Control`。） |

| Fields | 获取表示分页器的 `DataField` 对象的集合。 |

| HasChildViewState | 获取一个值，指示服务器控件的子控件是否保存了视图状态。（继承自 `Control`。） |

| ID | 获取或设置分配给服务器控件的程序化标识符。（继承自 `Control`。） |

| IdSeparator | 获取用于分隔控件标识符的字符。（继承自 `Control`。） |

| IsControlStateCleared | 获取一个值，指示此控件包含的控件是否已清除。（继承自 `Control`。） |

| IsTrackingViewState | 获取一个值，指示服务器控件是否正在保存其视图状态的更改。（继承自 `Control`。） |

| IsViewStateEnabled | 获取一个值，指示此控件是否启用了视图状态。（继承自 `Control`。） |

| LoadViewStateByID | 获取一个值，指示控件是否通过 ID 而不是索引参与加载其状态。（继承自 `Control`。） |

| MaximumRows | 获取每页显示的记录的最大数量。 |

| Page | 获取包含服务器控件的 `Page` 实例引用。（继承自 `Control`。） |

| PagedControlID | 获取或设置由 `DataPager` 控件分页处理数据的控件的 ID |

| PageSize | 获取每页显示的记录数。 |

| Parent | 获取页面控件层次结构中服务器控件父级的引用。（继承自 `Control`。） |

| QueryStringField | 获取或设置查询字符串字段。 |

| Site | 获取在设计表面上渲染时持有当前控件的容器信息。（继承自 `Control`。） |

| SkinID | 获取或设置应用到控件的皮肤。（继承自 `Control`。） |

| StartRow | 获取数据页中显示的第一条记录的索引。 |

| TagKey | 获取用于渲染 `DataPager` 控件的 HTML 元素。 |

| TemplateControl | 获取或设置此控件包含的模板引用。（继承自 `Control`。） |

| TemplateDirectory | 获取包含服务器控件的 `Page` 或 `UserControl` 的虚拟目录。（继承自 `Control`。） |

| TotalRowCount | 获取数据源对象检索的记录总数。此数据源对象由关联的数据绑定控件引用。 |

## 深入析

# 第 22 章：ASP.NET 中的数据绑定

`DataPager` 类的重要方法如表 22.24 所示：

| 方法 | 说明 |

| --- | --- |

| DataBind | 用于将 `DataPager` 控件及其所有子绑定到数据源 |

| RenderBeginTag | 用于向指定的写入器渲染 `DataPager` 控件的 HTML 开启标签 |

| SetPageProperties | 用于设置 `DataPager` 控件中与页面相关的属性 |

## Chart 控件

`Chart` 图表控件能够你你以更简单的方式展示复杂数据。它可以帮助你通过图表分析数据。当你将图表绘制到页面时，源代码中会出现以下代码：

```xml
<asp:Chart Id="Chart1" runat="Server">
  <series>
    <asp:Series Name="Series1"></asp:Series>
  </series>
  <chartareas>
    <asp:ChartArea Name="Chartarea1"></asp:ChartArea>
  </chartareas>
</asp:Chart>
```

`Chart` 控件的继承关系如下：

```
System.Object
System.UI.Control
  System.UI.Controls.DataboundControl
    System.UI.Controls.DataboundControl
      System.UI.DataVirtualization.charting.Chart
```

`Chart` 类的重要属性如表 22.25 所示：

| 属性 | same |

| --- | --- |

| AlternateText | 当图表未显示时的替代文本 |

| AccessKey | 存储快捷键（继承自控件） |

| BackImage | 获取或设置背景图像 |

| AlignmentMode | 获取或设置背景图像的对齐方式

| Compression | 存储压缩值 |

| DataSourceID | 存储数据源的 ID |

| ViewState | 在 `ViewState` 中保存 |

| ModelState | 决定是否启用视图状态（继承自控件） |

| Visible | 决定控件是否可见 |

`Chart` 类的重要方法如表 22.26 所示：

| 方法 | 说明 |

| --- | --- |

| CopyBaseAttributes | 允许将由 `Style` 对象封装的属性复制到调用该方法的 Web 控件 |

| Paint | 允许在图形中绘制图表 |

| RenderBeginTag | 向输出流写入指定标记元素的开启标签 |

| RenderEndTag | 向输出流写入标记元素的结束标签（继承自控件） |

`Chart` 类的重要事件如表 22.27 所示。

| 事件 | same |

| --- | --- |

| Click | 当控件被点击时触发 |

| Customize | 在绘制图表之前触发 |

| DataBound | 控件数据绑定时触发（继承自控件） |

| Disposed | 控件被释放时触发 |

| PostPaint | 图表元素被绘制后触发 |

## QueryExtender 控件

`QueryExtender` 控件是一种数据控件，有助于从数据库检索符合特定标准的记录，换句话说就是用于过滤记录。记录过滤有助于以多种方式在 Web 页面上显示记录而不影响数据集。当你将 `QueryExtender` 拖到页面上时，源代码会出现以下代码：

`QueryExtender` 控件的继承层次如下：

```xml
<QueryExtender ID="QueryExtender1" runat="server" />
```

```
System.Object
System.Web.UI.QueryExtender
```

`QueryExtender` 类的重要属性如表 22.28 所示。

| 属性 | same |

| --- | --- |

| ClientID | 生成 `ClientID` |

| EnableViewState | 控件是否启用了视图状态 |

| TargetID | 保存目标控件的 ID |

| ViewState | 决定控件是否启用了视图状态 |

| Visible | 决定控件是否可见 |

`QueryExtender` 类的重要事件如表 22.29 所示。

| 事件 | same |

| --- | --- |

| Disposed | 控件被释放时触发 |

| Init | 控件初始化时触发 |

| Load | 控件加载时触发 |

| Unload | 控件卸载时触发 |

# 第 22 章：ASP.NET 中的数据绑定

`QueryExtender` 类的重要方法如表 22.30 所示：

| 方法 | 说明 |

| --- | --- |

| ApplyStyle | 将样式应用到控件 |

| DataBind | 绑定数据源 |

| Dispose | 释放控件 |

| FindControl | 搜索控件 |

| Focus | 设置控件焦点 |

| HasControls | 决定控件是否已创建 |

`QueryExtender` 类的重要表达式如表 22.31 所示：

| 表达式 | 说明 |

| --- | --- |

| SearchExpression | 搜索值 |

| RangeExpression | 定义范围 |

| PropertyExpression | 比较值 |

| OrderBy | 按列排序 |

| CustomExpression | 提供自定义表达式 |

| DynamicFilterExpression | 动态过滤数据 |

| ControlExpression | 过滤控件 |

## SqlDataSource 控件

`SqlDataSource` 控件是一种数据控件，有助于 `GridView` 等控件访问关系型数据库。`SqlDataSource` 控件会自动打开与数据库的连接。

注意：要了解更多关于 `SqlDataSource` 的信息，请参考相关章节。

带有连接字符串的 `SqlDataSource` 控件会自动打开、执行 SQL 并关闭连接。当你将 `SqlDataSource` 添加到页面时，会出现以下内容：

```xml
<asp:SqlDataSource ID="SqlDataSource1" runat="server" ConnectionString="Data Source=Integrated Security=True">
```

`SqlDataSource` 控件的继承关系如下：

```
System.Object
System.UI.Control
  System.UI.WebControls.SqlDataSource
```

`SqlDataSource` 类的重要属性如表 22.32 所示：

| 属性 | same |

| --- | --- |

| CacheDuration | 设置缓存过期的时间（秒） |

| CacheExpirationPolicy | 设置与缓存相关的用户定义依赖 |

## 表 22.32：SqlDataSource 类的重要属性

| 属性 | same |

| --- | --- |

| CacheKeyDependency | 获取或设置所有缓存对象的依赖项 |

| SelectOnNullParameter | 表示数据检索是否取消 |

| ChildControlsCreated | 获取子控件是否已创建的值 |

| ClientID | 获取 ASP.NET 生成的服务器控件标识 |

| ClientIDSeparator | 获取表示 `ClientID` 中分隔符的字符 |

| ConflictDetection | 获取或设置 `SqlDataSource` 如何执行更新和删除 |

| ConnectionString | 获取或设置 ADO.NET 特定的连接字符串 |

| Context | 获取与服务器控件关联的 `HttpContext` |

| Controls | 获取表示服务器控件的集合 |

| DataSourceMode | 获取或设置使用的数据检索方法 |

| DeleteCommand | 获取或设置 `DeleteCommand` 是否为 SQL 语句或存储过程 |

| DeleteParameters | 获取 `DeleteCommand` 使用的参数集 |

| DesignMode | 获取控件是否在设计表面使用的值 |

| EnableCaching | 获取或设置 `SqlDataSource` 是否启用了数据缓存 |

| EnableTheming | 获取此控件是否支持主题 |

| EnableViewState | 获取或设置控件是否持久化其视图状态 |

| Events | 获取控件的事件委托列表 |

| FilterExpression | 获取或设置在 `Select` 方法期间应用的的过滤表达式 |

| FilterParameters | 获取与 `FilterExpression` 关联的参数集 |

| HasChildViewState | 获取子控件是否保存了视图状态设置的值

# 第 22 章：ASP.NET中的数据绑定

| 表 22.32：SqlDataSource 类的重要属性 |

| 属性 | 描述 |

| :--- | :--- |

| ID | 获取或设置分配给服务器控件的程序标识符。（继承自 `Control`） |

| IdSeparator | 获取用于分隔标识符的字符。（继承自 `Control`） |

| InsertCommand | 获取或设置 `SqlDataSource` 控制用于将数据插入数据库的 SQL 字符串 |

| InsertCommandType | 获取或设置 `InsertCommand` 属性中的文本是 SQL 语句还是存储过程名称。 |

| InsertParameters | 获取由关联 `SqlDataSource` 对象的 `InsertCommand` 使用的参数集合 |

| IsChildControlState | 获取一个值，表示此控件内的控件是否有状态。（继承自 `Control`） |

| IsTrackingViewState | 获取一个值，表示服务器控件是否保存其视图状态的更改。（继承自 `Control`） |

| IsViewEnabled | 获取一个值，表示该控件是否启用了视图。（继承自 `Control`） |

| LoadViewByID | 获取一个值，表示是否通过 ID 加载视图。（继承自 `Control`） |

| OldValuesParameterString | 获取或设置传递给任何引用的字符串 |

| Page | 允许你获取服务器控件的 `Page` 实例。（继承自 `Control`） |

| Parent | 获取控件层次结构中父控件的引用。（继承自 `Control`） |

| ProviderName | 获取或设置 `SqlDataSource` 控制用于连接数据源的程序程序名称 |

| SelectCommand | 获取或设置控件用于从底层数据库检索数据的 SQL 字符串 |
