# Common properties of the Exception class

| Property | Description |
|---|---|
| Message | A message that describes the error. |
| Source | The name of the application or object that caused the error. |
| InnerException | The Exception object that caused the exception at the application level. |

# Methods of the HttpServerUtility class for working with exceptions

| Method | Description |
|---|---|
| GetLastError() | Gets the most recent exception. |
| ClearError() | Clears the most recent exception. |

# Code that gets the Exception object at the method level

```
try
{
    statements that could throw an exception
}
catch (Exception ex)
{
    statements that use the Exception object named ex
}
```

# Code that gets the Exception object at the page level

```
Exception ex = Server.GetLastError();
```

# Code that gets the Exception object at the application level

```
Exception ex = Server.GetLastError().InnerException;
```

# Code that displays the error message and source of the Exception object

```
Server.ClearError();
Response.Write(ex.Message + "<br />" + ex.Source);
```

# Description

+   - You can use a try-catch statement in any method of a code-behind file to get the Exception object for an error.
+   - The Page_Error method is executed when an unhandled exception occurs. Within this method, you use the GetLastError method of the Server object to get the Exception object for the error.
+   - If you don’t handle an exception with a try-catch statement or a Page_Error method, an HttpUnhandledException is thrown. Then, you can use the Application_Error method in the global.asax file to handle the exception. To do that, you use the GetLastError method of the Server object to get the Exception object for the HttpUnhandledException, and you use the InnerException property of that exception to get the Exception object that caused the error.
+   - During testing, you may want to use the Write method of the HttpResponse object to write information about the exception to the page. Before you do that, you need to clear the error from the Server object so the ASP.NET Server Error page isn’t displayed.