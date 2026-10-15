
> NOTE
> These properties are not used by the Web Parts control set when rendering a DeclarativeCatalogPart control. The property is overridden only for the purpose of preventing it from appearing in Microsoft Visual Studio 2010 designer tools.

## The PageCatalogPart Control

The PageCatalogPart control is used with the CatalogZone control to add a specific functionality to the catalog section of a Web page. This control allows users to restore previously deleted WebPart controls of a Web page. This is the only way users have to restore the deleted Web Parts controls. The PageCatalogPart control adds a list of check boxes to the catalog zone controls corresponding to each deleted Web Parts control. To restore these controls on the Web page, users simply need to select the required check box and a Web part zone where the Web Parts control is to be added, and click the Add button.

To add the PageCatalogPart control to the CatalogZone control, drag and drop the PageCatalogPart control from the Toolbox to the CatalogZone control in the Design view of a Default.aspx page. Figure 16.14 shows the PageCatalogPart control inside the CatalogZone control in the Design view:

![](img/e073a4882197be4ab61103cbe0bcb394_818_0.png)

**Figure 16.14: Displaying the PageCatalogPart Control**

```
<asp:CatalogZone ID="CatalogZone1" runat="server" Height="183px" width="318px">
<ZoneTemplate>
<asp:PageCatalogPart ID="PageCatalogPart1" runat="server" Height="198px" />
</ZoneTemplate>
</asp:CatalogZone>
```

The PageCatalogPart control is an object of the PageCatalogPart class. This control is associated to the PageCatalogPart class, which provides the same events, methods, and properties as those provided by the CatalogZone class.

- System.Object
- System.Web.UI.Control
- System.Web.UI.WebControls.WebControl
- System.Web.UI.WebControls.Panel
- System.Web.UI.WebControls.WebPart
- System.Web.UI.WebControls.WebParts.CatalogPart
- System.Web.UI.WebControls.WebParts.PageCatalogPart

You can declare the PageCatalogPart class to add a PageCatalogPart control. The syntax to declare the PageCatalogPart class is given as follows:

```
PageCatalogPart pagecatalogpart;
```

## The ImportCatalogPart Control

The ImportCatalogPart control imports the description file of a Web Parts control or server control that is used as a Web Parts control. This enables the server control to be added to a Web page with pre-assigned settings. The description file enables users to share the settings of Web Parts control. The ImportCatalogPart control is the third control (the other two being DeclarativeCatalogPart and PageCatalogPart), which is used with the CatalogZone control to add a specific functionality to the catalog section of a Web page. This control provides you with options that allow you to browse and upload a description file required for importing a WebPart control.

The ImportCatalogPart control is an object of the ImportCatalogPart class.

> **NOTE**
> 
> A description file is an XML file with a .WebPart extension. It contains property values, state data, and reference to the assembly or source file. If the properties of a Web Part control are customized, the description file contains values for those properties as well.

You can add an ImportCatalogPart control to a Web page by dragging and dropping it from the Toolbox to the CatalogZone control in the Design view of a Default.aspx page. Figure 16.15 shows the ImportCatalogPart control inside the CatalogZone control in the Design view:

![](img/e073a4882197be4ab61103cbe0bcb394_819_0.png)

**Figure 16.15: Displaying the ImportCatalogPart Control**

You can also add the ImportCatalogPart control by using the following code in the <form> element of the Default.aspx page:

```aspx
<asp:CatalogZone ID="CatalogZone1" runat="server">
    <ZoneTemplate>
        <asp:ImportCatalogPart ID="ImportCatalogPart1" runat="server" />
    </ZoneTemplate>
</asp:CatalogZone>
```

The ImportCatalogPart control is created by using the ImportCatalogPart class of the .NET Framework class library. This class is available in the System.Web.UI.WebControls.WebParts namespace.

The inheritance hierarchy of the ImportCatalogPart class is given as follows:

```text
System.Object
    System.Web.UI.Control
        System.Web.UI.WebControls.WebControl
            System.Web.UI.WebControls.Panel
                System.Web.UI.WebControls.WebParts.Part
                    System.Web.UI.WebControls.WebParts.CatalogPart
                        System.Web.UI.WebControls.WebParts.ImportCatalogPart
```

The syntax of the ImportCatalogPart control is given as follows:

```csharp
ImportCatalogPart ImportCatalogPart1;
```

You can use the various properties and methods of the ImportCatalogPart class to handle the ImportCatalogPart control. The properties of the ImportCatalogPart class allow you to specify the appearance and behavior of a zone on a Web page. The properties of the ImportCatalogPart control cannot be inherited by the derived classes of a base class. Noteworthy methods of the ImportCatalogPart class are listed in Table 16.27:

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

Till now, you must have got some idea of important Web Parts controls. Now, suppose you want to change the appearance of a Web page. To do so, you have to go to the properties of the Web page to make the changes at design time. However, instead of this traditional approach, you can use a Web Parts control called EditorZone. The EditorZone control is one of the primary editing controls used to change the appearance, format, and structure of Web pages containing Web Parts controls at run time. In addition, you can use the EditorZone control to change the behavior and content of Web Parts controls. The EditorZone control is visible in the edit mode of the Web page. This control contains various EditorPart controls, such as AppearanceEditorPart and BehaviorEditorPart, which are used to customize the Web page. The EditorZone control is an object of the EditorZone class.

To add an EditorZone control to the Web page, drag and drop the EditorZone control from the Toolbox to the Design view of a Default.aspx page. Figure 16.16 shows the EditorZone control in the Design view:

![](img/e073a4882197be4ab61103cbe0bcb394_820_0.png)

**Figure 16.16: Displaying the EditorZone Control**

You can also add an EditorZone control by using the following code in the <form> element of the Default.aspx page:

```
<asp:EditorZone ID="EditorZone1" runat="server">
</asp:EditorZone>
```

Noteworthy properties of the EditorZone class are listed in Table 16.30:

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
