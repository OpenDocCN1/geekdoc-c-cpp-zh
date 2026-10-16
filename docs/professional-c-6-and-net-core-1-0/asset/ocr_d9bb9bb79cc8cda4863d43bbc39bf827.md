Bower Packages tool that you can access by clicking the application context menu Manage Bower Packages. This tool is very similar to the NuGet Package Manager; it just makes it easy to manage Bower packages (see Figure 40.10).

![](bbox=[0.1, 0.14, 0.9, 0.45])

# Figure 40.10

Now that the infrastructure is in place, it’s time to get into the HTTP request and response.

# Request and Response

With the HTTP protocol, the client makes a request to the server. This request is answered with a response.

The request consists of a header and, in many cases, body information to the server. The server uses the body information to define different results based on the needs of the client. Let’s have a look at what information can be read from the client.

To return an HTML-formatted output to the client, the GetDiv method creates a div element that contains span elements with the passed arguments key and value (code file WebSampleApp/RequestAndResponseSample.cs):

```
public static string GetDiv(string key, string value) =>
  $"<div><span>{key}:</span><span>{value}</span></div>";
```

Because such HTML div and span tags are needed to surround strings in following examples, extension methods are created to cover this functionality (code file WebSampleApp/HtmlExtensions.cs):

```
public static class HtmlExtensions
{
  public static string Div(this string value) =>
```