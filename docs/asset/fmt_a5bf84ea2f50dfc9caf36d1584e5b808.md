
- `System.web.UI.WebControls.Panel`
  - `System.web.UI.WebControls.WebParts.Part`
  - `System.web.UI.WebControls.WebParts.PageCatalogPart`
    - `System.web.UI.WebControls.WebParts.PageCatalogPart`

你可以声明 `PageCatalogPart` 类以将其添加到 `PageCatalog` 控件中。声明 `PageCatalogPart` 类的语法如下：

```csharp
public class PageCatalogPart:PageCatalogPart
```

## ImportCatalogPart 控件

`ImportCatalogPart` 控件将带有预定义设置的 Web Part 描述文件导入到 Web 页面。这个 `ImportCatalogPart` 控件是第三种（另外两个使用的是 `DeclarativeCatalogPart` 和 `PageCatalogPart`），它与 `CatalogZone` 控件配合使用，为 Web 页面的目录部分添加特定功能。该控件提供了选项，允许你浏览并上传导入 WebPart 所需描述文件。

`ImportCatalogPart` 控件是 `ImportCatalogPart` 类的对象。

> 描述文件是一个带有 `.WebPart` 扩展名的 XML 文件。它包含属性、状态数据以及对程序集或源文件的引用。如果 Web Part 控件的属性经过了自定义，这些属性在描述文件中的值也会相应改变。

### 深度解析

你可以通过从 `Default.aspx` 页面的设计视图将工具箱中的 `ImportCatalogPart` 控件拖放到 `CatalogZone` 控件来向 Web 页面添加 `ImportCatalogPart` 控件。图 13.14 显示了设计视图中 `CatalogZone` 控件内的 `ImportCatalogPart` 控件：

![](img/17af790174c480761404624aeed9b30b_636_0.png)

图 13.14：导入 `ImportCatalogPart` 控件

你也可以通过在 `Default.aspx` 页面的 `<embed>` 元素中使用以下代码添加 `ImportCatalogPart` 控件。

```asp
<asp:CatalogZone ID="CatalogZone" runat="server">
  <Template>
    <asp:ImportCatalogPart ID="ImportCatalogPart" runat="server" />
  </Template>
</asp:CatalogZone>
```

`ImportCatalogPart` 控件使用 .NET Framework 类库中的 `ImportCatalogPart` 类创建。该位于 `System.Web.UI.WebControls.WebParts` 命名空间中。`ImportCatalogPart` 类的继承关系如下：

```text
System.Object
System.Web.UI.Control
System.Web.UI.WebControls.Control
System.Web.UI.WebControls.WebPartsPart
System.Web.UI.WebControls.WebParts.Part
System.Web.UI.WebControls.WebParts.ImportCatalogPart
```

`ImportCatalogPart` 的语法如下：

`ImportCatalogPart ImportCatalogPart();`

你可以使用 `ImportCatalogPart` 类的各种属性和方法来处理 `ImportCatalogPart` 控件。`ImportCatalogPart` 类的属性允许你指定 Web 页面上区域的外观和行为。`ImportCatalogPart` 控件的属性无法被基类的派生类继承。`ImportCatalogPart` 类的方法列在表 13.2 中。

| 方法 | 说明 |
| --- | --- |
| GetAllWebPartDescriptions | 获取目录中 WebPart 控件的描述 |
| GetWebPart | 根据传递的参数检索 WebPart 控件 |

`ImportCatalogPart` 类的重要属性列在表 13.28 中：

| 属性 | 说明 |
| --- | --- |
| BrowseHelpText | 获取或设置一段文本，提示用户浏览到描述文件的位置 |

## 第 13 章：ASP.NET 4.5 中的登录与 Web Parts 控件

| 表 13.28：ImportCatalog 类的重要属性 |
| --- | | --- |
| 属性 | 说明 |
| ImportedPart | 获取或设置一段文本，提示用户浏览到描述文件的位置 |
| ErrorLabel | 获取或设置一段文本，提示用户浏览到描述文件的位置 |
| UploadButton | 获取或设置一段文本，提示用户浏览到描述文件的位置 |
| UploadText | 获取或设置一段文本，提示用户浏览到描述文件的位置 |

## EditorZone

到目前，你已经对重要的 Parts 有了一些了解。现在，假设你想更改区域的外观。`EditorZone` 控件与 `CatalogZone` 控件配合使用，为 Web 页面的目录部分添加特定功能。该控件提供了选项，允许你浏览并上传导入 WebPart 所需描述文件。`EditorZone` 允许你更改外观。`EditorZone` 控件是 `PageCatalog` 类的对象。

要向 Web 页面添加 `EditorZone` 控件，请从 `Default.aspx` 页面的设计视图将工具箱中的 `EditorZone` 控件拖放到 `CatalogZone` 控件。图 13.15 显示了 `EditorZone`：

![](img/17af790174c480761404624aeed9b30b_637_0.png)

图 13.15：设计 `EditorZone` 控件

你也可以使用 `Default.aspx` 页面的 `code` 元素添加 `EditorZone` 控件：

```asp
<asp:CatalogZone Id="CatalogZone1" runat="server">
  <ContentTemplate>
    <asp:EditorZone Id="EditorZone1" runat="server">
  </ContentTemplate>
</asp:CatalogZone>
```

`EditorZone` 控件使用 .NET Framework 类库中的 `EditorZone` 类创建。该类位于 `System.Web.UI.WebControls.WebParts` 命名空间中。`EditorZone` 类的继承关系如下：

```text
System.Object
System.Web.UI.Control
System.Web.UI.WebControls.Control
System.Web.UI.WebControls.WebPartsPart
System.Web.UI.WebControls.WebParts.Part
System.Web.UI.WebControls.WebParts.ImportCatalogPart
System.Web.UI.WebControls.WebParts.EditorZone
```

`EditorZone` 的语法如下：

`EditorZone EditorZone();`

你可以使用 `EditorZone` 类的各种属性和方法来处理 `EditorZone` 控件。`EditorZone` 类的属性允许你指定 Web 页面上区域的外观和行为。`EditorZone` 控件的属性无法被基类的派生类继承。`EditorZone` 类的方法列在表 13.29 中。

| 方法 | 说明 |
| --- | --- |
| AddAttributesToEditor | 向指定的添加文本标记语言（HTML）属性和样式 |
| CreateBorderStyle | 使用 WebControl 创建样式对象 |
| CreateEditorPartChrome | 获取与 EditorZone 相关的 EditorPartChrome 类实例 |
| CreateEditorParts | 创建区域中所有的 EditorParts |
| InvalidateEditorParts | 移除所有的 EditorParts |
| RaisePostBackEvent | 执行与动词相关的操作，或调用事件 |
| RenderBody | 重写区域主体 |
| RenderContents | 提供起始和结束标签之间的区域内容 |
| RenderFooter | 指定控件脚部的动词 |
| RenderHeader | 为头部区域提供特殊渲染 |
| Close | 结束 Web parts 处理 |
| RenderVerb | 为 ToolZone 提供动词 |
| RenderVerbs | 渲染区域级别的动词 |

`EditorZone` 类的重要属性列在表 13.30 中：

| 属性 | 说明 |
| --- | --- |
| ApplyVerb | 获取 WebPart 对象引用，允许修改 Web Part |
| AssociatedDisplayModes | 获取存在 ToolZone 控件时激活的 WebPartDisplayMode 对象 |
| CancelVerb | 获取 WebPart 对象引用，允许取消修改 |
| EditorPartChrome | 获取 EditorPartChrome 类的实例 |
| EditorParts | 获取 EditorZone 中包含的所有 EditorParts |
| UIStyle | 获取包含在内的控件样式属性 |
| EmptyZoneText | 设置或获取一条消息文本，当区域为空时显示 |
| EmptyZoneTextStyle | 获取空区域的样式属性 |
| ErrorStyle | 获取 EditorZone 控件的样式属性 |

# 第 13 章：ASP.NET 4.5 中的登录与 Web Parts 控制

| 表格 13.30：EditorZone 类的重要属性 |
| 属性 | 描述 |
| --- | --- |
| ErrorText | 获取或设置在编辑 UI 中显示错误消息的文本 |
| FooterStyle | 获取区域脚区域的样式属性 |
| HeaderCloseVerb | 获取 ToolZone 头部中 WebPart 对象的引用，以控制该控件 |
| HeaderStyle | 获取头部区域的样式属性 |
| HeaderText | 获取或设置区域区域的文本 |
| HeaderVerb | 获取 ToolZone 中所有显示头部的样式属性 |
| InstructionText | 获取或设置如何使用 ToolZone 控件的说明文本 |
| InstructionTextStyle | 获取在 ToolZone 顶部显示的文本的属性 |
| LabelStyle | 获取 ToolZone 中标签的样式属性 |
| OKVerb | 获取控件的引用并隐藏编辑 UI |
| Padding | 获取或设置包含 Web Parts 的表格中的单元格内边距 |
| Chrome | 获取区域内 Web Parts 边界的样式属性 |
| PartType | 获取或设置 Web Parts 的类型 |
| PartStyle | 获取 Web Parts 边界和内容的样式属性 |
| TitleStyle | 获取 Web Parts 标题的样式属性 |
| ButtonType | 获取或设置表示区域的按钮 |
| VerbStyle | 获取 Web Parts UI 的特征 |
| ZoneTemplate | 提供向 EditorZone 添加子元素的模板 |

# LayoutEditorPart 控件

你可以使用 `LayoutEditorPart` 控件为 Web Parts 创建功能完整的编辑器，它们关联了各自的 `LayoutEditorPart` 控件。要更改 Web Parts 的布局，只需在关联的 `LayoutEditorPart` 控件中进行。

`LayoutEditorPart` 控件在 Web Part 处于编辑模式时可见。在此模式下，你可以选择并更改 Web Part 的属性。`LayoutEditorPart` 控件提供了以下选项：

- Chrome Style - 定义 Web Parts 控件的样式，可以最小化或最大化。
- Zone - 设置要修改的 Web Part 控件所在的 WebPartZone。
- Zone Index - 设置 Web Parts 控制的位置。

你必须在持久化格式中使用 `LayoutEditorPart` 控件，以便在浏览器会话之间保留值。要实现这一点，你需要在 `<ZoneTemplate>` 元素内部声明 `<asp:LayoutEditorPart>`。向 Web 页面添加 `LayoutEditorPart` 控件，请从工具箱拖放 `LayoutEditorPart` 控件以修改 `Default.aspx` 的 Web Parts。图 13.16 显示了设计视图中 `EditorZone` 控件内的 `LayoutEditorPart` 控件：

![](img/17af90174c48076140462ed9b30b0.png)

你也可以在 `Default.aspx` 页的 `<form>` 元素中使用以下代码使用 `LayoutEditorPart` 控件：

```
 <asp:EditorZone ID="EditorZone" runat="server">
    <ZoneTemplate>
        <asp:LayoutEditorPart ID="LayoutPart1" runat="server" />
    </ZoneTemplate>
</asp:EditorZone>
```

`LayoutEditorPart` 控件是 `LayoutEditorPart` 类的对象。

> 注意
>
> 如果你在 `EditorZone` 控件以外的任何区域放置 `LayoutEditorPart` 控件，设计器将报错。

`LayoutEditorPart` 控件是由 .NET 库中的 `LayoutEditorPart` 类创建的。`LayoutEditorPart` 类允许你修改关联 Web Parts 的布局。该类位于 `System.Web.UI.WebParts` 命名空间中。`LayoutEditorPart` 类的继承层次如下：

```
System.Object
System.Web.UI.WebControls.WebControl
System.Web.UI.WebControls.Panel
System.Web.UI.WebParts.Control
System.Web.UI.WebParts.LayoutEditorPart
System.Web.UI.WebParts.LayoutEditorPart
```

`LayoutEditorPart` 控件与 `LayoutEditorPart` 类关联。该类采用各种方法执行任务，例如对 Web Parts 控件应用更改以及判断两个实例是否相等。`LayoutEditorPart` 类的方法如表 13.31 所示：

| 表 13.31：LayoutEditorPart 类的方法 |
| 方法 | 描述 |
| --- | --- |
| ApplyChanges | 使用 LayoutEditorPart 控件中的更改更新关联的 Web Part 属性 |
| SyncChanges | 从 Web Part 控件获取值并分配给关联的 LayoutEditorPart 控件 |

现在，让我们查看继承自属性。该类作为基类提供了一系列属性和方法，并继承了来自 `Control` 和 `WebControl` 等类的某些属性。`LayoutEditorPart` 类继承的各种属性包括 `Font`、`Enabled` 和 `Style`。`LayoutEditorPart` 类的重要属性如表 13.32 所示：

| 表格 13.32：LayoutEditorPart 类的重要属性 |
| 属性 | 描述 |
| --- | --- |
| DefaultButton | 获取或设置包含在 Panel 控件中的默认按钮的 ID |
| Display | 获取一个值，指定当关联的 Web Parts 处于编辑模式时是否应该显示 LayoutEditorPart 控件 |
| Title | 获取或指定作为 LayoutEditorPart 控件标题的字符串 |

# AppearanceEditorPart 控件

`AppearanceEditorPart` 控件允许用户编辑与页面上 Web Parts 控件外观相关的属性。此控件位于 `EditorZone` 中，仅在选择 Web Parts 控件进行编辑时可见。`AppearanceEditorPart` 控件上显示以下选项：

- Title—指定一个作为 `AppearanceEditorPart` 控件标题的字符串。
- Height—指定 `AppearanceEditorPart` 控件的高度。
- Width—指定 `AppearanceEditorPart` 控件的宽度。
- Chrome Type—选择标题和边界类型（虚线、单线或双线）。
- Direction—选择水平或垂直的内容流方向。
- Hidden—隐藏或显示 `AppearanceEditorPart` 控件。

要向 `EditorZone` 控件添加 `AppearanceEditorPart` 控件，请从工具箱拖放该控件到 `Default.aspx` 的设计视图中。图 13.17 显示了在 `EditorZone` 控件中的 `AppearanceEditorPart`：
