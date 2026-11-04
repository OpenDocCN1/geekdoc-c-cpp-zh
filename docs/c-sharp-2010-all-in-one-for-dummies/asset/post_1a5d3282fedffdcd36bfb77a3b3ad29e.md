
- 1. Open Visual Studio and click on New Project.
  The New Project dialog box appears.
- 2. In Installed Templates under the Visual C# node, select Web.
- 3. In the box to the right, click ASP.NET Web Service Application.
- 4. Change the Name to ANewService and the Solution to Book7\Chapter2.
  An example is shown in Figure 2-1.
- 5. Click OK.

This process generates a project that has all the right references for a Web service project in ASMX and gives you a sample file to start with.

## Analyzing the file setup

Note that although a Service1.asmx file (and the usual code-behind file) is created, the markup file has only one line in it:

```
<%@ WebService Language="C#" CodeBehind="Service1.asmx.cs" Class="ANewService.Service1" %>
```

This is by design. Nothing goes in the markup file. All the magic is in the code-behind.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_761_0.png)

Figure 2-1: Make a new Web service.

## Breaking down the sample code

The Service1.asmx.cs file does all the work in our new service, starting with the code in the template. Let's run through that code a line at a time:

```
1 using System;
2 using System.Collections.Generic;
3 using System.Linq;
4 using System.Web;
5 using System.Web.Services;
6 
7 namespace ANewService
8 {
9     /// <summary>
10     /// Summary description for Service1
11     /// </summary>
12 [WebService(Namespace = "http://tempuri.org/")]
13 [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]
14 [System.ComponentModel.ToolboxItem(false)]
15     /// To allow this Web Service to be called from script, using ASP.NET AJAX,
16     // uncomment the following line.
17     // [System.Web.Script.Services.ScriptService]
18 public class Service1 : System.Web.Services.WebService
19 {
20
21     [WebMethod]
22     public string HelloWorld()
23     {
24         return "Hello World";
25     }
26 }
```

There are eight things to point out:

- Line 5 brings in the System.Web.Services namespace; it's essential to the rest of the template.
- Line 12 sets the Namespace for the service. The namespace, just like the namespace of your .NET classes, can be anything you want. It doesn't refer to a real place on the Web.
- Line 13 sets the Web Service Binding. WS-I is the Web Services Interoperability organization who (you guessed it) sets even more standards for Web services. Basic Profile 1.1 is more or less the industry standard. You can find out more at http://www.ws-i.org.
- Line 14 declares if the item should be a Toolbox item in design time environments. This declares whether it should show up in design time Toolboxes.
- Line 16 (when uncommented) activates runtime support for AJAX.
- Line 17 is a normal, everyday class definition, but notice that it inherits System.Web.Services.WebService.
- On Line 20, you can see the `[WebMethod]` attribute. This allows you to control what methods are available to the service from the class, and there are a few attributes for fine-grained control.
- The code itself is fairly boring — the functional code is exactly the same as it would be in a normal class. All the things that make it a Web service are in the declaration.

## Running the service

Press F5 and run the service. If all goes well, you should see something like Figure 2-2. This is the default visualization for a service — remember that you didn't make a user interface; IIS did this for you, to make it easier to test. External users can't see this.

Clicking the Service Description gives you the WSDL for the whole service. This is what a non-.NET application needs to build its proxy. Note that all it does is append a ?WSDL to the end of the URL.

Clicking the Hello World link gives you a test screen and implementation guidance for the method. You will have one of these links for every one of the methods in the class marked with WebMethod.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_763_0.png)

Figure 2-2:
Running the default service.

## Building the code for SHARP

First you need to get set up. Here's what you need to do to start using the Web template:

- 1. Add a new Web Service Application project to the solution by right-clicking the solution and selecting Add New Project. Name the project SharpAsmx.
- 2. If you haven't already, add a data connection to the ConferenceDB. The database is downloadable from csharpfordummies.net.
- 3. Right-click on the SharpAsmx project and add an Entity Data Model by selecting Add ...New Item and picking ADO.NET Entity Data Model from the list. (It's under Data.) I named it SHARP.edmx.
- 4. When the Entity Data Model wizard appears, select Generate from Database and click Next.
- 5. In Choose Your Data Connection, pick the ConferenceDb you added in Step 1. Keep the rest of the defaults.
- 6. When it asks you to copy the file to your project, choose No. You don't need copies of the database floating around.
- 7. In Choose Your Database Objects, pick all the tables except sysdiagrams, and change the Model Namespace to SharpModel. An example appears in Figure 2-3.
- 8. Click Finish.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_764_0.png)

Figure 2-3: Adding the Sharp tables to the model.

That's how you set up an ASMX Web service project. You have a data source, an entity model (you could use your organization's domain model, or hand-rolled procedures and ADO.NET, or whatever), and a starting point for the service.

Next, you set up some services that make sense of your user interface. There are two schools of thought on this. First, you can roll up the entity model in the service signature itself. Second, you could write a separate business layer and just call the Business Layer (BL) methods with the services.

The deciding factor is reuse. If you will later need to roll exactly this logic into a standalone application (anything that won't use the services), then make a separate BL. For simplicity, we will do the former.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_765_0.png)

- 1. Using the default template, delete the default HelloWorld method and put in a method signature for a new conferencesAtLocation method. It will accept a conferenceId (maybe from Web site navigation) and return a list of conferences at that location.

```csharp
public List<Conference> conferencesAtLocation(int locationId)
{
}
```

- 2. The first step is just to get the entities from the Entity Data Model. Add the bold lines. They set up a context for the Entity Framework, then get the list of conferences.

```csharp
public List<Conference> conferencesAtLocation(int locationId)
{
    ConferenceDbEntities conferenceContext = new ConferenceDbEntities();
    ObjectSet<Conference> allConferences = conferenceContext.Conferences;
}
```

- 3. Next, write a Linq query to just get the conferences with the locationId. This is in the bold lines below.

```csharp
public List<Conference> conferencesAtLocation(int locationId)
{
    ConferenceDbEntities conferenceContext = new ConferenceDbEntities();
    ObjectSet<Conference> allConferences = conferenceContext.Conferences;
    var conferenceQuery = from c in allConferences
                          where c.LocationId == locationId
                          select c;
}
```

- 4. In order to use the results of the Linq query, you must use an iterator. You need to dispose of the context. Finally, you return the results. These steps are in the bold lines added below.

```csharp
public List<Conference> conferencesAtLocation(int locationId)
{
    ConferenceDbEntities conferenceContext = new ConferenceDbEntities();
    ObjectSet<Conference> allConferences = conferenceContext.Conferences;
    var conferenceQuery = from c in allConferences
                          where c.LocationId == locationId
                          select c;
    List<Conference> locationConferences = conferenceQuery.ToList();
    conferenceContext.Dispose();
    return locationConferences;
}
```

- 5. To make it a Web service, you need to add the WebMethod decorator on the method signature, and you are done.

```
[WebMethod]
public List<Conference> conferencesAtLocation(int locationId)
{
ConferenceDBEntities conferenceContext = new ConferenceDBEntities();
ObjectSet<Conference> allConferences = conferenceContext.Conferences;
var conferenceQuery = from c in allConferences
where c.LocationId == locationId
select c;
List<Conference> locationConferences = conferenceQuery.ToList();
conferenceContext.Dispose();
return locationConferences;
}
```

- 6. Press F5 to run the test page, and click on the conferencesAtLocation method link. Enter 3 into the Test field, and the result should come back like Figure 2-4 if everything is good.

So what about all that other stuff that goes into SOAP? Security, transactions, and like that? It's all baked in, but it's well beyond the scope of this book.

For instance, check out the SoapHeader attribute. It allows you to specify even the most complex security attributes on your Web methods. There's more, too. Check out MSDN.

## Deploying

Deploying an XML Web Service is just like deploying a Web application. They are effectively the same thing.

One benefit of ASMX over WCF is the simple configuration. In fact, if you check out the configuration file for the application you built here, you'll see that the only configuration information revolves around the Entity Model. Adding an ASMX service to a Web project is easy.

Something important that you need to know: After you deploy, the sample test page doesn't run anymore. You'll still get the information service page, but if you try to run the test script, you'll get the message shown in Figure 2-5. This is just for security and can be overridden, though I don't advise overriding it in a production setting.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_766_0.png)

Book VII
Chapter 2
Building Web Services with ASMX
