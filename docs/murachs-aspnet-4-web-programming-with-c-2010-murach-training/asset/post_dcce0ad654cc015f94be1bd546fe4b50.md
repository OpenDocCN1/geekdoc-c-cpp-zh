
## Section 1

### The essence of ASP.NET web programming

This section presents the essential skills for designing, coding, and testing ASP.NET web applications. After chapter 1 introduces you to the concepts and terms that you need to know for web programming, chapters 2 and 3 teach you the essential skills for designing web forms and writing the C# code that makes them work. Then, chapter 4 shows you how to use the many features for testing and debugging ASP.NET applications. Finally, chapter 5 presents the essential HTML and CSS skills that you will need as an ASP.NET programmer.

When you finish all five chapters, you’ll be able to develop real-world applications of your own. You’ll have a solid understanding of how ASP.NET works. And you’ll be ready to learn all of the other ASP.NET features and techniques that are presented in the rest of this book.

## 1
### An introduction to ASP.NET web programming

This chapter introduces you to the basic concepts of web programming and ASP.NET. Here, you’ll learn how web applications work and what software you need for developing ASP.NET web applications. You’ll also see how the HTML code for a web form is coordinated with the C# code that makes the web form work the way you want it to. When you finish this chapter, you’ll have the background you need for developing web applications of your own.

- **An introduction to web applications** ........................ 4
  Two pages of a Shopping Cart application ........................ 4
  The hardware and software components for web applications ........................ 6
  How static web pages work ........................ 8
  How dynamic web pages work ........................ 10
  How state is handled in ASP.NET applications ........................ 12
- **An introduction to ASP.NET application development** ........................ 14
  The software you need ........................ 14
  The components of the .NET Framework ........................ 16
  Three environments for developing ASP.NET applications ........................ 18
- **A quick preview of how an ASP.NET application works** ........................ 20
  The files used by the Shopping Cart application ........................ 20
  The aspx code for the Order form ........................ 22
  The C# code for the Order form ........................ 24
  How an ASP.NET application is compiled and run ........................ 26
- **Perspective** ........................ 28

### An introduction to web applications

A web application consists of a set of web pages that are generated in response to user requests. The Internet has many different types of web applications, such as search engines, online stores, auctions, news sites, discussion groups, games, and so on.

#### Two pages of a Shopping Cart application

Figure 1-1 shows two pages of a simple web application. In this case, the application is for an online store that lets users purchase a variety of Halloween products, including costumes, masks, and decorations. You'll see parts of this application throughout the book, so it's worth taking the time to become familiar with it in this chapter.

The first web page in this figure is used to display information about the various products that are available from the Halloween store. To select a product, you use the drop-down list that's below the banner at the top of the page. Then, the page displays information about the product including a picture, short and long descriptions, and the product's price.

If you enter a quantity in the text box near the bottom of the page and click the Add to Cart button, the second page in this figure is displayed. This page lists the contents of your shopping cart and provides several buttons that let you remove items from the cart, clear the cart entirely, return to the previous page to continue shopping, or proceed to a checkout page.

Of course, the complete Halloween Superstore application also contains other pages. For example, if you click the Check Out button in the second page, you're taken to a page that lets you enter the information necessary to complete a purchase.

An important point to notice about these pages is that they both contain controls that let the user interact with the page, like the drop-down list and buttons on the Order page. A page that contains controls like these is called a web form, and an ASP.NET application consists of one web form for each page in the application.

### The Order page of a Shopping Cart application

![](img/c024ccf88e28c30c07dd410d4342288f_24_0.png)

### The Cart page of a Shopping Cart application

![](img/c024ccf88e28c30c07dd410d4342288f_24_1.png)

Figure 1-1 Two pages of a Shopping Cart application

### The hardware and software components for web applications

Figure 1-2 shows the basic hardware and software components that are required for a web application. To start, a web application is a type of *client/server application*, which means that the functions of the application are split between a *client* computer and a *server* computer. The client and server computers are connected to one another via the Internet, and they communicate with each other using *HTTP*, or *Hypertext Transfer Protocol*.

To access a web application, you use a *web browser* that runs on a client computer. The most popular web browser is Microsoft’s Internet Explorer, but two alternatives are Mozilla Firefox and Chrome.

The web application itself is stored on the server computer. This computer runs *web server* software that enables it to send web pages to web browsers. Although many web servers are available, the two most popular are Microsoft’s *Internet Information Services* (or IIS) and The Apache Software Foundation’s *Apache HTTP Server*, which is usually just called *Apache*. For ASP.NET applications, though, the server typically runs IIS. Although Apache can be configured to run ASP.NET applications, it doesn’t support all of the features of ASP.NET.

Because most web applications work with data that’s stored in a database, most server computers also run a *database management system* (or *DBMS*). Two popular database management systems for ASP.NET development are Microsoft SQL Server and Oracle. Note, however, that the database server software doesn’t have to run on the same server computer as the web server software. In fact, a separate database server is often used to improve an application’s overall performance.

Although this figure shows the client and server computers connected via the Internet, this isn’t the only way a client can connect to a server in a web application. If the client and the server are on the same *local area network* (or *LAN*), they can connect via an *intranet*. Since an intranet uses the same protocols as the Internet, a web application works the same on an intranet as it does on the Internet.

### Components of a web application

![](img/c024ccf88e28c30c07dd410d4342288f_26_0.png)

### Description

- Web applications are a type of *client/server application*. In that type of application, a user at a *client* computer accesses an application at a *server* computer. In a web application, the client and server computers are connected via the Internet or via an *intranet* (a local area network).
- In a web application, the user works with a *web browser* at the client computer. The web browser provides the user interface for the application. The most popular web browser is Microsoft’s Internet Explorer, but other web browsers like Mozilla Firefox and Chrome may also be used.
- The application runs on the server computer under the control of *web server* software. For ASP.NET web applications, the server typically runs Microsoft’s web server, called *Internet Information Services*, or *IIS*.
- For most web applications, the server computer also runs a *database management system*, or *DBMS*, such as Microsoft’s *SQL Server*. The DBMS provides access to information stored in a database. To improve performance on larger applications, the DBMS can be run on a separate server computer.
- The user interface for a web application is implemented as a series of *web pages* that are displayed in the web browser. Each web page is defined by a *web form* using *HTML*, or *Hypertext Markup Language*, which is a standardized set of markup tags.
- The web browser and web server exchange information using *HTTP*, or *Hypertext Transfer Protocol*.

![](img/c024ccf88e28c30c07dd410d4342288f_26_1.png)
