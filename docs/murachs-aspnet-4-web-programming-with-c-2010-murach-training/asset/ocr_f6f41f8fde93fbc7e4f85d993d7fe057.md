# How to test an application using the ASP.NET Development Server

To test an ASP.NET application, you typically start by running it from within Visual Studio as a file-system web site so you can locate and correct any errors you encounter. This initial testing uses the default browser and the ASP.NET Development Server. Then, you test the application with other web browsers to make sure it works with them as well. You’ll learn the techniques for performing both of these types of testing in the topics that follow. In addition, you’ll learn how to use the Exception Assistant that’s displayed if an error occurs while you’re testing an application.

# How to test an application with the default browser

Unless you’ve changed it, Windows uses Internet Explorer as its default browser. Figure 4-1 presents six different ways you can run a web application with the default browser. Three of these techniques start the debugger so you can use its features to debug any problems that might arise. The other three techniques do not start the debugger.

The first time you run a web application using one of the first three techniques, Visual Studio displays a dialog box indicating that debugging isn’t enabled in the web.config file. From this dialog box, you can choose to enable debugging, or you can choose to run the application without debugging. In most cases, you’ll enable debugging so that you can use the debugger with your application.

All of the techniques listed in this figure except the View in Browser command start the application and display the application’s designated start page. However, the View in Browser command displays the selected page. For example, if you right-click the Cart page and choose View in Browser, the Cart page will be displayed. This command is most appropriate for making sure that the pages of an application look the way you want them to.

Notice that when you run an application using the ASP.NET Development Server, the URL for the page that’s displayed identifies the server as “localhost:” followed by a number that’s assigned by the server. In contrast, if you run an application under IIS as shown later in this chapter, the server is identified as just “localhost”.