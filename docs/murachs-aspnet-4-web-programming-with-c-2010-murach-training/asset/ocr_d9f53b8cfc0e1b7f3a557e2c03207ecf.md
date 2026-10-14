# How an ASP.NET application is compiled

![](bbox=[0.13, 0.12, 0.87, 0.455])

# What happens when an ASP.NET page is requested

+   1.  The ASP.NET runtime processes the .aspx file and generates a partial class (Order) that contains the declarations for the form and its controls, and a class (Order_.aspx) that contains the code that will initialize the form, instantiate the controls, and generate the HTML for the web page.
2.  The C# compiler compiles the partial class that contains the control declarations with the partial class defined by the code-behind file for the form into an *assembly* (.dll) that provides the event-handling code for the requested page.
3.  The C# compiler compiles the Order_.aspx class, which inherits the first compiled class (Order), and saves the result as an assembly that's executed when the page is requested.
4.  If necessary, the C# compiler compiles any other class files that are stored in the application's App_Code folder. These classes are saved in a single assembly.
5.  ASP.NET creates an instance of the page from the page's final assembly. Then, ASP.NET raises the appropriate events, which are processed by the event handlers for the page, and the page generates the HTML that's passed back to the web server for the response.

# Description

+   *   The first four steps of this process are done only the first time the aspx page is requested. After that, the page is processed directly from the compiled assemblies.
*   The default name of a web form that you add to a web site is Default.aspx, and the name of the code-behind class for that form is _.Default.

Figure 1-12  How an ASP.NET 4 application is compiled and run