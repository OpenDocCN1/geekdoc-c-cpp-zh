# The Framework Class Library

. .NET Framework includes the Framework Class Library (FCL). The FCL is a set of DLL assemblies that contain several thousand type definitions in which each exposes some functionality. Microsoft is producing additional libraries such as the Windows Azure SDK and the DirectX SDK. Additional libraries provide even more types, exposing even more functionality for your use. In fact, Microsoft is producing many libraries at a phenomenal rate, making it easier than ever for developers to use various Microsoft technologies.

Here are just of the kinds of applications developers can create using these assemblies:

+   - Web services Methods can process message sent over the Internet very easily using Microsoft's ASP.NET XML Web Service technology or Microsoft's Communication Foundation (WCF)

+   - Web Forms/MVC HTML-based applications (websites) Typically, ASP.NET will make database queries and web service calls, combine and filter the returned information, and then present that information in a browser by using any HTML-based user interface.

+   - Rich Windows GUI applications Instead of a webpage to create your UI, you can use the more powerful, high-performance functionality offered by Windows Store, Windows Presentation Foundation (WPF), or Windows Forms technologies. GUI applications can take advantage of controls, menus, and touch, style, and keyboard events, and they can exchange information directly with the underlying operating system. Rich Windows applications can also make database queries and consume web services.

+   - Windows console applications For very simple UI demands, a console application provides a quick and easy way to build an application. Compilers, utilities, and tools are typically implemented as console applications.

+   - Windows services Yes, it is possible to build service applications that are controllable via the Windows Service Control Manager (SCM) by using the .NET Framework.

+   - Database stored procedures Microsoft's SQL Server, IBM's DB2, and Oracle's database servers allow developers to write their stored procedures using the .NET Framework.

+   - Component library The .NET Framework allows you to stand-alone assemblies (components) containing types that can be easily incorporated into any of the previously mentioned applications.

> Important Visual Studio allows you to create a Portable Class Library project. This project type you to create a single class library assembly that works with various application types, including the .NET Framework proper, Silverlight, Windows Phone, Windows Store apps, and Xbox 360.

The FCL contains thousands of types, a set of related types is presented to the developer within a single namespace. For example, the System namespace (which you should become