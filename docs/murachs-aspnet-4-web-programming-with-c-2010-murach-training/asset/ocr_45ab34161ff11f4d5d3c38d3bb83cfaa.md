# Common members of the HttpCookieCollection class

| Indexer | Description |
|---|---|
| [name] | The cookie with the specified name. |

| Property | Description |
|---|---|
| Count | The number of cookies in the collection. |

| Method | Description |
|---|---|
| `Add(cookie)` | Adds a cookie to the collection. |
| `Clear()` | Removes all cookies from the collection. |
| `Remove(name)` | Removes the cookie with the specified name from the collection. |

# A method that creates a new cookie and adds it
to the HttpResponse object

```
private void AddCookie()
{
    HttpCookie nameCookie = new HttpCookie("UserName", txtUserName.Text);
    nameCookie.Expires = DateTime.Now.AddYears(1);
    Response.Cookies.Add(nameCookie);
}
```

# A method that retrieves the value of a cookie
from the HttpRequest object

```
protected void Page_Load(object sender, EventArgs e)
{
    if (!IsPostBack)
    {
        if (!(Request.Cookies["UserName"] == null))
            lblUserName.Text = "Welcome back "
                + Request.Cookies["UserName"].Value + ".";
    }
}
```

# A method that deletes a persistent cookie

```
private void DeleteCookie()
{
    HttpCookie nameCookie = new HttpCookie("UserName");
    nameCookie.Expires = DateTime.Now.AddSeconds(-1);
    Response.Cookies.Add(nameCookie);
}
```

# Description

+   - Cookies are managed in collections defined by the HttpCookieCollection class.
+   - To access the cookies collection for a request or response, use the Cookies property of the HttpRequest or HttpResponse object. To refer to these objects, use the Request and Response properties of the page.
+   - To delete a persistent cookie, create a cookie with the same name as the cookie you want to delete and set its Expires property to a time that has already passed. Then, when the client’s system detects that the cookie has expired, it deletes it.

Figure 8-11    How to work with cookies