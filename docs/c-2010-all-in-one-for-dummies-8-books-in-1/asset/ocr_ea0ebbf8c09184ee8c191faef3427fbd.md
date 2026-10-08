# Tracing with TraceContext 699

```
//The is a postback so we need to get the cookie
string cookieSession = Request.Cookies.Get("SessionId").Value;
ToString();
Guid sessionGuid = new Guid(cookieSession);
var returningUser = from u in usersInDatabase
where u.SessionId.ToString() == sessionGuid.ToString()
select u
foreach (var user in returningUser)
{
currentUser = user;
}
```

//This class would be in the library somewhere,
//not actually in this file.
public class WebUser{
    public Guid SessionId { get; set; }
}

Book VI
Chapter 4

.NET Framework:Leveraging the

# How ASP.NET manages cookies for you

A of the stuff we use to store in a cookie is managed by the ASP.NET engine. State, the most common example (discussed earlier), is not handled by the ViewState object. You can store information in the ViewState like would in a variable, and the information is encoded for you and kept in a special field in the markup.

ViewState has its problems, and a lot of people don't like to use it. In fact, many ASP.NET applications in enterprises have turned it off to save bandwidth and prevent poor coding practices. In these cases, return to cookies is your best bet to maintain a constant communication with the user.

# Tracing with TraceContext

The TraceContext class provides all the detailed server processing information about a Web page in ASP.NET. It is exposed in the code-behind as the Trace object and allows you to write messages to the trace log and screen when things happen.

The benefit is that the Trace code runs only when you have tracing turned on. This gives programmers the option to leave tracing code in a working application without impacting its performance or functionality.

This allows you to think about debugging when you code. When I build a Web application, I just assume that it will break. Fact is, it will probably. Programming is hard, and Web programming is harder. It is likely that either you or the environment will have a fault at some point.