# How It Works

In the first three steps, you witnessed the behavior of non-View State properties. You started off by writing some code in the Page_Load event handler that sets the DisplayDirection programmatically:

```
VB.NET
If Not Page.IsPostBack Then
    Banner2.DisplayDirection = Direction.Vertical
End If
```

```
C#
if (!Page.IsPostBack)
{
    Banner2.DisplayDirection = Direction.Vertical;
}
```

Because of the check for Page.IsPostBack, this code only fires when the page loads the first time. It doesn't fire when the page is reloaded due to a postback. When it fires, it sets the DisplayDirection property of the Banner control so the banner displays the correct image. However, as soon as the page is posted back, this value is lost and the control reverts to its default direction of Horizontal. One way to overcome this problem is to make sure the code fires both the first time and on subsequent postbacks. Removing the check for Page.IsPostBack is enough to accomplish this. However, this is not always a desired solution. Imagine you're getting the correct display direction from a database. Because fetching data from a database is a costly operation, you want to minimize the number of times you hit the database. In such scenarios, developers are likely to fetch the data only when the page loads the first time and expect it to stay around on subsequent postbacks. That is exactly what the NavigateUrl property does. You set its value once and it stays available, even if you post the page back to the server. This is accomplished with a View State property.

To see how this works, take a look at the setter of that property first:

```
VB.NET
Public Property NavigateUrl() As String
...
    Set(Value As String)
        ViewState("NavigateUrl") = Value
    End Set
End Property
```

```
C#
public string NavigateUrl
{
    ...
    set
    {
        ViewState["NavigateUrl"] = value;
    }
}
```

When you assign a value to the NavigateUrl property, its value is stored in the ViewState collection. You can see the ViewState collection as a bag that enables you to store data that you can retrieve