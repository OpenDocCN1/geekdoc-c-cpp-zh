button. Clicking the Submit button invokes the form’s action method with an HTTP method as defined with the method argument:

```
private static string GetForm() =>
    "<form method=\"post\" action=\"/form\">" +
    "<input type=\"text\" name=\"text1\" />" +
    "<input type=\"submit\" value=\"Submit\" />" +
"</form>";
```

For reading the form data, the HttpRequest class defines a Form property. This property returns an IFormCollection object that contains all the data from the form that is sent to the server:

```
private static string ShowForm(HttpRequest request)
{
    var sb = new StringBuilder();
    if (request.HasFormContentType)
    {
        IFormCollection coll = request.Form;
        foreach (var key in coll.Keys)
        {
            sb.Append(GetDiv(key,
HtmlEncoder.Default.Encode(coll[key])));
        }
        return sb.ToString();
    }
    else return"no form".Div();
}
```

Using the /form link, the form is received with the GET request (see Figure 40.14). When you click the Submit button, the form is sent with the POST request, and you can see the text1 key of the form data (see Figure 40.15).

![](bbox=[0.105, 0.546, 0.895, 0.657])

Figure 40.14

![](bbox=[0.105, 0.696, 0.895, 0.798])

Figure 40.15

# Cookies

To remember user data between multiple requests, you can use cookies. Adding a cookie to the HttpResponse object sends the cookie within the HTTP header from the server to the client. By default, a cookie is