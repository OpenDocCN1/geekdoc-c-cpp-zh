![](bbox=[0.32, 0.08, 0.58, 0.38])

# Figure 17.6: Showing the Files that Constitute a New Web Site to Host a Silverlight 3.0 Application

As shown in Figure 17.6, there are several files in the Web application, SampleSilverlightApplication.Web. Broadly, a Web application within a Silverlight 3.0 application has three essential files as follows:

+   - An ASP.NET file – Loads when a Silverlight application run and hosts the MainPage.xaml XAML file. In our case, the ASP.NET file is the SampleSilverlightApplicationTestPage.aspx (Figure 17.6). An ASP.NET file is the default startup page of a Silverlight 3.0 application.
+   - An HTML file (a test page) – Hosts the Silverlight application. In our case, the HTML file is SampleSilverlightApplicationTestPage.html (Figure 17.6).
+   - A JavaScript helper file – Provides methods, such as createObject() and createObjectEx(), to embed a Silverlight application in a Web page. The createObject() and createObjectEx() methods are used to create and initialize the Silverlight content in an ASPX or HTML test page that hosts the Silverlight application. In our case, the JavaScript helper file is Silverlight.js (Figure 17.6).

Depending on the host application that you select, there may be other files that are automatically added to the project. Normally, you use the predefined project templates in Visual Studio 2010. Now, let’s discuss each of the files in detail beginning with the ASP.NET and HTML files that host the Silverlight applications.

# The ASP.NET and HTML Host Pages (Test Pages)

Whenever you create a Silverlight application, you need a page to host that Silverlight application. In Visual Studio 2010, you can opt to host a Silverlight application in either a simple HTML Web page or an ASP.NET Web application. In Visual Studio 2010, when you select an ASP.NET Web application project to host a Silverlight application, an ASP.NET Web application is automatically added to a Silverlight application. The ASP.NET Web application contains two test pages, which are ASP.NET and HTML test pages, created by default for an entire Silverlight application. In other words, it means that the ASP.NET and HTML pages are the test pages that are used to host your Silverlight content. The ASP.NET and HTML test pages can be used to test XAML content of a Silverlight application during the development of the application. In addition, they have the same name as the Silverlight application suffixed with the text TestPage.

The HTML test page (that is, .html test page) largely contains the same code as the TestPage.html file of Silverlight applications that are hosted in a single HTML page. This means that the HTML test page contains the code to create and initialize a Silverlight application. The ASP.NET test page (that is, .aspx test page) contains the equivalent ASP.NET code of the HTML test page. In addition, the ASP.NET test page is the default startup page, as it is the first page that appears when users run a Silverlight application. You can find the ASP.NET and HTML test pages in Solution Explorer, as shown in Figure 17.7: