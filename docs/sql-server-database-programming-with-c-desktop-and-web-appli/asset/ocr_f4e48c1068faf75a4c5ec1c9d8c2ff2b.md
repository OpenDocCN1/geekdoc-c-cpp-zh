# SQL Server Database Programming with C#

by developing the codes to perform the request to our sample database, exactly to the Faculty table,
to get the desired faculty information.

We will develop our Web service project in the following sequence:

+   1) Modify the default namespace to create our Web service namespace.
2) Create a customer class to handle error-checking process.
3) Create a customer returned class to hold all retrieved and retrieved faculty information. This class is derived from a class based on the base class above.
4) Add methods to our Web service to access our sample database.
5) Develop the detailed codes for those Web methods to perform the Web services.
6) Build a Windows-based and Web-based client to consume the Web service to pick up and display the required information in the GUI.
7) Deploy our completed Web service to Internet Information Service (IIS).

# 9.3.3 MODIFY THE DEFAULT NAMESPACE

First let's modify the Web service namespace to create our own namespace to store our Web project.
Open the main page **WebServiceSelect.asmx** by double-clicking on the Solution Explorer window, and perform the modifications that are shown in Figure 9.13 to do us. Let's have a closer look at this piece of modified codes to see how it works.

A. We need to use our own namespace to replace the default that is used by the Microsoft to tell the ASP.NET runtime from which our Web service is loaded as it runs. This specific namespace is unique because it is the home page of the CRC Press appended with the book's ISBN number. In fact, you can use any location as your specific namespace to store your Web project if you like.

| WebServiceSelect Project | HelloWorld() |
|---|---|
| using System; | |
| using System.Collections.Generic; | |
| using System.Linq; | |
| using System.Web; | |
| using System.Web.Services; | |
| namespace WebServiceSelect_Project | |
| { | |
// <summary>
// Description for summary
//</summary>
| [WebService(Namespace="https://www.nowledge.com/978-1032312354-3/")] | |
| [Binding(ConformsTo=Web.BasicProfile_1)] | |
| [System.ComponentModel.ToolItem(false)] | |
// To allow this Web Service to be called from script, using ASP.NET AJAX, uncomment the following line
// [System.Web.Scripts.Script.Script] |
| public class WebServiceSelect : System.Web.Services.WebService | |
| [WebMethod] | |
| public string HelloWorld() | |
| { | |
| return "Hello World"; | |
| } | |
} | |

FIGURE 9.13 The modified main service page.