
```aspx
<head runat="server">
    <title>Untitled Page</title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
        <asp:Button ID="Button1" runat="server" Text="Button" BackColor="#3366FF" Font-Bold="True"
            ForeColor="Yellow" /> <br />
        <br />
        <asp:TextBox ID="TextBox1" runat="server" BorderColor="#66CCFF"
            BorderStyle="Groove"
            Height="32px" Width="198px"></asp:TextBox>
        <br />
        <asp:ListBox ID="ListBox1" runat="server" BackColor="#CCFF99" Height="209px"
            Width="310px">
        </asp:ListBox>
        <font size="5"><strong>Adding Server Control in ASP.NET Application</strong></font>
        <p>
            <font><strong>Click Add button to add contents of text box to the list box</strong></font>
        </p>
    </div>
    </form>
</body>
</html>
```

## Some Common Properties of the Server Controls

The following table shows the inherited properties, common to all server controls :

| Property | Description |
|---|---|
| AccessKey | Pressing this key with the Alt key moves focus to the control. |
| Attributes | It is the collection of arbitrary attributes (for rendering only) that do not correspond to properties on the control. |
| BackColor | Background color. |
| BindingContainer | The control that contains this control's data binding. |
| BorderColor | Border color. |
| BorderStyle | Border style. |
| BorderWidth | Border width. |
| CausesValidation | Indicates if it causes validation. |
| ChildControlCreated | It indicates whether the server control's child controls have been created. |
| ClientID | Control ID for HTML markup. |
| Context | The HttpContext object associated with the server control. |
| Controls | Collection of all controls contained within the control. |
| ControlStyle | The style of the Web server control. |
| CssClass | CSS class |
| DataItemContainer | Gets a reference to the naming container if the naming container implements IDataItemContainer. |
| DataKeysContainer | Gets a reference to the naming container if the naming container implements IDataKeysControl. |
| DesignMode | It indicates whether the control is being used on a design surface. |
| DisabledCssClass | Gets or sets the CSS class to apply to the rendered HTML element when the control is disabled. |
| Enabled | Indicates whether the control is grayed out. |
| EnableTheming | Indicates whether theming applies to the control. |
| EnableViewState | Indicates whether the view state of the control is maintained. |
| Events | Gets a list of event handler delegates for the control. |
| Font | Font. |
| ForeColor | Foreground color. |
| HasAttributes | Indicates whether the control has attributes set. |
| HasChildViewState | Indicates whether the current server control's child controls have any saved view-state settings. |
| Height | Height in pixels or %. |
| ID | Identifier for the control. |
| IsChildControlStateCleared | Indicates whether controls contained within this control have control state. |
| IsEnabled | Gets a value indicating whether the control is enabled. |
| IsTrackingViewState | It indicates whether the server control is saving changes to its view state. |
| IsViewStateEnabled | It indicates whether view state is enabled for this control. |
| LoadViewStateById | It indicates whether the control participates in loading its view state by ID instead of index. |
| Page | Page containing the control. |
| Parent | Parent control. |
| RenderingCompatibility | It specifies the ASP.NET version that the rendered HTML will be compatible with. |
| Site | The container that hosts the current control when rendered on a design surface. |
| SkinID | Gets or sets the skin to apply to the control. |
| Style | Gets a collection of text attributes that will be rendered as a style attribute on the outer tag of the Web server control. |
| TabIndex | Gets or sets the tab index of the Web server control. |
| TagKey | Gets the HtmlTextWriterTag value that corresponds to this Web server control. |
| TagName | Gets the name of the control tag. |
| TemplateControl | The template that contains this control. |
| TemplateSourceDirectory | Gets the virtual directory of the page or control containing this control. |
| ToolTip | Gets or sets the text displayed when the mouse pointer hovers over the web server control. |
| UniqueID | Unique identifier. |
| ViewState | Gets a dictionary of state information that saves and restores the view state of a server control across multiple requests for the same page. |
| ViewStateIgnoreCase | It indicates whether the StateBag object is case-insensitive. |
| ViewStateMode | Gets or sets the view-state mode of this control. |
| Visible | It indicates whether a server control is visible. |
| Width | Gets or sets the width of the Web server control. |

## Common Methods of the Server Controls

The following table provides the methods of the server controls:

| Method | Description |
|---|---|
| AddAttributesToRender | Adds HTML attributes and styles that need to be rendered to the specified HtmlTextWriterTag. |
| AddedControl | Called after a child control is added to the Controls collection of the control object. |
| AddParsedSubObject | Notifies the server control that an element, either XML or HTML, was parsed, and adds the element to the server control's control collection. |
| ApplyStyleSheetSkin | Applies the style properties defined in the page style sheet to the control. |
| ClearCachedClientID | Infrastructure. Sets the cached ClientID value to null. |
| ClearChildControlState | Deletes the control-state information for the server control's child controls. |
| ClearChildState | Deletes the view-state and control-state information for all the server control's child controls. |
| ClearChildViewState | Deletes the view-state information for all the server control's child controls. |
| CreateChildControls | Used in creating child controls. |
| CreateControlCollection | Creates a new ControlCollection object to hold the child controls. |
| CreateControlStyle | Creates the style object that is used to implement all style related properties. |
| DataBind | Binds a data source to the server control and all its child controls. |
| DataBind(Boolean) | Binds a data source to the server control and all its child controls with an option to raise the DataBinding event. |
| DataBindChildren | Binds a data source to the server control's child controls. |
| Dispose | Enables a server control to perform final clean up before it is released from memory. |
| EnsureChildControls | Determines whether the server control contains child controls. If it does not, it creates child controls. |
| EnsureID | Creates an identifier for controls that do not have an identifier. |
| Equals(Object) | Determines whether the specified object is equal to the current object. |
| Finalize | Allows an object to attempt to free resources and perform other cleanup operations before the object is reclaimed by garbage collection. |
| FindControl(String) | Searches the current naming container for a server control with the specified id parameter. |
| FindControl(String, Int32) | Searches the current naming container for a server control with the specified id and an integer. |
| Focus | Sets input focus to a control. |
| GetDesignModeState | Gets design-time data for a control. |
| GetType | Gets the type of the current instance. |
| GetUniqueIDRelativeTo | Returns the prefixed portion of the UniqueID property of the specified control. |
| HasControls | Determines if the server control contains any child controls. |
| HasEvents | Indicates whether events are registered for the control or any child controls. |
| IsLiteralContent | Determines if the server control holds only literal content. |
| LoadControlState | Restores control-state information. |
| LoadViewState | Restores view-state information. |
| MapPathSecure | Retrieves the physical path that a virtual path, either absolute or relative, maps to. |
| MemberwiseClone | Creates a shallow copy of the current object. |
| MergeStyle | Copies any nonblank elements of the specified style to the web control, but does not overwrite any existing style elements of the control. |
