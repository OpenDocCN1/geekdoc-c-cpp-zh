4. Save all your changes and close the Global.asax file.

5. Next, open up the Web.config file, and as a direct child of <system.web>, add the following customErrors element:

```
<system.web>
  <customErrors mode="On" defaultRedirect="~/Errors/OtherErrors.aspx" redirectMode="ResponseRewrite">
    <error statusCode="404" redirect="~/Errors/Error404.aspx" />
  </customErrors>
</system.web>
```

Save and close the configuration file.

6. Create a new folder in the root of your website and call it Errors.

7. Inside this new folder, create two new Web Forms and call them Error404.aspx and OtherErrors.aspx, respectively. Make sure both of them are based on your custom template so they are using the main master page and inherit from BasePage. If you followed the exercises in the previous chapter and now use Profile to store the user's favorite theme, refer to the Common Mistakes section at the end of this exercise to learn about the pitfalls of using the master page and BasePage for your custom 404 error page.

8. Set the Title of Error404.aspx to File Not Found. Inside the content placeholder for the main content, add the following markup:

```
<asp:Content ID="Content2" ContentPlaceHolderID="cpMainContent" runat="Server">
<h1>File Not Found</h1>
<p>The page you requested could not be found. Please check out the
<a href="~/" runat="server">Homepage</a>
or choose a different page from the menu.</p>
<p>The Planet Wrox Team</p>
</asp:Content>
```

9. Switch to Design View, double-click the page to set up a Page_Load handler, and add the following code to it:

```
VB.NET
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    Response.Status = "404 Not Found"
    Response.StatusCode = 404
    Response.TrySkipIisCustomErrors = True
End Sub
```

```
C#
protected void Page_Load(object sender, EventArgs e)
{
    Response.Status = "404 Not Found";
    Response.StatusCode = 404;
    Response.TrySkipIisCustomErrors = true;
}
```

10. Open the generic OtherErrors.aspx page, set its Title to An Error Occurred, and enter the following content:

```
<asp:Content ID="Content" ContentPlaceHolderID="cpMainContent" runat="Server">
<h1>An unknown error occurred</h1>
```