send an instruction to the browser to fetch a new page. The third option, Server.Transfer, executes at the server. Because there's a difference in client- and server-side redirection, the following sections describe them in more detail.

# Programmatically Redirecting the Client to a Different Page

Each ASPX page has access to a property called Response, which you saw earlier when saving the code for the selected item. The Response object gives you access to useful properties and methods that are all related to the response from the server's browser. Two of these methods are the Redirect and RedirectPermanent methods. These methods send an instruction to the browser to request a new page. If you want to redirect your user to another page in your site or to a completely different website.

The difference between Redirect and RedirectPermanent mainly has to do with search engine optimization. Redirect tells the client that the page moved temporarily. You often use this to redirect a user to a new page based on some action. For example, after filling in a contact form, you may want to send the user to Thank.aspx which displays a message.

RedirectPermanent tells the page has moved permanently. This is useful if you want to tell a search engine to stop looking at an old page, and index the new one instead. For example, imagine your site has a page Index.aspx that you no longer use. Search engines may keep requesting this page. If you add the following code to the Code Behind of Index.aspx, clients (including search engines) are sent to Default.aspx. Moreover, search engines keep note of the permanence of the redirect and will stop redirecting Index.aspx and focus on Default.aspx instead.

VB.NET

```
Protected Sub Page_Load(Sender Object, e As EventArgs) Handles Me.Load
    Response.RedirectPermanent("Default")
End Sub
```

C#

```
protected void Page_Load(object sender, EventArgs e)
{
    Response.Redirect("Default");
}
```

The two methods have a second version (called an overload) that accepts an additional boolean parameter called endResponse, which enables you to exclude any remaining code after the redirect action when you pass False (false in C#) that is usually not necessary, unless you're better off calling the first version, which sends the response by default.

Quite often, when you want to send the user to a different page, you want to send some additional information. You can do that by putting in the query string, the part of the address that comes after the page, separated by a question mark. Consider the following URL:

```
http://localhost:49264/Demos/Target?CategoryId=10&From=Home
```

The entire part (after the question mark) is considered the query string. It consists of name-value pairs, each separated from another by an ampersand (&). In this case, you have two pairs: