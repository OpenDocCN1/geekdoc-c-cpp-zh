

你还可以通过在 Default.aspx 页面的 `<form>` 元素中插入以下代码来添加 WebPartZone 控件：

```
```aspx
<asp:WebPartZone ID="WebPartZone1" runat="server">
</asp:WebPartZone>
```
```

> **注意**
> 
> WebPartZone 控件还包含 `<ZoneTemplate>` 元素，该元素用于存储其他服务器控件，例如 Label 或 Textbox。

WebPartZone 控件是通过使用 .NET Framework 类库中的 WebPartZone 类创建的。该类的大部分功能都继承自基类 WebZone 和 WebPartZoneBase。WebPartZone 类位于 System.Web.UI.WebControls.WebParts 命名空间中。WebPartZone 类的命名空间层次结构如下：

```
```text
System.Object
    System.Web.UI.Control
        System.Web.UI.WebControls.WebControl
            System.Web.UI.WebControls.CompositeControl
                System.Web.UI.WebControls.WebParts.WebZone
                    System.Web.UI.WebControls.WebParts.WebPartZoneBase
                        System.Web.UI.WebControls.WebParts.WebPartZone
```
```

你可以使用 WebPartZone 类的各种属性和方法来使用 WebPartZone 控件。WebPartZone 类的属性允许你设置 WebPartZone 控件在网页上的外观和行为。WebPartZone 控件是向网页添加 Web Parts 控件的主要控件。你可以在 WebPartZone 控件中添加服务器控件，这些控件可以添加到网页中。

创建 WebPartZone 控件的语法如下所示：

```
```aspx
<WebPartZone <object name>>
```
```

使用 .NET Framework 类库，WebPartZone 类的声明如下：

```
```csharp
public class WebPartZone : WebPartZoneBase
```
```

WebPartZone 类值得注意的方法列于表 16.20 中：

| 方法 | 描述 |
|---|---|
| CreateWebPartChrome | 使派生区域能够为区域中 Web Parts 控件的外观替换自定义 WebPartChrome 对象 |
| EditWebPart | 启动在区域中编辑所选 Web Parts 控件的过程 |
| GetInitialWebParts | 重写抽象基方法并检索区域模板中包含的静态 WebPart 控件的初始值集合 |
| MinimizeWebPart | 最小化区域中选定的 Web Parts 控件 |
| OnCreateVerbs | 引发 CreateVerbs 事件 |
| RenderDropCue | 提供 UI 元素以指示 Web Parts 控件在区域内被拖放的位置 |
| RestoreWebPart | 将所选的最小化 Web Parts 控件恢复到正常状态 |

WebPartZone 类值得注意的属性列于表 16.21 中：

| 属性 | 描述 |
|---|---|
| AllowLayoutChange | 确定是否可以修改 Web Parts 控件的布局。该属性还允许你为 Web Parts 控件指定布局。 |

## 表 16.21：WebPartZone 类的注目属性

| 属性 | 描述 |
| --- | --- |
| DragDropEnabled | 检索一个值，指示是否可以将 Web Parts 控件拖放进或拖出区域。 |
| EditVerb | 获取对 WebPartVerb 类对象的引用以更改 Web Parts 控件 |
| ExportVerb | 获取对 WebPartVerb 类对象的引用以导出 Web Parts 控件的 XML 定义。 |
| HelpVerb | 获取对 WebPartVerb 类对象的引用以访问有关在 WebPartZone 控件中使用 Web Parts 控件的帮助内容。 |
| LayoutOrientation | 确定 WebPartZone 控件中的控件是水平对齐还是垂直对齐。该属性还允许你指定 WebPartZone 控件中 Web Parts 控件的对齐方式。 |
| MenuCheckImageStyle | 确定用作 WebPartZone 控件中 Web Parts 控件的动词菜单中复选标记的图像样式。 |
| MenuCheckImageUrl | 确定或指定用作 WebPartZone 控件中 Web Parts 控件的动词菜单复选标记的图像的 URL。 |
| MenuLabelHoverStyle | 获取或指定当鼠标指针悬停在其上时用于更改动词菜单标签外观的样式。 |
| MenuLabelStyle | 获取或指定应用于在 WebPartZone 控件中 Web Parts 控件标题栏中显示的动词菜单标签的样式。 |
| MenuLabelText | 获取或指定在 WebPartZone 控件中 Web Parts 控件标题栏中显示的动词菜单的标签。 |
| MenuPopupImageUrl | 获取或指定表示 WebPartZone 控件中 Web Parts 控件标题栏中动词菜单的图像的 URL。 |
| MenuPopupStyle | 获取应用于 WebPartZone 控件中 Web Parts 控件的动词菜单的样式。 |
| MenuVerbHoverStyle | 获取应用于当鼠标指针悬停在动词上时更改动词菜单中显示的动词外观的样式。 |
| MenuVerbStyle | 获取 WebPartZone 控件中 Web Parts 控件的动词菜单中动词的样式。 |
| MinimizeVerb | 获取对 WebPartVerb 类对象的引用以最小化 WebPartZone 控件中的 Web Parts 控件。 |
| RestoreVerb | 获取对 WebPartVerb 类对象的引用以将 Web Parts 控件的大小设置为正常。 |
| SelectedPartChromeStyle | 获取 WebPartZone 控件中 Web Parts 控件的样式。 |
| ShowTitleIcons | 确定在 WebPartZone 控件中 Web Part 控件的标题栏中显示的图标。 |
| TitleBarVerbButtonType | 确定用于 Web Parts 控件标题栏中动词的按钮类型。 |
| TitleBarVerbStyle | 获取 Web Parts 控件标题栏中显示的动词的样式。 |
| VerbButtonType | 检索或设置与 Web Parts 控件标题栏中动词关联的按钮类型。 |
| WebPartChrome | 检索对 WebPartChrome 控件的引用，该控件确定区域中 Web Parts 控件的外围渲染。 |

表 16.21：WebPartZone 类的注目属性

| 属性 | 描述 |
|---|---|
| WebParts | 检索区域内的 Web Parts 控件集合。 |
| WebPartVerbRenderMode | 检索或设置一个值，指示动词应在区域中 Web Parts 控件上如何呈现。 |
| ZoneTemplate | 检索或设置包含网页中控件的模板引用。 |

WebPartZone 类值得注意的事件列于表 16.22 中：

## 表 16.22：WebPartZone 类的注目事件

| 事件 | 描述 |
|---|---|
| CreateVerbs | 当为派生自 WebPartZoneBase 类的区域创建动词时引发 |

## CatalogZone 控件

你可以通过添加目录功能来个性化网站，该功能允许你高效地管理 Web Parts 控件。你可以通过向其中添加 CatalogZone 控件来创建启用目录的网页。

CatalogZone 控件有助于创建 Web Parts 控件的目录。这允许用户轻松地在网页上添加或更新控件。要向网页添加 CatalogZone 控件，只需从工具箱将 CatalogZone 控件拖放到 Default.aspx 页面的设计视图中即可。图 16.12 显示了设计视图中的 CatalogZone 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_814_0.png)

图 16.12：显示 CatalogZone 控件

你还可以通过在 Default.aspx 页面的 `<form>` 元素中插入以下代码来添加 CatalogZone 控件：

```
<asp:CatalogZone ID="CatalogZone1" runat="server">
</asp:CatalogZone>
```

当你向网页添加 CatalogZone 控件时，网页上的“选择模式”列表中会出现一种新的模式，称为目录模式。CatalogZone 控件在网页处于目录模式时显示，允许用户在其包含的网页上添加控件，也称为模板控件。因此，控件需要一个模板部分，该部分由 CatalogZone 控件部分内的 `<ZoneTemplate>` 元素表示。在模板部分内部，你可以放置多个 CatalogPart 控件，其中每个 CatalogPart 控件都作为可添加到网页上的服务器控件的容器控件。CatalogZone 控件是 CatalogZone 类的对象。请记住，只有在将控件的显示模式更改为 CatalogDisplayMode 模式后，才能在网页上查看 CatalogZone 控件。

CatalogZone 控件是通过使用 .NET Framework 类库中的 CatalogZone 类创建的。该类位于 System.Web.UI.WebControls.WebParts 命名空间中。

CatalogZone 类的继承层次结构如下：

```
System.Object
System.Web.UI.Control
```
