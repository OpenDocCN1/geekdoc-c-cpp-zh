# ASP.NET Empty Web Site

The ASP.NET Empty Web Site template gives you nothing but two configuration files (Web.config and Web.Debug.config). The ASP.NET Empty Web Site template is useful if you have a bunch of existing files you want to create a new website or when you want to create your site from scratch. You use this template as the basis for the sample website you build in the book and add folders as you progress through the book.

# ASP.NET Dynamic Data Entities Web Site

This template enables you to create a flexible powerful website to manage data in a database without a lot of manual code. This template is not discussed in this book, but you learn more about the Microsoft ADO.NET Entity Framework that is used by the template in Chapter 14.

# WCF Service

This template enables you to create a website containing one or more Windows Communication Foundation (WCF) Services. A WCF Service is somewhat similar to a service in that it enables you to create methods that are callable over a network. However, WCF services go much further than simple services and offer you lot more flexibility. You see how to create and consume a web service from a browser in Chapter 10.

It seems like you have to make a clear choice up for the right website template, this is really the case. Because an ASP.NET website in VS is essentially just a reference to a folder, it's easy to add types from one template to another. For example, it's perfectly acceptable (and very common) to add a WCF service file to a standard ASP.NET Web Forms Site or an ASP.NET Empty Web Site, as you see in Chapter 10.

# Creating and Opening a New Website

You have a number of different ways to create and open existing websites. The choices you have are largely influenced by the way you access the website (either on your local machine with Visual Studio it or on a remote machine), and whether you want to use IIS (the built-in web server that ships with VS) or the full version of IIS—the web server that comes with Windows.

All the examples in this book assume that you open sites from your local hard drive and that use IIS Express, a trimmed version of IIS, because it's very convenient to develop sites with it. However, Chapter 19 shows how to use and configure the full version of Internet Information Services, or IIS for short. This advanced web server comes with most editions of Windows and is mostly used for production hosting of your websites on the server editions of Windows, and because it's capable of serving web pages in high-traffic scenarios.

# Creating New Websites

The Next It Out section guides you through creating the Planet Wrox website, which is the project you work on in this book. All exercises in the remainder of the book assume you have this website in VS, except where stated otherwise. The exercise instructs you to store your website