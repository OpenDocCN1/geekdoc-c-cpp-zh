
PageCatalogPart 控件提供已关闭 WebParts 控件的复选框列表。要将这些已关闭的 WebParts 控件再次打开或添加到网页，请选中相应的复选框以及要添加控件的区域，然后单击网页上 PageCatalogPart 控件中的“添加”按钮。

- **ImportCatalog：** 帮助用户导入 WebParts 控件的描述文件（`.WebPart` 文件）。`.WebPart` 文件描述 WebParts 控件的设置，可将这些控件添加到网页上的指定区域。该控件提供浏览和上传 `.WebPart` 文件的功能。

可以通过执行以下步骤，在 Web 窗体的“设计”视图中插入 CatalogZone 控件：

- 1. 单击 **开始→所有程序→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010**。
- 2. 从菜单栏中选择 **文件→新建→网站**。
  此时将出现“新建网站”对话框。
- 3. 在中间的“模板”窗格中选择 **Visual C#→ASP.NET 网站**。
- 4. 将网站名称设置为 **CatalogzoneControl**。
- 5. 单击 **确定** 按钮。
  将创建 **CatalogzoneControl** 应用程序。
- 6. 从工具箱的 **WebParts** 选项卡中拖放 CatalogZone 控件。

在图 ASP-7.2 中，可以看到 CatalogZone 控件已添加到 **Default.aspx** 页面的“设计”视图中：

![](img/9862a98a1a2d3bb14334137965a1ec60_624_0.png)

图 ASP-7.2

了解了 CatalogZone 控件之后，现在我们来学习 WebPartZone 控件。

### 使用 WebPartZone 控件

**WebPartZone** 控件用于描述 WebParts 页面上的一个区域，以便放置 WebParts 或其他控件，如 **标签、文本框**和**图像**控件。放置后，可以根据最终用户的需求重新定位、最大化或最小化这些控件。**WebPartZone** 控件位于 `System.Web.UI.WebControls.WebParts` 命名空间中。

![](img/9862a98a1a2d3bb14334137965a1ec60_626_0.png)

图 ASP-7.3

了解了 WebPartZone 控件之后，现在我们来学习 EditorZone 控件。

### 使用 EditorZone 控件

设计网页后，有时可能需要修改其外观，例如颜色或样式。ASP.NET 4.0 提供 **EditorZone** 控件，它是用于编辑的主要控件之一。**EditorZone** 控件位于 **System.Web.UI.WebControls.WebParts** 命名空间中。它用于编辑 WebParts 页面的外观、格式和结构。还可以使用 **EditorZone** 控件更改 **WebParts** 控件的行为和内容。**EditorZone** 控件包含各种 **EditorPart** 控件，例如 **AppearanceEditorPart** 和 **BehaviorEditorPart** 控件，用于自定义 **WebParts** 页面。

表 7.11 列出了 EditorZone 类的值得注意的公共属性：

| 属性 | 描述 |
|---|---|
| `InstructionText` | 显示区域中的说明文本 |
| `EmptyZoneText` | 获取或设置当区域为空且没有控件时显示的消息文本 |
| `ErrorText` | 获取或设置编辑 UI 中显示错误消息的文本 |
| `HeaderText` | 设置区域标题区域的文本 |

表 7.12 列出了 EditorZone 类的值得注意的公共方法：

| 方法 | 描述 |
|---|---|
| `AddAttributesToRender` | 将提供的超文本标记语言 (HTML) 属性和样式添加到指定的 `System.Web.UI.HtmlTextWriter` 类 |
| `CreateControlStyle` | 创建样式对象，供 WebControl 类用来执行与该样式相关的所有属性 |
| `CreateEditorPartChrome` | 检索对 `EditorPartChrome` 对象的引用，该对象提供位于 `EditorZoneBase` 区域周围的外围 UI 元素（如边框、标题和图标） |
| `CreateEditorParts` | 以页面持久化形式创建区域模板中指定的所有 `EditorPart` 控件 |
| `InvalidateEditorParts` | 移除与 `EditorZoneBase` 区域关联的所有 `EditorPart` 控件 |
| `Close` | 结束修改 Web 部件控件的过程，并返回网页的浏览模式 |
| `RenderVerb` | 向 `ToolZone` 控件提供一个谓词 |
| `RenderVerbs` | 提供在区域级别应用的谓词 |

表 7.13 列出了 EditorZone 类的值得注意的公共事件。

| 事件 | 描述 |
|---|---|
| `DataBinding` | 在要计算控件的数据绑定表达式时调用 |
| `Disposed` | 在控件已被释放时调用 |

可以通过执行以下步骤，在 Web 窗体的“设计”视图中插入 EditorZone 控件：

- 1. 单击 **开始→所有程序→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010**。
- 2. 从菜单栏中选择 **文件→新建→网站**。
  此时将出现 **新建网站** 对话框。
- 3. 在中间的模板窗格中选择 **Visual C#→ASP.NET 网站**。
- 4. 将网站名称设置为 **EditorzoneControl**。
- 5. 单击 **确定** 按钮。
  将创建 **EditorzoneControl** 应用程序。
- 6. 从工具箱的 WebParts 选项卡中拖放 EditorZone 控件。

在图 ASP-7.4 中，可以看到 **EditorZone** 控件已添加到 **Default.aspx** 页面的“设计”视图中：

![](img/9862a98a1a2d3bb14334137965a1ec60_627_0.png)

了解了 EditorZone 控件之后，现在我们来学习 ConnectionsZone 控件。

### 使用 ConnectionsZone 控件

**ConnectionsZone** 控件允许将 **WebParts** 控件动态地相互连接。**ConnectionsZone** 控件位于 `System.Web.UI.WebControls.WebParts` 命名空间中。**ConnectionsZone** 控件提供一个用户界面，用于与启用了此类动态连接的 **WebParts** 控件建立连接。

表 7.14 列出了 ConnectionsZone 类的值得注意的公共属性：

| 属性 | 描述 |
|---|---|
| `ConfigureConnectionTitle` | 获取或设置由 ConnectionsZone 控件创建的连接 UI 的标题文本。 |
| `ConfigureVerb` | 获取对 WebPartVerb 对象的引用。可以使用此引用打开连接 UI 中的配置视图。 |
| `ConnectToConsumerText` | 获取或设置用户可以单击以选择用于连接的消费者控件的超链接文本。 |
| `ConnectToConsumerTitle` | 获取或设置连接 UI 中某一节的标题文本，用户可在该节中选择要与其他 WebParts 连接的消费者控件。 |
| `ConnectVerb` | 获取对 WebPartsVerb 对象的引用，以允许两个 WebParts 控件与其他 WebParts 连接。 |
| `GetText` | 获取或设置连接 UI 中消费者名称之前显示的文本。该消费者从提供者检索数据。 |
| `CancelVerb` | 检索对 WebPartsVerb 对象的引用，该对象使用户能够取消建立连接的过程。 |
| `CloseVerb` | 检索对 WebPartsVerb 对象的引用，该对象使用户能够关闭连接 UI。 |
| `DisconnectVerb` | 获取对 WebPartsVerb 对象的引用，该对象使用户能够断开两个已连接的 WebPart 控件。 |
| `ProvidersInstructionText` | 获取或设置连接已存在时连接 UI 的提供者部分中包含的说明文本。 |
| `SendText` | 获取或设置连接 UI 中提供者名称之前显示的文本。该提供者向消费者发送数据。 |
| `ProvidersTitle` | 获取或设置连接已存在时连接 UI 的提供者部分中包含的标题文本。 |
| `SendToText` | 获取或设置连接 UI 中提供者向其发送数据的消费者名称之前显示的文本。 |

表 7.15 列出了 ConnectionsZone 类的值得注意的公共事件：

| 事件 | 描述 |
|---|---|
| `DataBinding` | 在要计算控件的数据绑定表达式时调用 |
| `Disposed` | 在控件已被释放时调用 |

