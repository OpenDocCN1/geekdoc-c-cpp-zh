
`WebPartZone` 是通过使用 .NET Framework 类库中的 `WebPart` 类创建的。该类的大部分功能继承自基 `WebZone` 和 `WebPartBase` 类。`WebPartZone` 类位于 `System.UI.WebControls.WebParts` 命名空间。`WebPart` 的命名空间层次结构如下：

```
System.Object
  System.UI.Control
    System.UI.WebControls.WebControls.CompositeControl
      System.UI.WebControls.WebParts.WebPartBase
        System.UI.WebControls.WebParts.WebPartZone
```

你可以使用 `WebPartZone` 类的各种属性和方法来管理 `WebPartZone` 控件。

`WebPartZone` 类的属性允许你设置 Web 页面上 `WebPartZone` 控件的外观和行为。`WebPartZone` 是在 Web 页面上添加 Web Parts 主要控件。你可以在 `WebPartZone` 中添加多个控件。

创建 `WebPartZone` 的语法如下：

使用 .NET Framework 类库，`WebPart` 类的声明如下：

```
public class WebPart : WebPartBase
```

表 13.20 列出了 `WebPart` 类中值得注意的方法：

| 方法 | 描述 |

|---|---|

| `CreateWebPartChrome` | 允许区域对自定义 `WebPartChrome` 对象进行样式设置，使其符合区域内 Web Parts 控件的外观 |

| `EditWebPart` | 启动区域内选定 `WebPart` 控件的编辑过程 |

| `GetInitialWebParts` | 抽象基方法并检索区域模板内包含的初始静态 `WebPart` 控件集 |

| `MinimizeWebPart` | 最小化区域内选定的 `WebPart` 控件 |

| `OnCreateEvent` | 触发 `CreateWebPart` 事件 |

表 13.20：`WebPartZone` 类的值得注意的方法

| 方法 | 描述 |

|---|---|

| `RenderDropCue` | 提供 UI 元素，指示 `WebPart` 控件在区域内拖放时放置的位置 |

| `RestoreWebPart` | 将最小化的 Web Parts 控件恢复到正常状态 |

表 13.21 列出了 `WebPartZone` 类中值得注意的属性：

表 13.21：`WebPartZone` 类的值得注意的属性

| 属性 | 描述 |

|---|---|

| `AllowLayoutChange` | 决定是否可以修改 Web Parts 控件的布局。属性还允许你为 Web Parts 指定布局。 |

| `DragEnabled` | 获取一个值，指示 `WebPart` 控件是否可以被拖放到区域外。 |

| `EditVerb` | 获取 `WebVerb` 类对象的引用，将 `WebPart` 控件转换为菜单控件。 |

| `ExportVerb` | 获取 `WebVerb` 类对象的引用，以导出 Web 控件的 XML 定义。 |

| `HelpVerb` | 获取 `WebVerb` 类对象的引用，用于在 `WebPartZone` 中使用 `WebPart` 控件的帮助内容。 |

| `LayoutOrientation` | 决定 `WebPartZone` 中的控件是水平对齐还是垂直对齐。这还允许你指定 `WebPartZone` 中 Web Parts 控件的对齐方式。 |

| `MenuCheckStyle` | 决定用于菜单控件中 Web Parts 控件动词（verb）检查标记的图像。 |

| `MenuCheckImageUrl` | 确定或指定 `WebPartZone` 中 Web 控件动词检查标记的图像 URL。 |

| `LabelHoverStyle` | 确定或指定当鼠标指针悬停在动词标签上时，用于更改标签外观的样式。 |

| `LabelStyle` | 确定或指定应用于 `WebPartZone` 中 Web 控件标题栏显示的动词菜单标签的样式。 |

| `LabelText` | 确定或指定在 `WebPartZone` 中 Web Parts 标题栏显示的动词菜单标签。 |

| `PopupImageUrl` | 确定或指定 `WebPartZone` 控件中 Web 控件标题栏中表示动词菜单的图像 URL。 |

| `PopupStyle` | 应用于 `WebPartZone` 中 Web 控件动词的样式。 |

| `MenuHoverStyle` | 确定当鼠标指针悬停在显示的动词上时，用于更改其外观的样式。 |

| `MenuBorderStyle` | 确定 `WebPartZone` 中 Web 控件菜单动词的边界样式。 |

| `MinimizeVerb` | 获取 `WebVerb` 类对象的引用，将 `WebPartZone` 中的 Web Parts 控件最小化。 |

| `RestoreVerb` | 获取 `WebVerb` 类对象的引用，将 `WebPartZone` 中的 Web Parts 控件的大小恢复为正常。 |

| `SelectedChromeStyle` | 确定 `WebPartZone` 中 Web Parts 控件的样式。 |

| `ShowTitleIcons` | 决定 `WebPartZone` 中 Web 控件标题栏中是否显示图标。 |

| `TitleBarType` | 决定标题栏中使用的按钮类型。 |

| `WebPartChrome` | 获取区域 chrome 对象的引用。 |

| `WebParts` | 获取区域内的 Web Parts 集合。 |

| `WebPartRenderMode` | 确定或设置一个指示如何渲染动词（verbs）的值。 |

| `ZoneTemplate` | 获取或设置包含控件的模板。 |

`CatalogZone` 类的继承层次如下：

```
System.Object
System.web.UI.Control
System.web.UI.Controls.CompositeControl
System.web.UI.Controls.WebParts.CatalogZoneBase
System.web.UI.Controls.WebParts.ToolZone
System.web.UI.Controls.WebParts.CatalogZoneBase
System.web.UI.Controls.WebParts.CatalogZone
```

表 13.23 列出了 `CatalogZone` 类中值得关注的方法：

表 13.23：`CatalogZone` 的常用方法

| 方法 | 描述 |

| --- | --- |

| `CreateCatalogChrome` | 创建用于渲染区域内 `CatalogPart` 控件 UI 元素的 `CatalogChrome` 对象。 |

| `CreateCatalogParts` | 创建在 `CatalogZone` 控件中声明的所有 `CatalogParts` 的 实例。 |

| `InvalidateCatalogParts` | 删除所有与 `CatalogZoneBase` 区域相关的 `CatalogPart` 控件。 |

| `LoadData` | 当 Web 页面回传到 Web 服务器时，确定在 `CatalogZone` 控制中选中的 Web Parts 控件。选中的 `WebPart` 控件会被添加到 Web 页面中。 |

| `RenderCatalogPartLinks` | 创建 `CatalogZone` 基础区域中每个 `CatalogPart` 控件的链接。 |

表 13.24 列出了 `CatalogZone` 类中值得关注的属性：

表 13.24：`CatalogZone` 类的常用属性

| 属性 | 描述 |

| --- | --- |

| `SelectedCatalogPartID` | 获取或初始化一个字符串，用于识别区域中当前中的 `CatalogPart` 控件。 |

| `SelectedPartStyle` | 获取一个包含区域中当前选中 `CatalogPart` 控件样式属性的对象。 |

| `SelectTargetText` | 获取或设置 Catalog UI 中服务器控件的文本。这允许用户选择用于添加控件的区域。 |

| `ShowCatalogIcons` | 获取或设置一个值，指示 `CatalogZone` 控件中的控件是否显示其图标。 |

## 声明式 CatalogCatalogPart 控件

`DeclarativeCatalogPart` 控件是与 `CatalogZone` 控件一起使用的三个控件之一（另外两个控件是 `PageCatalogPart` 和 `ImportCatalogPart`）。该控件用于修改 Web 页的功能。当网站处于 `CatalogDisplayMode` 模式时，此控件会显示 Web Parts 和服务器控件的列表。用户可以从此 `CatalogZone` 向 Web 页面添加控件。

`DeclarativeCatalogPart` 控件是 `DeclarativeCatalogPart` 类的对象。你可以通过在 `Default.aspx` 页的设计视图中将控件从工具箱拖放到 `CatalogZone` 控件，向 `Default.aspx` 页添加 `DeclarativeCatalogPart` 控件。在 Web 页面上添加 `DeclarativeCatalogPart` 控件时，确保 Web 页面包含 `CatalogZone`。

# 第 13 章：ASP.NET 4.5 中的登录和 Web Parts 控件

图 13.12 显示了设计视图中包含 `CatalogZone` 的 `DeclarativeCatalogPart`：

![](img/17af790174c480761404624aeed9b30b_633_0.png)

图 13.12：通过使用 `Default.aspx` 中 `<element>` 标签中的代码显示 `DeclarativeCatalogPart` 控件。

```
<asp:DeclarativeCatalog ID="CatalogZone" run="server">
  <ZoneTemplate>
    <asp:DeclarativeCatalogPart ID="DeclarativeCatalogPart1" run="server">
    </asp:DeclarativeCatalogPart>
  </ZoneTemplate>
</asp:DeclarativeCatalog>
```

`DeclarativeCatalogPart` 是使用 .NET 框架类中的 `DeclarativeCatalogPart` 类创建的。该类可用 `System.Web.UI.WebControls` 命名空间。该类的继承层次如下：

- object

  - `System.web.UI.WebControls.WebControl`

    - `System.web.UI.WebControls.Panel`

      - `System.web.UI.WebControls.WebParts`

        - `System.web.UI.WebControls.WebParts.DeclarativeCatalogPart`

          - `System.web.UI.WebControls.WebParts.DeclarativeCatalogPart` class

现在，通过使用 `DeclarativeCatalogPart` 控件识别声明 `DeclarativeCatalogPart` 控件的语法。

声明 `DeclarativeCatalogPart` 控件的语法如下：

你可以创建一个或多个服务器控件并将它们添加到 `DeclarativeCatalogPart` 控件的 `WebPartList` 中。要实现此点，你必须继承 `WebPartsListUserControl` 类来创建用户控件，优先使用服务器控件，因为你可以通过使用相同的用户控件在网站的多个页面上显示该控件。当用户控件中的 Web Parts 被创建时，`DeclarativeCatalogPart` 控件会自动更新所有与用户相关的所有目录。

表 13.25 列出了 `DeclarativeCatalogPart` 类中值得关注的方法：

| 表 13.25：`DeclarativeCatalogPart` 类的常用方法 | 描述 |

| --- | --- |

| `ApplyStyle` | 将指定的样式应用于 `WebPart` 控件的元素上。 |

| `GetAvailableWebPartDescriptions` | 提供 Web 页面目录中所包含 `WebPart` 控件的详细信息（如 ID 和其他属性的值）。 |

| `CopyBaseAttributes` | 将指定的服务器控件的 `AccessKey`、`Enabled`、`ToolTip`、`TabIndex` 和 `Attributes` 复制到调用此方法的服务器控件中。这些属性及其值作为参数指定。 | 提供 `Panel` 控件的起始标签，以便添加到一个可以添加服务器控件的面板上。 |

| `RenderTag` | 提供 `Panel` 控件的结束标签，指示面板的结束。 |

| `GetWebPart` | 根据描述提供 Web Parts 控件的引用。 |

| `MergeStyle` | 将样式元素添加到 Web Parts 控件。 |

表 13.26 列出了 `DeclarativeCatalogPart` 类值得关注的属性：

# 表 13.26：`DeclarativeCatalogPart` 类常用属性

| 属性 | 描述 |

| --- | --- |

| `AccessKey` | 代表你可以访问 `DeclarativeCatalogPart` 控件的快捷键。 |

| `BackColor` | 指定或确定 `WebPart` 控件的背景颜色。 |

| `Chrome` | 确定 `WebPart` 控件的边界。 |

| `ChromeState` | 确定 `WebPart` 控件是最小化还是正常状态。 |

| `ControlStyle` | 确定 `WebPart` 控件的样式。 |

| `ControlStyleCreated` | 确定是否为 `WebPart` 控件指示了样式。 |

| `HasAttributes` | 确定是否设置了属性 |

| `WebPartsControlType` | 指定或确定包含目录 Web 的用户控件路径。 |

| `WebPartsTemplate` | 指定或确定包含目录 `WebPart` 控件的模板引用。 |

| `BorderWidth` | 指定或确定 `WebPart` 控件边界宽度。 |

| `CssClass` | 指定或确定 `WebPart` 控件的级联样式表 (CSS) 类。 |

| `Font` | 确定 `WebPart` 控件的字体。 |

| `ForeColor` | 指定 `WebPart` 控件的前景色。 |

| `GroupingText` | 为控件中的控件指定标题。 |

| `Height` | 指定 `WebPart` 控件的高度。 |

| `HorizontalAlign` | 确定 `Panel` 控件中内容的水平对齐方式。 |

| `ScrollBars` | 确定滚动条设置，如其外观和位置。 |

| `TabIndex` | 确定 `WebPart` 控件的选项索引。 |

| `ToolTip` | 指定悬停在 `WebPart` 控件上显示的文本。 |

| `Width` | 指定 `WebPart` 控件的宽度。 |

| `Wrap` | 确定控件中显示的文本是否换行。 |

| `BackimageURL` | 指定控件中显示的图像的 URL。 |

> 注意

这些属性在 Web Parts 控件渲染 `DeclarativeCatalogPart` 控件时不会被使用。重写该属性是为了防止其出现在 Visual Studio 2012 设计工具中。

## PageCatalogPart 控件

`PageCatalogPart` 控件由 `CatalogZone` 控件控制，用于为 Web 页面的目录部分添加特定功能。该控件允许用户恢复之前删除的 `WebPart` 控件的

## 第 13 章：ASP.NET 4.5 中的登录与 Web Parts 控件

这是恢复已删除的 Web Parts 控件的唯一方法。`PageCatalogPart` 控件为每个删除的 Web Part 控件对应的目录区域控件添加了一个复选框列表。要在 Web页面上恢复这些控件，用户只需选择正确的复选框以及要添加 Web Parts 控件的 Web 部分，然后点击添加（Add）按钮即可。

要将 `PageCatalogPart` 控件添加到 `CatalogZone` 控件中，请从 `Default.aspx` 页面的设计视图中将工具箱中的 `PageCatalogPart` 控件拖放到 `CatalogZone` 控件。图 13.13 显示了设计视图中 `CatalogZone` 控件内的 `PageCatalogPart`：

![](img/17af790174c480761404624aeed9b30b_635_0.png)

图 13.13：设计 `PageCatalogPart` 控件

你也可以使用 `Default.aspx` 页面的 `code` 元素添加 `PageCatalogPart` 控件：

```asp
<asp:CatalogZone Id="CatalogZone1" runat="server" Height="183px" width="318px">
  <ContentTemplate>
    <asp:PageCatalogPart Id="CatalogPart1" runat="server">
  </ContentTemplate>
</asp:CatalogZone>
```

`PageCatalog` 控制是 `PageCatalog` 类的对象。该类与 `PageCatalog` 类关联，它提供了与 `CatalogZone` 类提供的相同的事件、方法和属性。

`PageCatalog` 控件的继承层次结构如下：

- *System.object*

  - `System.web.UI.Control`

    - `System.web.UI.WebControls.Control`
