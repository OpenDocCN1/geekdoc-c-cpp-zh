# Traditional Page Processing

# Ajax Page Processing

![](bbox=[0.158, 0.137, 0.642, 0.396])

FIGURE 10-1

The second drawback of having a full-page reload has to do with the way the browser renders the page. Because the entire page is replaced, the browser has to dismiss the old one and then draw the new one. This causes the page to “flicker,” which results in an unattractive user experience. You can deploy Ajax techniques to overcome these two problems, as you see in the remainder of the chapter.

The concepts Ajax have been around for many years. Browsers since Internet Explorer 5 have shipped with the XMLHttpRequest object that enabled you to make calls to the server from JavaScript to send and receive data. However, people also used other techniques to emulate the behavior of what is now called Ajax, including Macromedia Flash, iframes, or hidden frames.

However, when Ajax was introduced, things really took off. In an attempt to stay ahead of the curve, Microsoft started building ASP.NET AJAX, the Ajax framework that is fully integrated in ASP.NET and Visual Studio. This framework offers a number of benefits that you as a web developer can take advantage of to create responsive applications.

In particular, ASP.NET AJAX enables you to:

+   * Create flicker-free pages that enable you to refresh portions of the page without a full reload and without affecting other parts of the page
* Provide feedback to your users during these page refreshes
* Update sections of a page and call server-side code on a scheduled basis using a timer
* Access server-side WCF and other services and work with the data they return

The nice thing about ASP.NET AJAX is that it is very easy to get started with. Creating a flicker-free page is a matter of dragging and dropping a few controls from the Toolbox onto your page. When you understand the basics of the Ajax framework, you can extend your knowledge by looking at more advanced topics such as calling WCF services.