

NOTE

要在网站的每个页面上使用 Web Parts 控件，必须使用单独的 WebPartManager 控件。然而，如果你想在包含 Web Parts 控件的多页网站上使用单个 WebPartManager 控件，请将 WebPartManager 控件放置在网站的主页上。

WebPartManager 控件是通过使用 .NET Framework 类库中的 WebPartManager 类创建的。该类位于 System.Web.UI.WebControls.WebParts 命名空间中，该命名空间位于 System.Web 程序集中。WebPartManager 类的继承层次结构如下：

+   System.Object
+   System.Web.UI.Control
+   System.Web.UI.WebControls.WebParts.WebPartManager

要使用 WebPartManager 控件，你需要在 Web 页面的源代码中声明它。

WebPartManager 控件的声明如下：

```
webPartManager <object name>;
```

WebPartManager 类的声明如下：

```
Public class WebPartManager : Control, INamingContainer, IPersonalizable
```

## Table 16.17: Noteworthy Methods of the WebPartManager Class

| Method | Description |
| --- | --- |
| ActivateConnections | 激活 Web 页面上所有当前处于非活动状态的连接。 |
| AddWebPart | 向 Web 页面添加一个 Web Parts 控件。 |
| BeginWebPartConnecting | 开始连接两个 Web Parts 控件的过程。 |
| BeginWebPartEditing | 开始修改一个 Web Parts 控件的过程。 |
| BuildProfileTree | 收集有关服务器控件的数据并将其发送到 Trace 属性，当为页面启用跟踪时，该属性会显示在 Web 页面上。 |
| CanConnectWebParts | 检查参与连接的 Web Parts，以确定控件是否能够连接。 |
| CheckRenderClientScript | 检查浏览器请求 Web 页面的能力。此方法还检查 EnableClientScript 属性的值，该属性指定是否渲染 Web 页面的客户端脚本。 |
| ClearChildControlState | 删除有关服务器控件的子控件的控件状态信息。此方法继承自 Control 类。 |
| ClearChildState | 删除有关服务器控件的子控件的视图状态和控件状态信息。此方法继承自 Control 类。 |
| ClearChildViewState | 删除有关服务器控件的子控件的视图状态信息。此方法继承自 Control 类。 |
| CloseWebPart | 关闭一个 Web Parts 控件，使其不在 Web 页面上渲染，但可以在 Web 页面上重新打开。 |
| ConnectWebParts | 连接存在于 WebPartZoneBase 区域中的两个 Web Parts 控件。 |
| Finalize | 使对象能够在对象被垃圾回收前释放资源并执行清理操作。 |
| Focus | 设置并移除对 WebPartManager 控件的焦点。 |
| GetConsumerConnectionPoints | 获取 ConsumerConnectionPoint 对象的集合，这些对象充当来自服务器控件的连接点。 |
| GetCurrentWebPartManager | 获取 Web 页面上 WebPartManager 控件的当前实例。 |
| GetDesignModeState | 检索与 WebPartManager 控件相关的设计时数据。 |
| GetDisplayTitle | 检索包含 Web Parts 控件的 DisplayTitle 属性值的字符串。 |
| GetExportUrl | 检索用户尝试导出 Web Parts 控件时使用的相对虚拟路径和查询字符串。 |
| GetGenericWebPart | 获取包含服务器控件的 GenericWebPart 控件实例的引用。 |
| GetHashCode | 作为 WebPartManager 类对象的哈希函数。哈希函数用于加密和解密数据，以便在通过 Internet 传输时使其安全。 |
| GetProviderConnectionPoints | 获取 ProviderConnectionPoint 对象的集合，这些对象充当作为提供者的服务器控件在 Web Parts 连接中的连接点。 |
| GetType | 返回当前对象的 Type 值。 |
| HasControls | 验证服务器控件是否包含子控件。 |
| HasEvents | 获取指定是否已为 Web Parts 控件或子控件注册事件的值。 |
| ImportWebPart | 导入包含 Web Parts 控件的状态和属性数据的 XML 描述文件。 |
| IsAuthorized | 指定是否可以将 Web Parts 或服务器控件添加到 Web 页面。 |
| IsLiteralContent | 决定服务器控件是否仅存储纯文本内容。（纯文本内容是指仅为纯文本，而非图像或控件的形式的内容。） |
| LoadControlState | 存储从先前页面请求保存的服务器控件的状态数据，并在后续请求中返回该数据。 |
| LoadCustomPersonalizationState | 存储由个性化对象传递给 WebPartManager 控件的自定义个性化数据。个性化数据在初始化过程中使用。个性化对象用于个性化 Web Parts 控件。 |
| LoadViewState | 返回先前页面请求的视图状态信息。该请求由 SaveViewState 方法保存。 |
| MapPathSecure | 返回控件的物理路径，该路径由虚拟路径映射，虚拟路径可以是绝对路径或相对路径。 |
| MemberwiseClone | 构造当前对象源的副本。 |
| MoveWebPart | 将服务器控件的位置从一个 WebPartZoneBase 区域更改到另一个区域，或更改到同一区域内的新位置。 |
| OnAuthorizeWebPart | 引发 AuthorizeWebPart 事件及其处理程序。 |
| OnBubbleEvent | 确定服务器控件的事件是否沿 Web 页面的用户界面 (UI) 服务器控件层次结构向上传递。 |
| OnConnectionsActivated | 引发 ConnectionActivated 事件以指定 Web 页面及其控件是否已在浏览器中加载。它还指示 Web 页面上的连接是否已激活以共享数据。 |
| OnConnectionsActivating | 引发 ConnectionActivating 事件以指示 Web 页面及其控件已在浏览器中加载，并且可以开始激活 Web 页面上的连接的过程。 |
| OnDataBinding | 引发 DataBinding 事件。 |
| OnDisplayModeChanged | 引发 DisplayModeChanged 事件以指定 WebPartManager 控件已完成更改 Web 页面显示模式的过程。 |
| OnDisplayModeChanging | 引发 DisplayModeChanging 事件以指定 WebPartManager 控件正在更改 Web 页面显示模式的过程中。 |
| OnInit | 引发 Init 事件。这是 WebPartManager 控件生命周期中的第一个事件。 |
| OnLoad | 引发 Load 事件。 |
| OnPreRender | 在 WebPartManager 控件在 Web 页面上渲染之前生成 PreRender 事件。此方法通知 WebPartManager 控件在保存视图状态和渲染内容之前执行任何必要的预渲染步骤。 |
| OnSelectedWebPartChanged | 在 Web Parts 控件被选中或其选择被清除后生成 SelectedWebPartChanged 事件。 |
| OnSelectedWebPartChanging | 在更改选定的 WebPart 控件时生成 SelectedWebPartChanging 事件。 |
| OnUnload | 生成基 Unload 事件以从 Web 页面中移除 WebPartManager 实例。 |
| OnWebPartAdded | 在 Web Parts 控件添加到 Web 页面后生成 WebPartAdded 事件。 |
| OnWebPartAdding | 在 Web Parts 控件添加到 WebPartZoneBase 区域时生成 WebPartAdding 事件。 |
| OnWebPartClosed | 生成 WebPartClosed 事件以指示 Web Parts 控件从 Web 页面中移除。 |
| OnWebPartClosing | 在 Web Parts 或服务器控件从 Web 页面中移除时生成 WebPartClosing 事件。 |
| OnWebPartDeleted | 在 Web Parts 控件从 Web 页面永久删除后生成 WebPartDeleted 事件。 |
| OnWebPartDeleting | 引发 WebPartDeleting 事件，该事件指示动态 WebPart 控件（或包含在 WebPartZoneBase 区域中的服务器或用户控件）正在被删除的过程中。 |
| OnWebPartMoved | 在 Web Parts 控件移动到 Web 页面上的另一个位置后生成 WebPartMoved 事件。 |

