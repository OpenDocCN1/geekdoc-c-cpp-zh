Remember, you don't have to type all this code manually because the download that comes with
this book contains all the code shown.

```
VB.NET
Public Property NavigateUrl() As String
Get
    Dim _navigateUrl As Object = ViewState("NavigateUrl")
    If _navigateUrl IsNot Nothing Then
        Return CType(_navigateUrl, String)
Else
        Return "http://p2p.wrox.com" ' Return a default value
End If
End Get
Set (Value As String)
    ViewState("NavigateUrl") = Value
End Set
Property
```

# C#

```
public string NavigateUrl
{
    object _navigateUrl = ViewState["NavigateUrl"];
    if (_navigateUrl != null)
    {
        return (string)_navigateUrl;
    }
    else
    {
        return "http://p2p.wrox.com"; // Return a default value
    }
}
set
{
    ViewState["NavigateUrl"] = value;
}
```

+   5. Switch to Markup View of the user control add runat="server" attributes to both
links. Give the link in the vertical panel id of VerticalLink and the other an id of
HorizontalLink. They should end up looking like this:

```
<a href="http://p2p.wrox.com" target="_blank" runat="server" id="VerticalLink">
n<a href="http://p2p.wrox.com" target="_blank" runat="server" id="HorizontalLink">
```

+   6. Switch to the Beginning of the user control (press F7) and modify the Page_Load handler
of the user control so it also sets the HRef property of the anchor element:

```
VB.NET
Case Direction.Horizontal
    HorizontalPanel.Visible = True
    VerticalPanel.Visible = False
```