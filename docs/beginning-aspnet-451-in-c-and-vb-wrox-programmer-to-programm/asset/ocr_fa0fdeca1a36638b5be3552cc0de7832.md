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

# VB.NET

```
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

# C#

```
protected void Page_Load(object sender, EventArgs e)
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

7. Save and close the two files that make up the user control you're done with now.

8. Open up the master page once more in Markup View and locate the control declaration. Right after the runat="server" attribute, add the following DisplayDirection attribute that sets the correct image type:

```
<Wx:Banner ID="Banner1" runat="server" DisplayDirection="Horizontal" />
```