
# The LayoutEditorPart Control

You can use the LayoutEditorPart control to create a full-fledged layout editor for Web Parts controls, which can have their respective LayoutEditorPart controls associated with them. To change the layout of a Web Parts control, simply make the required changes in the LayoutEditorPart control associated with the Web Parts control.

The LayoutEditorPart control is visible only when a Web page is in the edit mode. In this mode, you can select and change the properties of a Web Part control. The LayoutEditorPart control offers the following three options to modify a Web Parts control:

- ChromeState – Gets or sets the current state of a Web Parts control, which can be normal or minimized.
- Zone – Sets the WebPartZoneBase zone, which consists of the Web Parts control you want to modify.
- ZoneIndex – Sets the index position of Web Parts controls that reside in a WebPartZone control. This option allows you to determine the specific position of a Web Parts control within the WebPartZone control.

You must use the LayoutEditorPart control in page persistence format. This format enables the LayoutEditorPart control to retain its property values between browser sessions. To do this, you need to declare the <asp:LayoutEditorPart> element inside the <ZoneTemplate> element.

To add a LayoutEditorPart control to a Web page, drag and drop a LayoutEditorPart control from the Toolbox to the Design view of a Default.aspx page. Figure 16.17 shows the LayoutEditorPart control inside an EditorZone control in the Design view:

![](img/e073a4882197be4ab61103cbe0bcb394_823_0.png)

You can also add the LayoutEditorPart control by using the following code in the <form> element of the Default.aspx page:

```
<asp:EditorZone ID="EditorZone1" runat="server">
<ZoneTemplate>
<asp:LayoutEditorPart ID="LayoutEditorPart1" runat="server" />
</ZoneTemplate>
</asp:EditorZone>
```

The LayoutEditorPart control is an object of the LayoutEditorPart class.

> NOTE
> If you place LayoutEditorPart controls in any other zone except the EditorZone control, the designer generates an error.

The LayoutEditorPart control is created by using the LayoutEditorPart class of the .NET Framework class library. The LayoutEditorPart class allows you to modify the layout of the associated Web Parts control. This class is available in the System.Web.UI.WebControls.WebParts namespace. The inheritance hierarchy of the LayoutEditorPart class is given as follows:

```
System.Object
    System.Web.UI.Control
        System.Web.UI.WebControls.WebControl
            System.Web.UI.WebControls.Panel
                System.Web.UI.WebControls.WebParts.Part
                    System.Web.UI.WebControls.WebParts.EditorPart
                        System.Web.UI.WebControls.WebParts.LayoutEditorPart
```

The LayoutEditorPart control is associated with the LayoutEditorPart class. This class employs various methods to perform tasks, such as applying changes and style properties to a Web Parts control and determining if two object instances are equal. Noteworthy methods of the LayoutEditorPart class are listed in Table 16.31:

| Table 16.31: Noteworthy Methods of the LayoutEditorPart Class |
| Method | Description |
| ApplyChanges | Updates the associated WebPart control properties with the changes made in a LayoutEditorPart control |
| SyncChanges | Gets the property values from a WebPart control, which is then assigned to the associated LayoutEditorPart control |

Now, let's take a look at the properties of the LayoutEditorPart class, which is inherited from the EditorPart class. This class acts as a base class that provides a set of properties and methods to the LayoutEditorPart class, which also inherits some of the properties from other classes, such as Control, Part, and WebControl. The various properties inherited by the LayoutEditorPart class are Font, Enabled, Page, and Style. Noteworthy properties of the LayoutEditorPart class are listed in Table 16.32:

| Table 16.32: Noteworthy Properties of the LayoutEditorPart Class |
| Property | Description |
| DefaultButton | Retrieves or specify the ID of default button included in a Panel control |
| Display | Retrieves a value that specifies whether the LayoutEditorPart control should be displayed when the Web Parts control associated with it is in the edit mode |
| Title | Retrieves or specify a string used as a title for the LayoutEditorPart control |

## The AppearanceEditorPart Control

The AppearanceEditorPart control allows users to edit the properties associated with the appearance of a Web Parts control on the Web page. This control resides in an EditorZone zone and is visible only when a Web Parts control is selected for editing. The following options are displayed on the AppearanceEditorPart control:

- Title — Specifies a string value, which appears as a title of the AppearanceEditorPart control
- Height — Specifies the height of the AppearanceEditorPart control
- Width — Specifies the width of the AppearanceEditorPart control
- ChromeType — Selects the title and border type (dotted, single line, or double line) of the AppearanceEditorPart control by using the DropDownList control
- Direction — Selects the direction (horizontal or vertical) of content flow inside the AppearanceEditorPart control by using the DropDownList control
- Hidden — Hides or displays the AppearanceEditorPart control by using the CheckBox control

To add the AppearanceEditorPart control to the EditorZone control, drag and drop the control from the Toolbox to the EditorZone control in the Design view of a Default.aspx page. Figure 16.18 shows the AppearanceEditorPart control inside the EditorZone control in the Design view:

![](img/e073a4882197be4ab61103cbe0bcb394_825_0.png)

You can also add the AppearanceEditorPart control by using the following code in the `<form>` element of the `Default.aspx` page:

```
```aspx
<asp:EditorZone ID="EditorZone1" runat="server">
    <ZoneTemplate>
        <asp:AppearanceEditorPart
            ID="AppearanceEditorPart1"
            runat="server" />
    </ZoneTemplate>
</asp:EditorZone>
```
```

The AppearanceEditorPart control is created by using the AppearanceEditorPart class of the .NET Framework class library. The AppearanceEditorPart class provides an editor with control to modify the UI properties of the associated Web Parts control. This class is available in the System.Web.UI.WebControls.WebParts namespace. The inheritance hierarchy of the AppearanceEditorPart class is given as follows:

```
```text
System.Object
    System.Web.UI.Control
        System.Web.UI.WebControls.WebControl
            System.Web.UI.WebControls.Panel
                System.Web.UI.WebControls.WebParts.Part
                    System.Web.UI.WebControls.WebParts.EditorPart
                        System.Web.UI.WebControls.WebParts.AppearanceEditorPart
```
```

The AppearanceEditorPart class contains methods and properties that are used to work with the AppearanceEditorPart control at runtime. Noteworthy methods of the AppearanceEditorPart class are listed in Table 16.33:

**Table 16.33: Noteworthy Methods of the AppearanceEditorPart Class**

| Method | Description |
|---|---|
| ApplyChanges | Updates the associated WebPart control properties with the changes made in the AppearanceEditorPart control |
| SyncChanges | Gets the property values from a WebPart control, which is then assigned to the associated AppearanceEditorPart control |

Noteworthy properties of the AppearanceEditorPart class are listed in Table 16.34:

| Table 16.34: Noteworthy Properties of the AppearanceEditorPart Class |
| Property | Description |
| DefaultButton | Retrieves or specify the ID of default button included in a Panel control |
| Title | Retrieves or specify a string used as a title for the AppearanceEditorPart control |

## The PropertyGridEditorPart Control

The PropertyGridEditorPart control provides a UI that allows users to edit the custom properties of a Web Parts control on a Web page. This control resides in the EditorZone control on the Web page. The PropertyGridEditorPart control is visible only when the Web page is in the edit mode or when the user selects a Web Parts control for editing.

The PropertyGridEditorPart control enables users to edit the properties that are marked with the WebBrowsableAttribute attribute in the source code. This attribute specifies whether or not the property should be displayed in the PropertyGridEditorPart control. After specifying the editable properties, the PropertyGridEditorPart control creates an editable UI based on the type of properties to be edited.

To add the PropertyGridEditorPart control to a Web page, first drag and drop an EditorZone control from the Toolbox to the Design view of a Default.aspx page, and then drag and drop the PropertyGridEditorPart control from the Toolbox to the EditorZone control in the Design view. Figure 16.19 shows the PropertyGridEditorPart control inside the EditorZone control in the Design view:

![](img/e073a4882197be4ab61103cbe0bcb394_826_0.png)

Figure 16.19: Displaying the PropertyGridEditorPart Control

You can also add the PropertyGridEditorPart control by using the following code in the <form> element of the Default.aspx page:

```
<asp:EditorZone ID="EditorZone1" runat="server">
<ZoneTemplate>
<asp:PropertyGridEditorPart ID="PropertyGridEditorPart1" runat="server" />
</ZoneTemplate>
</asp:EditorZone>
```

The PropertyGridEditorPart control is an object of the PropertyGridEditorPart class. This control is created by using the PropertyGridEditorPart class of the .NET Framework class library. The PropertyGridEditorPart class enables users to modify the custom properties of the associated Web Parts or server control. This class is available in the System.Web.UI.WebControls.WebParts namespace. The inheritance hierarchy of the PropertyGridEditorPart class is given as follows:
