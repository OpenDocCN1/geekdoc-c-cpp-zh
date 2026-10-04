
5. Open the Markup View of Banner.ascx, copy the entire <asp:Panel>, and paste it below the existing Panel. Name the control HorizontalPanel and set the ImageUrl of the image to ~/Images/Banner48x60.gif. If you want to browse for the image instead of typing its path, position your cursor in Markup View after the opening quote of the Image attribute value and press Ctrl+Space. Picking URL in the menu that appears enables you to browse for file. Your code should look like this:

```
<asp:Panel Id="HorizontalPanel" runat="server">
<a href="http://p2w.worx.com" target="_blank">
<asp:Image Id="image2" runat="server" This is a sample banner
ImageUrl="~/Images/Banner48x60.gif" />
</a>
</asp:Panel>
```

6. Switch back to the Code Behind of the control and add the following code to the Page_Load handler. In C#, the handler should already be there. In Visual Basic, you can choose (Page Events) from the left drop-down list at the top of the Document Window and from the drop-down list to set up, or you can double-click the control in Design View.

### VB.NET

```vbnet
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
Select Case Direction
Case Direction.Horizontal
HorizontalPanel.Visible = True
VerticalPanel.Visible = False
Case Direction.Vertical
VerticalPanel.Visible = True
HorizontalPanel.Visible = False
End Select
End Sub
```

### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    switch (Direction)
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
}
```

7. Save and close the two files that make up the user control you're done with now.

8. Open up the master page once more in Markup View and locate the control declaration. Right after the runat="server" attribute, add the following DisplayDirection attribute that sets the correct image type:

```
<Wx:Banner ID="Banner1" runat="server" DisplayDirection="Horizontal" />
```

## CHAPTER 8 USER CONTROLS

IntelliSense will help you pick the right DisplayDirection from the list. If you don't get IntelliSense, wait a few seconds until VS has caught up with all the changes. Alternatively, save and close all open files (restart VS), open the master page, and try again.

- 9. Save all changes and request Default.aspx in the browser. Note that the right sidebar area now contains the horizontal image, breaking the layout because the image is too wide for the sidebar. If you don't see the banner appear at all, check your system for ad-blocking software that may stop the banner image from appearing.

- 10. Switch back to the master page and change the DisplayDirection from Horizontal to Vertical. Save your changes and refresh the page in the browser. The sidebar should now show the vertical banner, as shown in 8-9.

![](img/9e033e3b9560597824f8b22941d6d8bb_325_0.png)

Figure 8-9

- 11. Open the AboutUs.aspx page from the About folder in Markup View. If you don't have that file, create it. In the CpMainContent Content block, add some text describing you or your organization and the reason you created it. Switch to Design View and drop the Banner control from the Solution Explorer onto the design surface, right below the text you just added. VS detects the control in the master page called Banner1 and assigns the ID of Banner2 to the control you dropped. Notice how you see four banners in Design View; come from the Banner control in the master page and the other two come from the Banner control in the About Us page itself.

- 12. Select the user control you just added in Design View, open its Properties Grid, and set the DisplayDirection to Horizontal.

- 13. Save all your changes and press Ctrl+F5 to open the About Us page in your browser. In addition to the banner in the right sidebar, you should now also see the horizontal banner appear in the content area.

## How It Works

The property called DisplayDirection gives your user control some extra behavior. Pages using the control should now set the DisplayDirection value like this:

```
<Wdx:Banner ID="Banner1" runat="server" DisplayDirection="Horizontal" />
```

When the control is created by the ASP.NET runtime, the value set in the control declaration is assigned to the property DisplayDirection. If you don't assign a value, the default will be Horizontal for the current definition of the Direction enum, as that's the first item in the list and has an implicit value of zero.

When the page loads, this in the user control is executed:

```vbnet
Select DisplayDirection
Case Direction.Horizontal
HorizontalPanel.Visible = True
VerticalPanel.Visible = False
Case Direction.Vertical
VerticalPanel.Visible = True
HorizontalPanel.Visible = False
End Select
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

This code uses a Select/switch block to determine which image to show. When the DisplayDirection equals Horizontal, the Visible HorizontalPanel is set to True and the other control is hidden. The same principle is applied to the Vertical setting.

## Implementing View State Properties

In addition to the DisplayDirection, another property for the user control could be the URL that the banner links to. In the next section, you will see how to implement this and learn how to create a View State property called NavigateUrl that is able to survive postbacks.

CHAPTER 8 USER CONTROLS

## TRY IT OUT Implementing NavigateUrl Property

To set the URL that a user is taken programmatically, you need to be able to access the anchor tag that is defined in the control's markup. To do this, you need to give it an id and a runat="server" attribute. To be able to programmatically set the NavigateUrl property you'll need to add the Banner control and ensure that this property survives postbacks, you need to implement a View State property. To show you why you need a View State property, the first three steps of this exercise have you modify the About page so it sets the DisplayDirection of the Banner control programmatically. You'll then cause a postback so you can see that the value gets lost because it doesn't maintain its state. The second part of the exercise shows you how to implement NavigateUrl that is able to maintain its state.

- 1. Open the Code Behind of AboutUs.aspx and add the following code to the Page_Load handler. If the handler isn't there, switch to Design View and double-click somewhere on the gray area of the page.

```vbnet
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    If Page.PostBack
        Banner2.DisplayDirection = Direction.Vertical
    End If
End Sub
```

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    if (Page.PostBack)
    {
        Banner2.DisplayDirection = Direction.Vertical;
    }
}
```

Verify that the user control has an ID of Banner2 in the Markup View of the page, or update your code accordingly.

- 2. Switch to Design View and add a Button to the top of the Banner.ascx control by dragging it from the Standard category of controls is placed inside the page (not the one that's defined in the master page). There's no need to write any code for the Button's Click event.
3. Save the page and open it in your browser. Because of the code in Page_Load, the first time the page loads, the banner displays the vertical banner. Now click the button so the page will reload. The page displays the horizontal image. Because the DisplayDirection of the Banner control is set in Page_Load only when Page.PostBack is False, that is what happens when you postback, causing the banner to revert to its default setting of Horizontal.

- 4. To avoid this problem with the NavigateUrl, you need to implement it as a View State property where the ViewState collection is used to store the underlying value. That way, the value is sent to the banner and back to the server with every request. To implement the property, add the following code to the Code Behind of the Banner.ascx user control, right below the DisplayDirection property you created earlier.
