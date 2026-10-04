
5. Request Default.aspx in your browser by right-clicking it and choosing View in Browser. You now will see the web page with images from the DarkGrey theme, shown in Figure 6-18, that displays the page in Apple’s Safari.

![](img/9e033e3b9560597824f8b22941d6d8bb_260_0.png)

FIGURE 6-18

6. Go back to VS, open the Web.config file, and switch the two theme attributes of the <pages> element from DarkGrey to Monochrome. Open Default.aspx in your browser and you will see the page with the new theme and images as shown in Figure 6-19 that displays the page in Google Chrome. If you still see the old page, press Ctrl+F5 to cause a hard refresh. If you find that the page in the browser is showing a combination of the two themes, go back to VS, open Web.config, and merge the StyleSheet attribute from the <pages> element.

![](img/9e033e3b9560597824f8b22941d6d8bb_260_1.png)

FIGURE 6-19

# How It Works

From a point of view, nothing has changed in this exercise. Just as you saw before, the theme's style sheet is added to the head of the page. However, this time the style points to images located in the folder. The browser reads the CSS file, follows the link to images, downloads them, and then displays them at the right location as dictated by the various CSS selectors in the code.

The CSS files added for both themes contain a list of comments, so if you want to know what the CSS does, check out the files in the two folders.

Useful as themes may be to enable, the page developer, to quickly change the appearance and even the layout of the site, they become even more useful if you let users switch them at run time. This way, users can customize the site to their liking. The next section shows you how to accomplish this.

# Dynamically Switching Themes

Switching themes at run time has its benefits. For example, you can please your users by enabling them to choose a theme with the colors and layout they like. Not everyone appreciates a dark background with white text, so the option to change at run time is something that many people like. However, you can also deploy themes to visually impaired users. By creating a theme with a high-contrast color scheme and a large font size, you make it much easier for people to see their site. The themes in the Planet Wrox website only show screen elements like colors and layout, and it's easy to create a copy of one of those themes.

Because of the way themes are applied at run time, you need to set the theme early in the page's life cycle, in the PreInit event to be precise. The base page of the website is once again the ideal location to do this, because every page in the site inherits from this class.

To enable users to change the theme, you can offer them a drop-down menu that automatically posts back the active option to the server. In the list you get the chosen theme from the list, apply it to the page, and store the selection in a cookie so it can be retrieved on visits to the website.

Cookies are little pieces of text that you can store on the user's computer. The data you store in a cookie is only sent to the server that it sets in first, so other sites cannot read the cookie from yours. However, because cookies are stored on the user's computer as plaintext, you should not use them for any sensitive data, such as a password. Storing harmless makes the preferred theme an excellent use of cookies, though.

To create a cookie so it's stored on the user's computer, you use the Cookies collection on the Response object. This way, the cookie is sent to the browser with the response. Here's a quick example:

# VB.NET

```
Dim myCookie As HttpCookie = New HttpCookie("6")
myCookie.Expires = DateTime.Now.AddMonths(3)
myCookie.Value = "Cookie value"
Response.Cookies.Add(myCookie)
```

# C#

This code sends the cookie to the browser where it will be stored until it expires, in which this example is three months from the day the cookie is set. For each request to a page, the browser sends this cookie back to the server where you can read it again using the Cookies collection of the Request object, like this:

# VB.NET

```
Dim myCookie As HttpCookie = Request.Cookies.Get("CookieName")
If myCookie Is Not Nothing Then
    Label1.Text = myCookie.Value ' Would display "Cookie value"
End If
```

# C#

```
HttpCookie myCookie = Request.Cookies.Get("CookieName");
If (myCookie != null)
{
    Label1.Text = myCookie.Value // Would display "Cookie value"
}
```

In the following two exercises we see how to use the master page to enable the user to select a theme. The first exercise guides you through modifying the master page retrieves the name of the theme the user selects and stores it in a cookie. The second exercise shows you how to apply that theme at run time to every page that inherits from BasePage.

> NOTE There has been a lot of debate about cookies and whether or not they can harm your privacy. Generally, cookies are safe, because they only store data the server already has. They cannot be used to steal sensitive data from your computer if you haven't given this data to your server. In most scenarios, cookies improve the user's browsing experience by remembering little pieces of data instead of asking every single time you visit a page. Unfortunately, large corporations like advertising agencies use a unique cookie to track your tracks on the web, giving them global ideas of the sites you visit. To ensure visitors to your site understand what information you have about them, it is usually a good idea to add a privacy statement to your site describing the intent and usage of cookies and any personal data you may keep. Be aware that in Europe you must comply with the "cookie law" that doesn't allow you to create cookies without the user's consent.

# CHAPTER 6 CREATING CONSISTENT LOOKING WEBSITES

## TRY OUT: Letting the User Select a Theme

In this exercise you add a DropDownList control to the master page. This control contains the available themes you can choose. The user's choice is stored in a cookie so it's available again later. The final step is to preselect the correct theme in the drop-down list when the user revisits the page.

- 1. Open the master page in Markup View and locate the <aside> element. Replace the static text with a DropDownList by dragging it from the Toolbox. Change the ID from DropDown1 to ThemeList. Some type (for example, Select a Theme) followed by a line <br> in front of the drop-down list to clarify the purpose of the text.
- 2. Open the control's Smart Tasks panel (in Design View or Markup View), and enable AutoPostBack.
- 3. On the same Smart Tasks panel, click the Edit Items list and insert two items: one with the text Monochrome and one with the text DarkGrey.
- 4. Double-click the drop-down list in Design View to set up an event handler for the SelectedSelectedIndex event. Instead of double-clicking, you can also select the DropList, press F4 to open its Properties Grid, click the button with the lightning bolt to select the event, and double-click SelectedSelectedIndex. Figure 6-20 shows the Properties Grid in Events mode.

![](/9e033e3b9560597824f8b22941d6d8bb_263_0.png)

FIGURE 6-20

As you aware, you could also add this event handler in Markup View on the control declaration directly.

Any code you write in the SelectedSelectedIndex handler fires at the server when the user makes a selection in the drop-down list with the client. Within the handler block, add the following code that retrieves the theme from the store and stores it in a cookie:

VB.NET

```
Protected Sub ThemeList_SelectedIndex(sender As Object, 
                                e As EventArgs) Handles ThemeList.SelectedIndex
Dim preferredTheme As HttpCookie = New HttpCookie("*PreferredTheme*")
preferredTheme.Expires = DateTime.Now.AddMonths(3)
preferredTheme.Value = ThemeList.SelectedIndexValue
Response.Cookies.Add(preferredTheme)
Response.Redirect(Request.Url.ToString())
End Sub
```

C#

```csharp
protected void ThemeList_SelectedIndexChanged(object sender, EventArgs e)
{
    HttpCookie preferredTheme = new HttpCookie("*PreferredTheme*");
    preferredTheme.Expires = DateTime.Now.AddMonths(3);
    preferredTheme.Value = ThemeList.SelectedIndexValue;
    Response.Cookies.Add(preferredTheme);
    Response.Redirect(Request.Url.ToString());
}
```
