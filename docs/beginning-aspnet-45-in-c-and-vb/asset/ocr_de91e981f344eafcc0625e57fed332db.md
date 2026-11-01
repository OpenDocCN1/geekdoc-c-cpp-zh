When the control instance is created by the ASP.NET run time, the value you set in the control declaration is assigned to the property DisplayDirection. If you don't assign a value, the default will be Horizontal for the current definition of the Direction enum as that's the first item in the list and has an implicit value of zero.

When the page loads, this code in the user control is executed:

# VB.NET

```
```vbnet
Select Case DisplayDirection
    Case Direction.Horizontal
        HorizontalPanel.Visible = True
        VerticalPanel.Visible = False
    Case Direction.Vertical
        VerticalPanel.Visible = True
        HorizontalPanel.Visible = False
End Select
```
```

# C#

```
```csharp
switch (DisplayDirection)
{
    case Direction.Horizontal:
        HorizontalPanel.Visible = true;
        VerticalPanel.Visible = false;
        break;
    case Direction.Vertical:
        VerticalPanel.Visible = true;
        HorizontalPanel.Visible = false;
        break;
}
```
```

This code uses a Select Case/switch block to determine which image to show. When the DisplayDirection equals Horizontal, the Visible property of HorizontalPanel is set to True and the other control is hidden. The same principle is applied to the Vertical setting.

# Implementing View State Properties

In addition to the DisplayDirection, another useful property for the user control would be the URL that the banner links to. In the next section, you see how to implement this and learn how to create a View State property called NavigateUrl that is able to survive postbacks.

# TRY IT OUT Implementing the NavigateUrl Property

To be able to set the URL that a user is taken to programmatically, you need to be able to access the anchor tag that is defined in the control's markup. To do this, you need to give it an id and a runat="server" attribute. To be able to programmatically set the new NavigateUrl property that you'll add to the Banner control and to ensure that this property survives postbacks, you need to implement a View State property. To show you why you need a View State property, the first three steps of this exercise have you modify the About Us page so it sets the DisplayDirection of the Banner control programmatically. You'll then cause a postback so you can see that the value for the direction gets lost