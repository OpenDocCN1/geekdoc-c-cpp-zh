

> NOTE
> 这些属性在渲染 DeclarativeCatalogPart 控件时不会被 Web Parts 控件集使用。该属性仅被覆盖以防止其出现在 Microsoft Visual Studio 2010 设计器工具中。

## The PageCatalogPart Control

PageCatalogPart 控件与 CatalogZone 控件一起使用，为 Web 页面的目录部分添加特定功能。此控件允许用户恢复先前已删除的 WebPart 控件。该控件是用户恢复已删除 Web Parts 控件的唯一方式。PageCatalogPart 控件会在目录区域控件中为每个已删除的 Web Parts 控件添加一个复选框列表。要在 Web 页面上恢复这些控件，用户只需选择所需的复选框和 Web part 区域，然后单击 Add 按钮即可将 Web Parts 控件添加到该区域。

要将 PageCatalogPart 控件添加到 CatalogZone 控件，请从工具箱将 PageCatalogPart 控件拖放到 Default.aspx 页面的设计视图中的 CatalogZone 控件。图 16.14 显示了设计视图中 CatalogZone 控件内的 PageCatalogPart 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_818_0.png)

**Figure 16.14: Displaying the PageCatalogPart Control**

```
<asp:CatalogZone ID="CatalogZone1" runat="server" Height="183px" width="318px">
<ZoneTemplate>
<asp:PageCatalogPart ID="PageCatalogPart1" runat="server" Height="198px" />
</ZoneTemplate>
</asp:CatalogZone>
```

PageCatalogPart 控件是 PageCatalogPart 类的对象。此控件与 PageCatalogPart 类关联，该类提供的事件、方法和属性与 CatalogZone 类提供的相同。

- System.Object
- System.Web.UI.Control
- System.Web.UI.WebControls.WebControl
- System.Web.UI.WebControls.Panel
- System.Web.UI.WebControls.WebPart
- System.Web.UI.WebControls.WebParts.CatalogPart
- System.Web.UI.WebControls.WebParts.PageCatalogPart

您可以声明 PageCatalogPart 类以添加 PageCatalogPart 控件。声明 PageCatalogPart 类的语法如下所示：

```
PageCatalogPart pagecatalogpart;
```

## The ImportCatalogPart Control

ImportCatalogPart 控件导入 Web Parts 控件或用作 Web Parts 控件的服务器控件的描述文件。这使得服务器控件能够以预先分配的设置添加到 Web 页面。描述文件使用户能够共享 Web Parts 控件的设置。ImportCatalogPart 控件是与 CatalogZone 控件一起使用的第三个控件（另外两个为 DeclarativeCatalogPart 和 PageCatalogPart），用于为 Web 页面的目录部分添加特定功能。此控件为您提供选项，允许您浏览和上传导入 WebPart 控件所需的描述文件。

ImportCatalogPart 控件是 ImportCatalogPart 类的对象。

> **NOTE**
> 
> 描述文件是一个具有 .WebPart 扩展名的 XML 文件。它包含属性值、状态数据以及对程序集或源文件的引用。如果 Web Part 控件的属性已自定义，描述文件也将包含这些属性的值。

您可以通过从工具箱将 ImportCatalogPart 控件拖放到 Default.aspx 页面的设计视图中的 CatalogZone 控件来向 Web 页面添加 ImportCatalogPart 控件。图 16.15 显示了设计视图中 CatalogZone 控件内的 ImportCatalogPart 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_819_0.png)

**Figure 16.15: Displaying the ImportCatalogPart Control**

您也可以通过在 Default.aspx 页面的 <form> 元素中使用以下代码添加 ImportCatalogPart 控件：

```aspx
<asp:CatalogZone ID="CatalogZone1" runat="server">
    <ZoneTemplate>
        <asp:ImportCatalogPart ID="ImportCatalogPart1" runat="server" />
    </ZoneTemplate>
</asp:CatalogZone>
```

ImportCatalogPart 控件是使用 .NET Framework 类库的 ImportCatalogPart 类创建的。此类可在 System.Web.UI.WebControls.WebParts 命名空间中使用。

ImportCatalogPart 类的继承层次结构如下所示：

```text
System.Object
    System.Web.UI.Control
        System.Web.UI.WebControls.WebControl
            System.Web.UI.WebControls.Panel
                System.Web.UI.WebControls.WebParts.Part
                    System.Web.UI.WebControls.WebParts.CatalogPart
                        System.Web.UI.WebControls.WebParts.ImportCatalogPart
```

ImportCatalogPart 控件的语法如下所示：

```csharp
ImportCatalogPart ImportCatalogPart1;
```

您可以使用 ImportCatalogPart 类的各种属性和方法来处理 ImportCatalogPart 控件。ImportCatalogPart 类的属性允许您指定 Web 页面上区域的外观和行为。ImportCatalogPart 控件的属性不能被基类的派生类继承。ImportCatalogPart 类的重要方法列于表 16.27 中：

### Table 16.27: Noteworthy Methods of the ImportCatalogPart Class

| Method | Description |
|---|---|
| GetAvailableWebPartDescriptions | Retrieves a description of WebPart controls of a catalog |
| GetWebPart | Retrieves a WebPart control based on a description passed as a parameter |

### Table 16.28: Noteworthy Properties of the ImportCatalogPart Class

| Property | Description |
|---|---|
| BrowseHelpText | Retrieves or sets a text message that informs users to browse to the location of a description file |
| ImportedPartLabelText | Retrieves or sets the text displayed after a user imports a description file to represent or describe an imported control in the catalog of imported controls |
| PartImportErrorLabelText | Retrieves or sets an error message that is displayed if an error occurs during the import process |
| UploadButtonText | Retrieves or sets the text for the Button control that starts the upload process of a description file |
| UploadHelpText | Retrieves or sets the text of a message that enables the user to upload a description file |

## The EditorZone Control

到目前为止，您必须已经对重要的 Web Parts 控件有了一些了解。现在，假设您想要更改 Web 页面的外观。为此，您必须转到 Web 页面的属性以在设计时进行更改。然而，与这种传统方法不同，您可以使用一个名为 EditorZone 的 Web Parts 控件。EditorZone 控件是用于在运行时更改包含 Web Parts 控件的 Web 页面的外观、格式和结构的主要编辑控件之一。此外，您还可以使用 EditorZone 控件来更改 Web Parts 控件的行为和内容。EditorZone 控件在 Web 页面的编辑模式下可见。此控件包含各种 EditorPart 控件，例如 AppearanceEditorPart 和 BehaviorEditorPart，用于自定义 Web 页面。EditorZone 控件是 EditorZone 类的对象。

要向 Web 页面添加 EditorZone 控件，请从工具箱将 EditorZone 控件拖放到 Default.aspx 页面的设计视图。图 16.16 显示了设计视图中的 EditorZone 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_820_0.png)

**Figure 16.16: Displaying the EditorZone Control**

您也可以通过在 Default.aspx 页面的 <form> 元素中使用以下代码添加 EditorZone 控件：

```
<asp:EditorZone ID="EditorZone1" runat="server">
</asp:EditorZone>
```

EditorZone 类的重要属性列于表 16.30 中：

### Table 16.30: Noteworthy Properties of the EditorZone Class

| Property | Description |
|---|---|
| ApplyVerb | Retrieves a reference to a WebPartVerb object, which allows you to modify a Web Parts control in the edit mode |
| AssociatedDisplayModes | Retrieves the objects of the WebPartDisplayMode class activated when a ToolZone control is present on a Web page |
| CancelVerb | Retrieves a reference to a WebPartVerb object, which allows you to cancel the modification you made to a control in the edit mode |
| EditorPartChrome | Retrieves a reference to an instance of the EditorPartChrome class related to an EditorZoneBase zone |
| EditorParts | Retrieves all EditorPart controls contained in an EditorZoneBase zone |
| EditUIStyle | Retrieves the style attributes for the controls contained in a ToolZone control |
| EmptyZoneText | Sets or retrieves a message text, which appears when a zone is empty and has no controls |
| EmptyZoneTextStyle | Retrieves the style attributes for text in an empty zone |
| ErrorStyle | Retrieves the style attributes of an EditorZone control for displaying an error message if the control is not loaded or created |
| ErrorText | Retrieves or sets the text to display an error message in the editing UI |
| FooterStyle | Retrieves the style attributes for the footer area of a zone |
| HeaderCloseVerb | Retrieves a reference to a WebPartVerb object in the header of a ToolZone control to close the control |
| HeaderStyle | Retrieves the style attributes for the header area of a zone |
| HeaderText | Retrieves or sets the text for the header area of a zone |
| HeaderVerbStyle | Retrieves the style attributes of all the header verbs displayed in a ToolZone control |
| InstructionText | Retrieves or sets the text to instruct users how to use a ToolZone control |
| InstructionTextStyle | Retrieves the attributes for the text displayed at the top of a ToolZone control |
| LabelStyle | Retrieves the style attributes for the labels that appear in the editing controls of a ToolZone control |
| OKVerb | Retrieves a reference to a WebPartVerb object to apply editing changes to a control and hide the editing UI |
| Padding | Retrieves or sets the attributes related to cell padding in a table containing Web Parts controls |
| PartChromeStyle | Retrieves the style attributes for the borders of Web Parts controls contained in a zone |
| PartChromeType | Retrieves or sets the border type of Web Parts controls |
| PartStyle | Retrieves the style attributes for the border and content of Web Parts controls |
| PartTitleStyle | Retrieves the style attributes for the title bar of Web Parts controls |
| VerbButtonType | Retrieves or sets the button to represent the verbs in a zone |
| VerbStyle | Retrieves style characteristics for the UI of verbs of Web Parts controls |
| ZoneTemplate | Provides a template to add child controls to an EditorZone control |

