# How to use custom error handling

When an error occurs in an ASP.NET application, an exception is thrown. Then, if the exception isn’t handled by the application, an ASP.NET Server Error page is displayed. This page includes an error message, a portion of the source code that threw the unhandled exception, and other debugging information. Since this type of error page usually isn’t appropriate for the users of an application, you typically replace the generic error pages with your own custom error pages after you’re done testing the web site but before you go live with it.

# An introduction to custom error handling

Figure 20-7 describes four techniques you can use to display your own custom error pages. Depending on your application, you may need to use one or more of these techniques.

The first technique is to enclose code that might generate exceptions in a try block of a try-catch statement. Then, you can redirect to a custom error page if an exception does occur.

The second technique is to code a Page_Error method in the code-behind file for a page. This method is called whenever an unhandled exception occurs on the page. Then, in the Page_Error method, you redirect the user to a custom error page.

The third technique is to code an Application_Error method in the global.asax file. This method is called whenever an unhandled exception occurs on a page that doesn’t have a Page_Error method. Then, the Application_Error method can redirect the user to a custom error page.

The fourth technique is to use the customErrors element in the web.config file to designate custom error pages. This technique is used to display custom error pages when common HTTP errors such as a 404 – Not Found error occur.