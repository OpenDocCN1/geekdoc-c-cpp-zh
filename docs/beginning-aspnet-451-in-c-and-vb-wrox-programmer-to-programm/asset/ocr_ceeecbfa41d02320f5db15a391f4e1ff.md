# 242 | CHAPTER 7 NAVIGATION

This would be the case if your site ran under www.PlanetWrox.com/Site rather than under www.PlanetWrox.com, for example. To see what that means, consider this image that uses the tilde in its ImageUrl:

```
<asp:Image ID="Image" runat="server" ImageUrl="~/Images/Header.jpg" />
```

When you use an application folder named Site, the image is searched for at /Site/Images/Header.jpg. If you recount the site to run without an application folder, the image is looked for at /Images/Header.jpg without needing to change any code.

You can also use the ~ syntax on HTML elements, provided you add the runat attribute. This way, the path is processed at the server and returned to the client. The following example shows a plain HTML link that links to a page in the Management folder:

```
<a href="~/Management/Default.aspx" runat="server">Management</a>
```

IIS Express, the web server that serves with VS 2013, will always start a new site at the root directory. That means it will use a URL similar to http://localhost:59898/ and not http://localhost:59898/Site/. Therefore, root-based URLs will work as expected.

# Absolute URLs

In contrast to relative URLs that refer to a resource or site root, you can also use absolute URLs that refer to a resource by its full path. Instead of directly referring to an image optionally specifying a folder, you include the full name of the domain and protocol information (the // prefix). Here's an example that refers to the Wrox logo in the Wrox Programmer Programmer site (http://p2p.wrox.com), where you can go for questions about the Wrox and other books or for general questions regarding programming:

```
<img src="http://p2p.wrox.com/images/header/wrox_logo.gif" />
```

Absolute URLs are required if you want to refer to a resource outside your own website. With such a URL, the // prefix is mandatory. If you leave it out, the browser will look for a folder named p2p.wrox.com inside your own website.

Absolute URLs are unambiguous. They refer to a fixed location, which helps to make sure you're fetching the exact same resource, no matter where the source document is located. You may think that they are ideal for everywhere—including references to resources within your own site—but that is not the case. The protocol and domain information affects the size of the page in the browser, making it unnecessarily slower to download. But more important, it creates difficulties if you are changing your domain name. For example, if you your site was running on www.myapplication.com and you are moving to www.anotherdomain.com, you will need to update all the absolute URLs in the entire website.

You will also have trouble with absolute URLs during development. Often, you test your website on a URL such as http://localhost/. If you were to point all your images to that URL, they would all break as soon as you put your site on a production domain like .www.PlanetWrox.com.,

In short, use absolute URLs with caution. You may need them when referring to resources outside your website, but you should give preference to relative URLs within your own projects wherever possible.