608 SQL Server Database Programming with C#

# ## 9.5 BUILD ASP.NET WEB SERVICE TO UPDATE AND DELETE DATA FOR SQL SERVER DATABASE

In this section we discuss how to update and delete a record against the Student table in our database via the Web Services. Two web methods were developed in this service project: SQLUpdateSP and SQLDeleteSP. Both methods call the associated stored procedure to perform the data updating and deleting operations.

Open Studio.NET 2022 and create a new WCF Service Application WebServiceUpDtProject in the folder C:\Chapter 9. Then right-click on the newly created project from the Solution explorer and select Add | New Item to open the Add New Item wizard. Select Web from the left pane and Web Service from the middle pane. Enter WebServiceUpDt.asmx in the Name box, and click Add to add this into your project. As we did in Section 9.3.3, perform the following operations to build this service:

+   1. Modify the namespace to create our Web service namespace.
2. Create a customer base class to handle error-checking codes to protect our real Web service class.
3. Create a customer returned class to hold required or updated student information. This class is a derived class based on the base class above.
4. Add Web methods to our Web service class to access our sample database.
5. Develop the detail code for these Web methods to perform the Web services.

Let's start our jobs based on this sequence now.

# ## 9.5.1 MODIFY THE DEFAULT NAMESPACE AND ADD DATABASE CONNECTION STRING

Open the main service page WebServiceUpDt.asmx by double-clicking on it from the Solution explorer, and change the default namespace to our special one that shown in step A on Figure 9.95.

| WebServiceUpDt Project | HelloWorld() | |
| --- | --- |
| using System.Web.Services; namespace WebServiceUpDt { // /// Summary description for WebServiceUpDt // /// [WebService(Namespace = "https://www.routledge.com/978-1023123354/\/\)] [WebServiceBinding(ConformsTo=ToolItem(false))] [System.ComponentModel] // To allow this Service to be called from script, as ASP.NET AJAX, uncomment the following line. // [System.Web.Script.Services.ScriptService] public class WebServiceUpDt : System.Web.Services.WebService [WebMethod] public string HelloWorld() { return "Hello World"; } } |

FIGURE 9.95 The modified namespace.