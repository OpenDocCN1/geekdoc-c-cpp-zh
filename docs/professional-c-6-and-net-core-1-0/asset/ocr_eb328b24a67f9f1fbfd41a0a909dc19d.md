information is available. SignalR makes use of the WebSocket technology, and it has a fallback to a pull-based mechanism of communication in case WebSockets are not available.

WebHooks allows you to integrate with public services, and these services can call into your public ASP.NET Web API service. WebHooks is a technology to receive push notification from services such as GitHub or Dropbox and many other services.

The foundation of SignalR connection management, grouping of connections, and authorization and integration of WebHooks are discussed in Chapter 43, “WebHooks and SignalR.”

# Windows Services

A web service, whether it’s done with WCF or ASP.NET Web Services, needs a host to run. Internet Information Server is usually a good option because of all the services it offers, but it can also be a custom program. With the custom option, creating a background process that runs with the startup of Windows is a Windows Service. This is a program designed to run in the background in Windows NT kernel–based operating systems. Services are useful when you want a program to run continuously and be ready to respond to events without having been explicitly started by the user. A good example is the World Wide Web Service on web servers, which listens for web requests from clients.

It is easy to write services in C#. .NET Framework base classes are available in the System.ServiceProcess namespace that handles many of the boilerplate tasks associated with services. In addition, Visual Studio .NET enables you to create a C# Windows Service project, which uses C# source code for a basic Windows Service. Chapter 39, “Windows Services,” explores how to write C# Windows Services.

# Web Applications

The original introduction of ASP.NET 1 fundamentally changed the web programming model. ASP.NET 5 is the new major release, which allows the use of .NET Core for high performance and scalability. This new release can also run on Linux systems, which was a high demand.

With ASP.NET 5, ASP.NET Web Forms is no longer covered (this can still be used and is updated with .NET 4.6), so this book has a focus on the modern technology ASP.NET MVC 6, which is part of ASP.NET 5.

ASP.NET MVC is based on the well-known Model View Controller (MVC) pattern for easier unit testing. It also allows a clear separation for writing user interface code with HTML, CSS, and JavaScript, and it only uses C# on the backend.

> NOTE Chapter 41, “ASP.NET MVC,” covers ASP.NET MVC 6.