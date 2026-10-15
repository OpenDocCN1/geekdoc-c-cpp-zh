

## 表 26.44：EntityDataSource 类的注目属性

| 属性 | 描述 |
|---|---|
| TemplateControl | 获取或设置包含此控件的模板的引用。 (继承自 Control) |
| TemplateSourceDirectory | 获取包含当前服务器控件的 Page 或 UserControl 的虚拟目录。 (继承自 Control) |
| UniqueID | 获取服务器控件的唯一、层级限定的标识符。 (继承自 Control) |
| UpdateParameters | 获取在更新操作期间使用的参数集合 |
| ViewState | 获取一个状态信息字典，允许您在对同一页面的多次请求中保存和恢复服务器控件的视图状态。 (继承自 Control) |
| ViewStateIgnoresCase | 获取一个值，该值指示 StateBag 对象是否不区分大小写。 (继承自 Control) |
| Visible | 获取或设置一个值，该值指示控件是否以视觉方式显示。 (继承自 DataSourceControl) |
| Where | 获取或设置一个值，该值指定记录要包含在检索的数据中必须为真的条件 |
| WhereParameters | 获取用于创建 Where 子句的参数集合 |

EntityDataSource 类的注目方法在表 26.45 中列出：

## 表 26.45：EntityDataSource 类的注目方法

| 方法 | 描述 |
|---|---|
| DataBind() | 将数据源控件与数据库绑定 |
| Dispose() | 使控件能够在释放内存之前完成最后步骤 |

EntityDataSource 类的注目事件在表 26.46 中列出：

## 表 26.46：EntityDataSource 类的注目事件

| 事件 | 描述 |
|---|---|
| ContextCreated | 在创建上下文类型对象的实例后调用 |
| ContextCreating | 在创建上下文类型对象的实例之前调用 |
| ContextDisposing | 在释放上下文类型对象之前调用 |
| DataBinding | 当服务器控件绑定到数据源时发生。 (继承自 Control。) |
| Deleted | 在删除操作完成后调用 |
| Deleting | 在删除操作开始前调用 |
| Disposed | 当服务器控件从内存中释放时发生，这是 ASP.NET 页面请求时服务器控件生命周期的最后阶段。 (继承自 Control。) |
| Init | 当服务器控件初始化时发生，这是其生命周期的第一步。 (继承自 Control。) |
| Inserted | 在插入操作完成后调用 |
| Inserting | 在插入操作开始前调用 |

| 事件 | 描述 |
|---|---|
| Load | 当服务器控件加载到 Page 对象中时发生。 (继承自 Control。) |
| PreRender | 在 Control 对象加载后但在呈现之前发生。 (继承自 Control。) |
| Selected | 在数据检索操作完成后调用 |
| Selecting | 在数据检索操作开始前调用 |
| Unload | 当服务器控件从内存中卸载时发生。 (继承自 Control。) |
| Updated | 在更新操作完成后调用 |
| Updating | 在更新操作开始前调用 |

现在，让我们学习 SiteMapDataSource 控件。

## SiteMapDataSource 控件

SiteMapDataSource 控件允许您使用 SiteMap 配置文件中存储的数据进行工作。此控件还提供了使用站点地图数据与数据服务器控件自定义站点导航的能力，而不管控件是否不是导航控件。SiteMapDataSource 控件的继承层次结构如下：

```
System.Object
  System.Web.UI.Control
    System.Web.UI.HierarchicalDataSourceControl
      System.Web.UI.WebControls.SiteMapDataSource
```

SiteMapDataSource 类的注目属性在表 26.47 中列出：

## 表 26.47：SiteMapDataSource 类的注目属性

| 属性 | 描述 |
|---|---|
| ContainsListCollection | 获取一个值，该值指示数据源控件是否包含数据源视图对象的集合 |
| Context | 获取与当前 Web 请求关联的服务器控件的 HttpContext 对象。 (继承自 Control。) |
| Controls | 获取表示 UI 层次结构中指定服务器控件的子控件的 ControlCollection 对象。 (继承自 HierarchicalDataSourceControl。) |
| DesignMode | 获取一个值，该值指示控件是否正在设计表面上使用。 (继承自 Control。) |
| EnableTheming | 获取一个值，该值指示此控件是否支持主题。 (继承自 HierarchicalDataSourceControl。) |
| EnableViewState | 获取或设置一个值，该值指示服务器控件是否将其视图状态以及其包含的任何子控件的视图状态持久保存到请求客户端。 (继承自 Control。) |
| Events | 获取控件的事件处理程序委托列表。此属性为只读。 (继承自 Control。) |
| HasChildViewState | 获取一个值，该值指示当前服务器控件的子控件是否具有任何已保存的视图状态设置。 (继承自 Control。) |
| ID | 获取或设置分配给服务器控件的程序标识符。 (继承自 Control。) |
| IdSeparator | 获取用于分隔控件标识符的字符。 (继承自 Control。) |

## 立即可用的解决方案

## 使用 SqlDataSource 控件

在本章中，您已了解到可以使用任何数据源控件，例如 SqlDataSource 控件，通过数据绑定控件，例如 GridView 控件来显示或自定义数据。数据源控件和数据绑定控件的选择取决于应用程序的需求。

> NOTE
> 在本节中，我们将使用 GridView 控件介绍所有数据源控件。

现在，让我们了解 SqlDataSource 控件。实施以下步骤以使用 SqlDataSource 控件在 GridView 控件中显示数据：

- 1. 创建一个 Web 应用程序并将其保存为 SqlDataSource（可在 CD 上获得）。

> NOTE
> 本章中的应用程序是使用“新建网站”对话框中的 ASP.NET 空 Web 站点模板创建的。创建应用程序后，您需要向应用程序添加 Default.aspx 页面。

- 2. 将 SqlDataSource 控件拖放到 Default.aspx 页面的设计视图中。现在，单击智能标记，如图 26.1 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1299_0.png)

图 26.1：将 SqlDataSource 控件添加到 Web 页面

> NOTE
> 图 26.1 中 SqlDataSource 控件右侧的箭头符号代表智能标记。

- 3. 单击配置数据源选项以使用 SqlDataSource 控件配置数据源，如图 26.2 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1300_0.png)

# 图 26.2：配置 SqlDataSource 控件的数据源

配置数据源向导出现（图 26.3）。

- 4. 单击新建连接按钮，如图 26.3 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1300_1.png)

# 图 26.3：单击新建连接按钮

添加连接对话框出现（图 26.4）。

5. 在添加连接对话框中，分别从服务器名称组合框中选择服务器名称，从选择或输入数据库名称组合框中选择数据库名称。在此示例中，我们选择了 northwnd 作为数据库（图 26.4）。

6. 单击测试连接按钮以测试与数据库的连接，如图 26.4 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1301_0.png)

# 图 26.4：添加连接

Microsoft Visual Studio 消息框出现，显示与数据库的连接已成功建立（图 26.5）。

7. 单击 Microsoft Visual Studio 消息框中的确定按钮，如图 26.5 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1301_1.png)

# 图 26.5：显示成功消息

8. 单击添加连接对话框中的确定按钮。现在，已创建到 northwnd 数据库的连接（图 26.6）。

9. 单击下一步按钮，如图 26.6 所示：

