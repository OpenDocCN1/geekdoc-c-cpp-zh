# CHAPTER 6 CREATING CONSISTENT LOOKING WEBSITES

```
if (!string.IsNullOrEmpty(selectedTheme))
{
    ListItem item = ThemeList.Items.FindByValue(selectedTheme);
    if (item == null)
    {
        item.Selected = true;
    }
}
```

6. Save all changes and request Default.aspx in your browser gallery. The drop-down list in the sidebar should display the first item in the list. Select the other option from the list and the page will reload. The item you choose last in the drop-down list should now be preselected in the drop-down list. Close your browser and then browse to Default.aspx. The theme you choose should still be selected in the drop-down list. Notice that you keep seeing the same theme you have written without any code that applies the selected theme. You will see that in a later exercise.

> COMMON MISTAKES If you get an error, make sure you have no typos in the code. If nothing happens (for example, the page doesn't post back), check if you used the AutoPostBack attribute on the DropDownList to control it. Also, check the spelling of the name of the code (PreferredTheme) in both codes. Finally, if the correct item is not preselected after a postback or after you reload your browser, check your browser's or computer's security settings. You may have configured your browser to delete cookies when you close the browser, or you may have security software running on your machine that blocks cookies altogether. If you can't make it work in one browser, try it in another to rule out problems with the code.

# How It Works

You made three changes to the master page. First, you added the drop-down list and set AutoPostBackTo True. This causes the page to submit itself back to the server as soon as you choose a new item. When happens, the code in the SelectedIndexChanged handler fires. This code creates a cookie that can be stored on the user's computer. To make the cookie between browser sessions, you need to set the Expires property. In the example, the cookie is set to expire three months from now, which means the browser will discard it after that period. Every time the user chooses a new theme, this date is extended, setting it for another three months:

# VB.NET

```
Dim preferredTheme As HttpCookie = New HttpCookie("PreferredTheme")
preferredTheme.Expires = DateTime.Now.AddMonths(3);
```

# C#

```
Cookie preferredTheme = new HttpCookie("PreferredTheme");
preferredTheme.Expires = DateTime.Now.AddMonths(3);
```