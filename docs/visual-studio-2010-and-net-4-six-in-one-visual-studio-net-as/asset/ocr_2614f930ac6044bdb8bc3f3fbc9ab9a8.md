The initial release of Atlas was in January 2007 under the brand of ASP.NET AJAX, and was released as an extension to ASP.NET 2.0. The next milestone was version 3.5 was released as part of ASP.NET 3.5, and received designer support in Visual Studio 2008. ASP.NET 4.0 contains ASP.NET Ajax 4.0, and the Visual Studio 2010 integrated development environment (IDE) adds nice designer features to help with client-side development.

> The ASP.NET team continually publishes previews of the next version of ASP.NET Ajax that you can access at http://aspnet.codeplex.com. As of this writing, a Beta version is available for download.

ASP.NET Ajax has the following pillars:

+   - ASP-NET Ajax Extensions — This is a server-side framework that adds new Ajax functionality to existing server-side code with new web controls using the ScriptManager, the UpdatePanel, and UpdateProgress.
- Microsoft Ajax Library — This is a client-side JavaScript framework that does not depend on ASP.NET on the server, so it can be used with other server-side technologies. Using (or modifying) the Library source code is permitted by the New BSD License.
- ASP.NET Ajax Control Toolkit — This is Open Source project built on top of the Microsoft Ajax Library that provides more than 40 reusable controls and extenders. It is a joint effort between Microsoft and the community, and new controls are continually added to the Toolkit.
- Visual Studio — This provides design-time support and project templates to create Ajax components and Ajax-enabled applications in a productive manner.

The ASP.NET Ajax technology was designed to be cross-browser and a Browser Compatibility Layer ensures that every component built on top of it, ASP.NET supports Internet Explorer 6.0+, Firefox 1.5+, Opera 9.0+, Safari 2.0+, and Google Chrome.

# USING THE ASP.NET AJAX SERVER CONTROLS

Ajax can drastically boost the user experience of web applications — that is, Ajax is friendly with the users. However, when you try to implement it with the XMLHttpRequest object and pure JavaScript, you find that it is completely different from what you are used to on server side — that, Ajax is not friendly with the developers.

If you have chosen ASP.NET (because you need the higher abstraction level it gives to create a server-side web application) and Visual Studio (which like its productivity features), using the XMLHttpRequest object you may feel like going back to the Stone Age. Microsoft felt that, and created the ASP.NET Ajax Extensions component (later became an integral part of ASP.NET) to provide the same high-level control-centric approach for the most (most common) Ajax scenarios in ASP.NET.