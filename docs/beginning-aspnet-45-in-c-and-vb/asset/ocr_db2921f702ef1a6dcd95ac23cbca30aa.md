Useful as themes may be to enable you, the page developer, to quickly change the appearance and even the layout of the site, they become even more useful if you let your users switch them at run time. This way, users can customize the site to their liking. The next section shows you how to accomplish this.

# Dynamically Switching Themes

Switching themes at run time has a few benefits. For example, you can please your users by enabling them to choose a theme with the colors and layout they like. Not everyone appreciates a dark background with white text, so the option to change that at run time is something that many people like. However, you can also deploy themes to help visually impaired users. By creating a theme that has a high-contrast color scheme and a large font size, you make it much easier for people to see your site. The themes in the Planet Wrox website only change screen elements like colors and layout, but it's easy to create a copy of one of those themes and then change the font size and the color scheme.

Because of the way themes are applied to a page at run time, you need to set the theme early on in the page's life cycle, in the PreInit event to be precise. The base page of the website is once again the ideal location to do this, because every page in the site inherits from this class.

To enable users to change the theme, you can offer them a drop-down menu that automatically posts back to the server when they change the active option in the list. At the server, you get the chosen theme from the list, apply it to the page, and then store the selection in a cookie so it can be retrieved on subsequent visits to the website.

Cookies are little pieces of text that you can store on the user's computer. The data you store in a cookie is sent only to the server that set it in the first place, so other sites can't read the cookie from yours. However, because cookies are stored on the user's computer as plaintext, you should never use them to store any sensitive data, such as a password. Storing harmless data like the preferred theme is an excellent use of cookies, though.

To create a cookie so it's stored on the user's computer, you use the Cookies collection on the Response object. This way, the cookie is sent to the browser along with the response. Here's a quick example:

```
VB.NET
Dim myCookie As HttpCookie = New HttpCookie("CookieName")
myCookie.Expires = DateTime.Now.AddMonths(3)
myCookie.Value = "Cookie value"
Response.Cookies.Add(myCookie)
```

```
C#
HttpCookie myCookie = new HttpCookie("CookieName");
myCookie.Expires = DateTime.Now.AddMonths(3);
myCookie.Value = "Cookie value";
Response.Cookies.Add(myCookie);
```

This code sends the cookie to the browser where it will be stored until it expires, which in this example is three months from the day the cookie is set. For each request to a page, the browser sends this cookie back to the server where you can read it again using the Cookies collection of the Request object, like this: