
In this example, the code is set up to expect a DivideByZeroException. This exception is thrown when value2 contains the value 0. Although at first it seems like a good idea to implement exception handling here, it's actually much better to write code that checks for this value before the division is carried out, instead of letting an exception occur:

```
VB.NET
If value2 <> 0 Then
    result = value1 / value2
    ResultLabel.Text = result.ToString()
Else
    ResultLabel.Text = "Sorry, division by zero is not possible."
End If
```

```
C#
if (value2 != 0)
{
    result = value1 / value2;
    ResultLabel.Text = result.ToString();
}
else
{
    ResultLabel.Text = "Sorry, division by zero is not possible.";
}
```

Of course it would even be better if you had placed a CompareValidator on the page, making sure that ValueBox2 could never contain the value zero. Chapter 9 explains how to use this control.

Although Try Catch blocks are useful to catch exceptions that you anticipate, what about errors you don't? How can you deal with unexpected errors? Because they are unexpected, you won't know when they occur, so it's difficult to write code to handle them.

To solve this problem, the next section shows you how you can globally catch and log unhandled exceptions and send information about them by e-mail. This way, you know they occurred, giving you, the page developer, a chance to fix them before they happen again.

## Global Error Handling and Custom Error Pages

To shield your users from the technical details of the exception, you should provide them with a user-friendly error page instead. Fortunately, ASP.NET enables you to define custom error pages: ASPX pages that are shown to the user when an exception occurs. You can map different types of errors (server errors, page not found errors, security problems, and so forth) to different pages.

You define the error page or pages you want to show in the customErrors element of the Web.config file. A typical element looks like this:

```
<customErrors mode="On" defaultRedirect="~/Errors/Error500.aspx"
    redirectMode="ResponseRewrite">
    <error statusCode="404" redirect="~/Errors/Error404.aspx" />
    <error statusCode="500" redirect="~/Errors/Error500.aspx" />
</customErrors>
```

The mode attribute determines whether or not a visitor to your site gets to see a detailed error page.

The attribute supports the following three values:

- `On`—Every visitor to your site always sees the custom error page when an error occurs.
- `Off`—The custom error page is never shown and full error details are displayed on the page.
- `RemoteOnly`—The full error details are shown to local users (browsing the site from the same machine as the site runs on), while all other users get to see the custom error page. This setting enables you to see error messages on your site during development, while your users are always presented with the custom error page.

Within the opening and closing tags of the customErrors element you define separate <error /> elements, one for each HTTP status code you want to support. The previous configuration defines two custom pages: one that is shown when the requested page could not be found (a 404 status code) and one that is shown when a server error occurs (a 500 code).

For all other HTTP status codes you haven't defined explicitly, the defaultRedirect attribute is used to determine the custom error page.

The redirectMode attribute determines the way the new page is shown to the user and is discussed later in this chapter.

Although custom error pages shield your users from the exception details, they don't help in informing you that an exception occurred. All these pages do is hide the real error and show a page with a custom error message instead. To be notified about these exceptions, you could write some code that looks at the exception and then sends you an e-mail with the details. Alternatively, you could write code that inserts the error details in a database, or writes them to a text file.

ASP.NET offers you a handy, central location to write code that is triggered when an exception occurs. You write this code in a special event handler called Application_Error inside the Global.asax file that you saw first in Chapter 11. Inside this event handler, you can collect relevant data about the exception, stick it in an e-mail message, and send it to your own Inbox. This gives you detailed information about exceptions that occur on your site, aiding in fixing the problem as soon as possible. You see how to write this code in the next exercise.

## TRY IT OUT Handling Exceptions Site Wide

In this Try It Out you learn how to write code in the Global.asax file to send the exception message by e-mail. Additionally, you see how to create global error pages that are shown to your user in case of an error.

1. If you didn't add the Global.asax file to your site in Chapter 11, you need to add it first. To do so, right-click the website in the Solution Explorer and choose Add ▸ Add New Item. In the list with templates, select Global Application Class. Leave its name set to Global.asax and click Add.
2. At the top of the Global.asax file, right after the Application directive, add the following Import statement. Note that when adding an Import statement in Markup View, both VB.NET and C# use the keyword Import, rather than Imports and using that you normally use in Code Behind:

```
```vbnet
<%@ Application Language="VB" %>
<%@ Import Namespace="System.Net.Mail" %>
```
```

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
