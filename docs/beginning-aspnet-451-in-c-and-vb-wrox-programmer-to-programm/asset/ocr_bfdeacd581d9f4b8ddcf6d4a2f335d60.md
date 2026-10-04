# 26 | CHAPTER 6 CREATING CONSISTENT LOOKING WEBSITES

# ## TRY OUT Letting the User Select a Theme

In this exercise you add a DropDownList control to the master page. This control contains the available themes you can choose. The user's choice is stored in a cookie so it's available again later. The final step is to preselect the correct theme in the drop-down list when the user revisits the page.

+   1. Open the master page in Markup View and locate the <aside> element. Replace the static text Sidebar Goes Here and replace it with a DropDownList by dragging it from the Toolbox between the two <div> tags. Change the ID from DropDown1 to ThemeList. Some type (for example, Select a Theme) followed by a line break <br> in front of the drop-down list to clarify the purpose of the text.

+   2. Open the control's Smart Tasks panel (in Design View or Markup View), and enable AutoPostBack.

+   3. On the same Smart Tasks panel, click the Edit Items list and insert two items: one with the text Monochrome and one with the text DarkGrey.

+   4. Double-click the drop-down list in Design View to set up an event handler for the SelectedSelectedIndex event. Instead of double-clicking, you can also select the DropDownList, press F4 to open its Properties Grid, click the button with the lightning bolt to select the event, and double-click SelectedSelectedIndex. Figure 6-20 shows the Properties Grid in Events mode.

![](bbox=[0.633, 0.306, 0.866, 0.453])

FIGURE 6-20

As you aware, you could also add this event handler in Markup View on the control declaration directly.

Any code you write in the SelectedSelectedIndex handler fires at the server when the user makes a selection in the drop-down list with the client. Within the handler block, add the following code that retrieves the theme from the store and stores it in a cookie:

VB.NET

```
Protected Sub ThemeList_SelectedIndex(sender As Object, 
                                e As EventArgs) Handles ThemeList.SelectedIndex
Dim preferredTheme As HttpCookie = New HttpCookie("*PreferredTheme")
preferredTheme.Expires = DateTime.Now.AddMonths(3)
preferredTheme.Value = ThemeList.SelectedIndexValue
Response.Cookies.Add(preferredTheme)
Response.Redirect(Request.Url.ToString())
End Sub
```

C#

```
protected void ThemeList_SelectedIndexChanged(object sender, EventArgs e)
{
    HttpCookie preferredTheme = new HttpCookie("*PreferredTheme*");
    preferredTheme.Expires = DateTime.Now.AddMonths(3);
    preferredTheme.Value = ThemeList.SelectedIndexValue;
    Response.Cookies.Add(preferredTheme);
    Response.Redirect(Request.Url.ToString());
}
```