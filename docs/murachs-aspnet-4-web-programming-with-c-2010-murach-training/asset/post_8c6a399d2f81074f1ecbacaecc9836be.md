
## How static web pages work

Many of the web pages on the Internet are *static web pages* that don’t change in response to user input. These pages are *HTML* documents that are defined by *HTML*, or *Hypertext Markup Language*.

Figure 1-3 shows how a web server handles static web pages. The process begins when a user at a web browser requests a web page. This can occur when the user enters a web address, called a *URL (Uniform Resource Locator)*, into the browser’s address box or when the user clicks a link that leads to another page.

In either case, the web browser uses HTTP to send an *HTTP request* to the web server. The HTTP request includes information such as the name and address of the web page being requested, the address of the browser making the request, and the address of the web server that will process the request.

When the web server receives an HTTP request from a browser, the server retrieves the requested HTML file from disk and sends the file back to the browser in the form of an *HTTP response*. The HTTP response includes the HTML document that the user requested along with the addresses of the browser and the web server.

When the browser receives the HTTP response, it formats and displays the HTML document. Then, the user can view the content. If the user requests another page, either by clicking a link or typing another web address in the browser’s address box, the process begins again.

Figure 1-3 also shows the components of a URL. The first component is the protocol, in this case, HTTP. In most cases, you can omit the protocol and HTTP is assumed.

The second component is the *domain name*, which identifies your web site. The URL in this figure, for example, includes the domain name for our web site, www.murach.com. The browser uses the domain name to identify the server that’s hosting the web site.

After the domain name, you specify the path where the file resides on the server. Notice that forward slashes are used to separate the components of a path in a URL. After the path, you specify the name of the file you want to display in the browser. In this case, the file is a static web page named *index.htm*.

### How a web server processes static web pages

![](img/c024ccf88e28c30c07dd410d4342288f_28_0.png)

### The components of an HTTP URL

http://www.murach.com/books/cs10/index.htm
protocol domain name path file name

### Description

- A *static web page* is an HTML document that is the same each time it's viewed. In other words, a static web page doesn't change in response to user input. Everyone who views a static web page sees exactly the same content.
- Static web pages are usually simple HTML files that are stored on the web server. When a browser requests a static web page, the web server retrieves the file from disk and sends it back to the browser. Static web pages usually have a file extension of .htm or .html.
- A web browser requests a page from a web server by sending the server an HTTP message known as an *HTTP request*. The HTTP request includes, among other things, the name of the HTML file being requested and the Internet addresses of both the browser and the web server.
- A user working with a browser can initiate an HTTP request in several ways. One way is to type the address of a web page, called a *URL*, or *Uniform Resource Locator*, into the browser's address area and then press the Enter key. Another way is to click a link that refers to a web page.
- A web server replies to an HTTP request by sending a message known as an *HTTP response* back to the browser. The HTTP response contains the addresses of the browser and the server as well as the HTML document that's being returned.

## How dynamic web pages work

A web application consists of one or more web pages that are not static, but that can change in some way each time the page is displayed. Instead of being stored on disk in the form of HTML files, these pages are generated dynamically by the application. As a result, the generated pages are often referred to as *dynamic web pages*.

One of the key differences between static web pages and dynamic web pages is that dynamic web pages are web forms that contain one or more *server controls*, such as labels, text boxes, and buttons. Users work with these controls to interact with the application.

Figure 1-4 shows the basic processing for a dynamic web page. To start, the browser sends an **HTTP** request to the web server (**IIS**) that contains the address of the web page being requested, along with the information that the user entered into the form. When IIS receives this request, it determines that it’s a request for a web form by looking up the extension of the requested page in a list of *application mappings*. These mappings indicate what program a file extension is associated with. Because an .aspx file is associated with ASP.NET, the web server passes the request on to the **ASP.NET application server** for processing. ASP.NET, in turn, manages the execution of the web form that’s requested.

By the way, you should realize that if you’re using IIS 7, an HTTP request may be sent to ASP.NET for processing even if the request isn’t for an .aspx file. That’s because IIS 7 provides a mode that integrates ASP.NET with the IIS server. One advantage of using integrated mode is that it lets you restrict access to static web pages as well as dynamic web pages using the ASP.NET authentication and authorization features you’ll learn about in Chapter 19. To determine whether or not an ASP.NET application uses integrated mode, you use *application pools*. You can learn more about using application pools with IIS 7 in Appendix B.

When the web form is executed, it processes the information the user entered and generates an **HTML** document. If, for example, the web form displays data from a database, it queries the database to get the requested information. Then, it generates a page with that information, which is returned by ASP.NET to the web server. The web server, in turn, sends the page back to the browser in the form of an **HTTP** response, and the browser displays the page. This entire process that begins with the browser requesting a web page and ends with the page being sent back to the client is called a *round trip*.

When a user clicks on a control to start an **HTTP** request, it is called “posting back to the server,” which is referred to as a *postback*. In the Order form in Figure 1-1, for example, the user starts a postback by selecting an item in the drop-down list or by clicking on the Add to Cart button. Then, the web form for the Order page is processed using the new values that the user has entered into the page.

### How a web server processes dynamic pages

![](img/c024ccf88e28c30c07dd410d4342288f_30_0.png)

### The URL for an ASP.NET web page

http://www.microsoft.com/express/product/default.aspx

### Description

- A *dynamic web page* is an HTML document that's generated by a web form. Often, the web page changes according to information that's sent to the web form by the browser.
- When a web server receives a request for a dynamic web page, it looks up the extension of the requested file in a list of *application mappings* to find out which application server should process the request. If the file extension is .aspx, the request is passed on to ASP.NET for processing.
- When the *application server* receives a request, it runs the specified web form. Then, the web form generates an HTML document and returns it to the application server, which passes it back to the web server and from there to the browser.
- The browser doesn't know or care whether the HTML was retrieved from a static HTML file or generated dynamically by a web form. Either way, the browser simply displays the HTML that was returned as a result of the request.
- After the page is displayed, the user can interact with it using its controls. Some of those controls let the user *post* the page *back* to the server, which is called a *postback*. Then, the page is processed again using the data the user entered.
- The process that begins with the user requesting a web page and ends with the server sending a response back to the client is called a *round trip*.
- If you omit the file name from the URL when you use your browser to request a page, IIS will look for a file with one of four names by default: Default.htm, Default.asp, index.htm, and iisstart.asp. (If you're using IIS 7, it will also look for a file with the name index.html or default.aspx.) If you want another page to be displayed by default, you can add the name of that page to this list. See Appendix B (Windows 7 and Windows Vista) or Appendix C (Windows XP) for more information.

Figure 1-4 How dynamic web pages work
