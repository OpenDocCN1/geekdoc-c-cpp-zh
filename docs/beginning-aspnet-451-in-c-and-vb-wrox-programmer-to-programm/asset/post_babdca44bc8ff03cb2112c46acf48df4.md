
Besides visual controls like Menu, navigation is also about structure. A well-organized site is easy for users to navigate. The Web.sitemap file that is used by the navigation controls helps define the logical structure of your site.

Another important part of navigation takes place at the server. Sending a user from one page to another in Code behind some condition is a very common scenario. For example, imagine an administrator entering a new CD or concert in the Management section of the website. When the review is completed, you may want to show the administrator the full details by redirecting her to a new page.

In this chapter, you learn how to use the navigation options at your site. Before you look at the built-in navigation controls, however, you need to understand the different options you have to address the resources in your site, such as ASPX pages and images.

## DIFFERENT WAYS TO MOVE AROUND YOUR SITE

The most common way to move a user from one page to another is by using the <a> element. This element has an `href` attribute that enables you to define the address of a page or other resource you want to link. Between the tags you can place the content you want to link, such as text, an image, or other HTML. The following snippet shows a small example of the <a> element:

```html
<a href="Login.aspx">You can log in here</a>
```

With this code in a web page, after users click the "You can log in here", they are taken to the Login.aspx page, which should be in the same folder as the page that contains the link. 

The <a> element is a server-side control called the HyperLink. It eventually ends up as an <a> element in the page. The NavigateUrl property of this control maps directly to the `href` attribute of the <a> element. For example, a server-side HyperLink in a content page looks like this:

```asp
<asp:HyperLink id="LoginLink" runat="server" NavigateUrl="Login.aspx">
You can log in here;
</asp:HyperLink>
```

Other than the id that is assigned by the ASP.NET runtime, this code is identical to the earlier example. In both cases, the `href` attribute points to the Login.aspx page using a relative URL. The next topic describes the differences between relative and absolute URLs.

```html
<a id="LoginLink" href="Login.aspx">You can log in here</a>
```

## Understanding Absolute and Relative URLs

Key working with links in your site is a good understanding of what a uniform resource locator inside or outside your website can take. A URL is used to uniquely identify a resource in your or another website. These URLs are used in different places, including the `href` attribute of a hyperlink or a <link> element to a css file, the `src` attribute pointing to an image or a JavaScript source file, and the `url()` value of a CSS property. A URL can be expressed as a relative URL or an absolute URL. Both have advantages and disadvantages that you should be aware of.

## Relative URLs

In the previous examples you saw a relative URL that points to another resource to the location where the URL is used. This means the page containing the <a> element and the Login.aspx page both be placed in the same folder in your site. To refer to resources in other folders you can use the following URLs. All the examples are based on a site structure in Figure 7-1.

To link from Login.aspx in the root to Default.aspx in the Management folder, you can use this URL:

```html
<a href="/Management/Default.aspx">Management</a>
```

To refer to Header.jpg from Default.aspx in the Management folder, you can use this URL:

```html
<img src="../Images/Header.jpg" />
```

The leading periods ".." navigate one folder up to the root, and then for each folder you want to go up in the site hierarchy, like the <img> element. 

For a deeper hierarchy, you can use multiple dots, like the <img> element. You can use it to refer to the image pages from the Reviews folder, which is located under the Management folder:

```html
<img src="../Images/Header.jpg" />
```

One benefit of relative URLs is that you can move files to another directory at the same level without breaking your internal links. However, at the same time, it makes it difficult to move files to a different level in the site hierarchy. If you moved the Login.aspx page to a separate folder like Members, the link to the Management folder would break. The New Members folder doesn't have Management as its subfolder, so Management/Default.aspx is no longer a valid link.

To overcome this problem, you can use root-based URLs.

## Root-Based Relative URLs

Root-based relative URLs always start with a leading slash to indicate the root of the site. If you take the link to the Management folder, its root-based version looks like this:

```html
<a href="/Management/Default.aspx">Management</a>
```

Note the leading slash in front of the Management to indicate the root of the site. This link is unambiguous. It always points to the Default.aspx file in the Management folder in the root. With this link, moving the Login.aspx page to a subfolder doesn't break; it still points to the exact same file.

## Relative URLs in Server-Side Controls

With ASP.NET Server Controls, you have another option at your disposal to refer to resources in your website: You can use the tilde (~) character to point to the current root of the site. This is especially useful when you run your website as a separate application folder under the main website.

![](img/9e033e3b9560597824f8b22941d6d8bb_278_0.png)

This would be the case if your site ran under www.PlanetWrox.com/Site rather than under www.PlanetWrox.com, for example. To see what that means, consider this image that uses the tilde in its ImageUrl:

```asp
<asp:Image ID="Image" runat="server" ImageUrl="~/Images/Header.jpg" />
```

When you use an application folder named Site, the image is searched for at /Site/Images/Header.jpg. If you recount the site to run without an application folder, the image is looked for at /Images/Header.jpg without needing to change any code.

You can also use the ~ syntax on HTML elements, provided you add the runat attribute. This way, the path is processed at the server and returned to the client. The following example shows a plain HTML link that links to a page in the Management folder:

```html
<a href="~/Management/Default.aspx" runat="server">Management</a>
```

IIS Express, the web server that serves with VS2013, will always start a new site at the root. Therefore, root-based URLs will work as expected.

## Absolute URLs

In contrast to relative URLs that refer to a resource or site root, you can also use absolute URLs that refer to a resource by its full path. Instead of directly referring to an image specifying a folder, you include the full name of the domain and protocol information (the // prefix). Here's an example that refers to the Wrox logo in the Wrox Programmer site (http://p2p.wrox.com), where you can go for questions about Wrox and other books or for general questions regarding programming:

```html
<img src="http://p2p.wrox.com/images/header/wrox_logo.gif" />
```

Absolute URLs are required if you want to refer to a resource outside your own website. With such a URL, the // prefix is mandatory. If you leave it out, the browser will look for a folder named p2p.wrox.com inside your own website.

Absolute URLs are unambiguous. They refer to a fixed location, which helps to make sure you're fetching the exact same resource, no matter where the source document is located. You may think that they are ideal for everywhere—including references to resources within your own site—but that is not the case. The protocol and domain information affects the size of the page in the browser, making it unnecessarily slower to download. But more important, it creates difficulties if you are changing your domain name. For example, if your site was running on www.myapplication.com and you are moving to www.anotherdomain.com, you will need to update all the absolute URLs in the entire website.

You will also have trouble with absolute URLs during development. Often, you test your website on a URL such as http://localhost/. If you were to point all your images to that URL, they would all break as soon as you put your site on a production domain like .www.PlanetWrox.com.,
