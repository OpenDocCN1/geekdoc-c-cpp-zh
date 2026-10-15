You can also add the WebPartZone control by inserting the following code in the `<form>` element of the Default.aspx page:

```
```aspx
<asp:WebPartZone ID="WebPartZone1" runat="server">
</asp:WebPartZone>
```
```

> **NOTE**
> 
> The WebPartZone control also contains the `<ZoneTemplate>` element, which is used for storing other server controls, such as Label or Textbox.

The WebPartZone control is created by using the WebPartZone class of the .NET Framework class library. This class derives most of its functionalities from the base WebZone and WebPartZoneBase classes. The WebPartZone class is available in the System.Web.UI.WebControls.WebParts namespace. The namespace hierarchy of the WebPartZone class is as follows:

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

You can use the various properties and methods of the WebPartZone class to use the WebPartZone control. The properties of the WebPartZone class allow you to set the appearance and behavior of the WebPartZone control on a Web page. The WebPartZone control is the primary control to add Web Parts controls on the Web page. You can add server controls in the WebPartZone control, which can be added to the Web page.

The syntax for creating a WebPartZone control is given as follows:

```
```aspx
<WebPartZone <object name>>
```
```

Using the .NET Framework class library, the WebPartZone class is declared as follows:

```
```csharp
public class WebPartZone : WebPartZoneBase
```
```

Noteworthy methods of the WebPartZone class are listed in Table 16.20:

| Method | Description |
|---|---|
| CreateWebPartChrome | Enables derived zones to substitute a custom WebPartChrome object to the appearance of Web Parts controls in a zone |
| EditWebPart | Initiates the process of editing a selected Web Parts control in a zone |
| GetInitialWebParts | Overrides the abstract base method and retrieves the initial set of values of static WebPart controls contained within a zone's template |
| MinimizeWebPart | Minimizes a selected Web Parts control in a zone |
| OnCreateVerbs | Raises the CreateVerbs event |
| RenderDropCue | Provides UI elements to indicate where a Web Parts control is dragged and dropped within a zone |
| RestoreWebPart | Restores a selected minimized Web Parts control to the normal state |

Noteworthy properties of the WebPartZone class are listed in Table 16.21:

| Property | Description |
|---|---|
| AllowLayoutChange | Determines whether or not the layout of a Web Parts control can be modified. This property also allows you to specify a layout for the Web Parts control. |