and 2.0, you can now take any former ASP.NET application, recompile it on the .NET Framework 4, and run it on a 64-bit processor.

# Localization

ASP.NET and Visual Studio make it easy (well, relatively easy) to localize applications. Through the use of resource files (.resx), strongly typed resource access, and locale-aware data binding, you can build pages that will dynamically change based on the culture settings of the requester.

# Health Monitoring

The built-in health-monitoring capabilities are rather significant features designed to make it easier to manage a deployed ASP.NET application. ASP.NET health monitoring is built around various health-monitoring events (referred to as Web events) occurring in your application. Using the health-monitoring system enables you to perform event logging for Web events such as failed logins, application starts and stops, or any unhandled exceptions. The event logging can occur in more than one place, so you can log to the Event Log or even back to a database. In addition to performing this disk-based logging, you can also use the system to e-mail health-monitoring information.

Besides working with specific events in your application, you can use the health-monitoring system to take health snapshots of a running application. As with many of the features built into ASP.NET, you can extend the health-monitoring system and create your own events for recording application information.

# Easy Access to Data

ASP.NET Web Forms include a set of server controls designed to enable you to easily bind data to user interface elements on a page. Using these data controls can significantly reduce the amount of VB code you would need to write to manually retrieve data and bind to it — sometimes they eliminate the need for VB code altogether. Even better, this functionality is not limited to data coming from a relational database. In fact, several data-source server controls are at your disposal; and you can even create your own.

ASP.NET AJAX 4 adds client-side data-binding with the addition of the DataView control and client-side templates. These tools enable JSON (JavaScript Object Notation) objects to be bound to the values or attributes of elements in a page using a notation similar to that of WPF.

# Administration and Management

The initial release of ASP.NET focused on the developer, and little thought was given to the people who had to administer and manage all the ASP.NET applications. Instead of working with consoles and wizards as they did in the past, administrators and managers of these new applications now had to work with unfamiliar XML configuration files such as machine.config and web.config.

To remedy this situation, if you are using Windows XP or Windows Server 2003, ASP.NET includes a Microsoft Management Console (MMC) snap-in that enables Web application administrators to edit configuration settings easily on-the-fly through IIS. If you are using one of the newer versions of Windows that include IIS 7.0, the IIS Manager has been enhanced to give you the same capabilities of the MMC snap-in.

# VISUAL STUDIO SUPPORT FOR ASP.NET

Visual Studio 2010 offers a wide range of features to assist you in building applications; IntelliSense, code snippets, integrated debugging, CSS style support, and the ability to target multiple versions of the .NET framework are a few examples. When working with ASP.NET you'll see that many of these productivity features also apply when working with inline code, client-side JavaScript code, XML, and HTML markup.