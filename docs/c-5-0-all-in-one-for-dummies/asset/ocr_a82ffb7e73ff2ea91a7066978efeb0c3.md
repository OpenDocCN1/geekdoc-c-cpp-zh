# Working in Visual Studio

You already know the basics of working in Visual Studio in C#; you've been working in Visual Studio all along. Working with Visual Studio in the web world is a little different, but not much. Using Visual Studio to build a web application is a lot like Windows Presentation Foundation (WPF) actually, because web applications have a code element to the design view — the HTML document, in an ASPX file. Then there is a code element, in an ASPX. CS file.

A lot of other files make web pages work, too. There are images and style sheets and script files. All of them have editors in Visual Studio. None of them have a darn thing to do with C#, though, so I won't talk about them much here. For more on those files, see the upcoming section, “Recognizing the other file types” or refer to ASP.NET 3.5 For Dummies (Wiley) by Ken Cox.

![](bbox=[0.12, 0.48, 0.24, 0.62])

The following steps were done in Visual Studio 2012 Professional. If you're using Web Express, the screenshots will look different.

The following steps set up a simple site in Visual Studio. You'll use this site to look at all of Visual Studio's cool web features. Then you can begin looking at more complex sites. Here's all you need to do to set up your simple site:

+   1. Open Visual Studio and click on File, then New, and then Project.
+   2. In the New Project dialog box, select Visual C# in the tree view to the left and then Web, and choose ASP.NET Web Forms Application in the right-side window.
+      I named mine AspNetFirstSample.
+   3. Click OK.
+      Visual Studio makes a project.

Hey, that's it. It runs a lot like all the other projects that you've done, making all the files that you need to make a web project work. To run the project, press <F5>. When you do so, Visual Studio launches Cassini, the Web Server that comes with Visual Studio. Your web browser launches, and your project launches.

The templates that come with Visual Studio today for web applications have a lot of prepopulated content. The Web Forms example has a Default page, along with a Contact and About page, prepopulated. There is already a master page template for the site and configuration and script files in the project. In short, Microsoft has gotten things kicked off for you.