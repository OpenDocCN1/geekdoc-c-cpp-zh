```
} catch (SmtpException ex) { ErrorMessage.Text = "Something went wrong while sending your message."; }
```

# # Exercise 3 Solution

To understand which exceptions occur in the site and find out they occur (that is, what pages or code files are causing the exceptions) you can log all exceptions using some code in the Application_Error event handler. The exception details you can intercept in this method should help you understand the cause of the exception, which in turn should help in finding a fix for it.

To prevent your users from seeing the "Yellow Screen of Death" error messages, you need to use custom error pages. You should create a simple Web Form that tells the user something went wrong.

To tell the ASP.NET run time to show the contents of that file instead of the error message, you need the following element in your Web.config:

```
<customErrors mode="On" defaultRedirect="~/Errors/AllOtherErrors.aspx">
  <error statusCode="500" redirect="~/Errors/Error500.aspx" />
</customErrors>
```

This element sets up a special page for error code 500 that occurs when your code crashes unexpectedly.

When other exceptions occur, such as a "Page not found" error, users are sent to the more generic AllOtherErrors.aspx page.