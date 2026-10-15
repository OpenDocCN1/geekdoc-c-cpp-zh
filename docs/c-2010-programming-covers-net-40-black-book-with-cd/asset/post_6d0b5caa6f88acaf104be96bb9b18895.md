
System.Object
    System.Web.UI.Control
        System.Web.UI.WebControls.WebControl
            System.Web.UI.WebControls.Panel
                System.Web.UI.WebControls.WebParts.Part
                    System.Web.UI.WebControls.WebParts.EditorPart
                        System.Web.UI.WebControls.WebParts.PropertyGridEditorPart

The syntax of the PropertyGridEditorPart control is given as follows:
PropertyGridEditorPart propgrid;

The PropertyGridEditorPart class resides in the System.Web.UI.WebControls.WebParts namespace and cannot be inherited. This class consists of the Title and Display properties. The Title property is used to obtain or set a title text for a Web Parts control and the Display property is used to determine whether the control is displayed when the Web page is in the edit mode or not.

The two important methods in the PropertyGridEditorPart class are ApplyChanges and SyncChanges. The ApplyChanges method saves the value that a user sets on the PropertyGridEditorPart control to the corresponding properties of a Web Parts control. This method is called when the user clicks the OK or Apply button on the editing UI. It returns true if the values from the PropertyGridEditorPart control are saved to a WebPart control and returns false if the values are not saved in the WebPart control. The SyncChanges method updates the values of the PropertyGridEditorPart control so that the users can edit the values of these properties.

## The BehaviorEditorPart Control

The BehaviorEditorPart control, as the name suggests, provides options that enable users to modify the behavior of Web Parts controls. This control usually remains hidden and is visible only when a Web page containing Web Parts controls is in the edit mode. Similar to other EditorPart controls, the BehaviorEditorPart control is also contained inside the EditorZone control.

The various options provided by the BehaviorEditorPart control are as follows:

- Description – Describes the functionality a Web Parts control in brief
- TitleUrl – Specifies the link for additional information about a Web Part control
- TitleIconImageUrl – Specifies an image, which appears in the title bar of a Web Part control
- CatalogIconImageUrl – Specifies an image, which appears as a representative of a Web Parts control in the catalog of controls
- HelpUrl – Specifies the link of the help file of a Web Parts control
- HelpMode – Specifies the type of UI to display the help content of a Web Part control
- Hidden – Hides or displays a Web Parts control
- ImportErrorMessage – Retrieves or specifies the error message, which appears when importing a Web Parts control
- ExportMode – Exports the properties of a Web Parts control
- AuthorizationFilter – Specifies a string value, which indicates whether you can add a Web Parts control to a Web page or not
- AllowClose – Specifies a value that allows a user to close a Web Parts control on a Web page
- AllowEdit – Specifies a value that allows a user to modify a Web Parts control on Web page
- AllowHide – Specifies a value that allows a user to hide a Web Parts control
- AllowMinimize – Specifies a value to minimize a Web Parts control
- AllowZoneChange – Specifies a value that indicates whether a Web Parts control can be moved from one zone to another

To add the BehaviorEditorPart control to a Web page, drag and drop the control from the Toolbox to the EditorZone control in the Design view of a Default.aspx page. Figure 16.20 shows the BehaviorEditorPart control inside the EditorZone control in the Design view:

![](img/e073a4882197be4ab61103cbe0bcb394_828_0.png)

You can also add the BehaviorEditorPart control by using the following code in the `<zonetemplate>` element of the EditorZone control on the Default.aspx page:

```
```aspx
<ZoneTemplate>
    <asp:BehaviorEditorPart ID="BehaviorEditorPart1" runat="server" />
</ZoneTemplate>
```
```

The BehaviorEditorPart control is an object of the BehaviorEditorPart class. The BehaviorEditorPart control is used for modifying UI properties, such as Title, Link, Description, and Help link, in a Web page. You can add the BehaviorEditorPart control by using the BehaviorEditorPart class, which belongs to the System.Web.dll assembly. The namespace hierarchy of the BehaviorEditorPart class is given as follows:

```
```text
System.Object
    System.Web.UI.Control
        System.Web.UI.WebControls.WebControl
            System.Web.UI.WebControls.Panel
                System.Web.UI.WebControls.WebParts.Part
                    System.Web.UI.WebControls.WebParts.EditorPart
                        System.Web.UI.WebControls.WebParts.BehaviorEditorPart
```
```

The syntax of the BehaviorEditorPart control is given as follows:

```
```text
BehaviorEditorPart behaviorA;
```
```

The BehaviorEditorPart class derives from the EditorPart class, which is used to modify the properties of the associated Web Parts control. The BehaviorEditorPart class inherits various methods, properties, and events from the Control class, such as ApplyStyle, Title, and DataBinding. Noteworthy properties of the BehaviorEditorPart class are listed in Table 16.35:

| Property | Description |
|---|---|
| DefaultButton | Retrieves or specifies the ID of default button included in a Panel control |
| Display | Retrieves a value that specifies whether the BehaviorEditorPart control should be displayed when the Web Parts control associated with it is in the edit mode |

## NOTE

To create a connection between Web Parts controls, a user needs to switch to the ConnectionDisplayMode and select the connection verb from the Web Part verb menu.

Noteworthy properties of the ConnectionsZone class are listed in Table 16.36:

| Property | Description |
|---|---|
| `ConfigureConnectionTitle` | Gets or sets the title text of a connection UI created by a ConnectionsZone control. |
| `ConfigureVerb` | Gets a reference to a WebPartVerb object. You can use this reference to open the configuration view in a connection UI. |
| `ConnectToConsumerInstructionText` | Gets or sets the text displayed in the section of a connection UI where users select the consumer control to connect to the provider control. |
| `ConnectToConsumerText` | Gets or sets the hyperlink text that users click to select a consumer control for a connection. |
| `ConnectToConsumerTitle` | Gets or sets the title text of the section in a connection UI where users select the consumer control to connect with. |
| `ConnectToProviderInstructionText` | Gets or sets the text that is displayed in the section of a connection UI where users select the provider control to connect to the consumer control. |
| `ConnectToProviderText` | Gets or sets a hyperlink text that users click to open and then select a provider control for a connection. |
| `CancelVerb` | Retrieves a reference to a WebPartVerb object that enables the user to cancel the process of establishing a connection. |
| `CloseVerb` | Retrieves a reference to a WebPartVerb object that enables the user to close the connection UI. |
| `ConnectToProviderTitle` | Gets or sets the title text of the section in the connection UI where users select the specific provider control to connect with. |
| `ConnectVerb` | Gets a reference to a WebPartVerb object to allow two Web Parts controls to connect with each other. |
| `ConsumersInstructionText` | Gets or sets the instructional text contained in the consumers section of a connection UI, when a connection already exists. |
| `ConsumersTitle` | Gets or sets the title text of the consumers section present in a connection UI, when a connection already exists. |
| `DisconnectVerb` | Gets a reference to a WebPartVerb object to enable the user to disconnect two connected WebPart controls. |
| `ExistingConnectionErrorMessage` | Gets or sets the message string that is displayed in a connection UI when an error occurs in an existing connection. |
| `GetFromText` | Gets or sets the text present before the name of provider in the connection UI. This provider is used by a consumer to retrieve data. |
| `GetText` | Gets or sets the text present before the name of consumer in the connection UI. This consumer retrieves the data from provider. |
| `InstructionTitle` | Gets or sets the description text for the action performed on a consumer or provider control in a connection UI to manage existing connections. |
