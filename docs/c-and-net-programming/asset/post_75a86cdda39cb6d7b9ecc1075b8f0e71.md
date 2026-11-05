
## 7. Server-side Object Tags

If an object instance is to be created on the server, then server-side object tags are used. When the page is compiled, an instance of the specified object is created. To specify the object, the identifier attribute is used.

## 8. Server-side Include Directives

With server-side include directives, the raw contents of a file can be included anywhere in an ASP.NET file by specifying the type of the path to filename with the **pathtype** attribute.

## 9. Server-side Comments

To prevent server code from executing, certain character sequences are used to comment it out. Full blocks can also be commented rather than a single line.

## 21.9 Web Application Example

### Simple ASP.NET Web Application

- There are two parts to web application in ASP.NET, the **markup** and the **C#** portions.

### Part I Markup Portion: WebFormTechnical_Info.aspx

```aspx
<%@ Page Language="C#" AutoEventWireup="true"
CodeBehind="WebFormTechnical_Info.aspx.cs"
Inherits="WebApplication.WebFormTechnical_Info" %>

<html>
<body background="Bookrack.bmp">

<TITLE>Most Read Books</TITLE>

<H1 align="center"><FONT color="white" size="7">Displaying <br> Most Read Books
    </FONT></H1>

<P align="left"><FONT color="blue" size="5"><STRONG>

<U>Great Read Times  <%WriteDate();%> </U>

</STRONG></FONT></P>

<FONT size="5" color="yellow"><%WriteBooks();%></FONT>

</body>
</html>
```

### Part II: C# part of a web forms — WebFormTechnical_Info.cs

```csharp
using System;
using System.Web.UI;
using System.Web.UI.WebControls;

public class BooksPage:Page
{
    protected void WriteDate()
    {
        Response.Write(DateTime.Now.ToString());
    }

    protected void WriteBooks()
    {
        Response.Write("<P>Meghdoot-Kalidas</P>");
        Response.Write("<P>Mahabharat-Vyas</P>");
        Response.Write("<P>Ramayana-Valmiki</P>");
    }
}
```

### Execution

- **Server side**  
  A request for an .aspx file causes the ASP.NET runtime to parse the file for code that can be compiled. It then generates a page class that instantiates and populates a tree of server control instances. This page class represents the ASP.NET page.
- **ASP.NET code**  
  The first time a page is requested, the code is compiled. Compiling code in .NET means that a compiler in a first step emits Microsoft Intermediate Language (MSIL) and produces metadata if source code is compiled to managed code.

## 21.10 ASP.NET Life Cycle

The ASP.NET life cycle can broadly be divided into two groups:

1. Application Life Cycle
2. Page Life Cycle

### 1. ASP.NET Application Life Cycle

The application life cycle has the following stages:

![](img/3005a4307e6d8f3bb7e76eea28a92357_690_0.png)

Fig. 21.10.1 ASP.NET application life cycle

### Stage 1: Application Start

1. User makes a request for accessing application resource, a page. Browser sends this request to the web server.
2. The life cycle of an ASP.NET application starts when a request is made by a user. This request is to the Web server for the ASP.NET Application. This happens when the first user normally goes to the home page for the application for the first time.
3. During this time, there is a method called Application_Start which is executed by the web server. Usually in this method, all global variables are set to their default values.
4. A unified pipeline receives the first request and the following events take place:
   - An object of the class ApplicationManager is created for this task.
   - An object of the class HostingEnvironment is created that provides information regarding the resources.
   - Now, top level items in the application are compiled.

### Stage 2: Object Creation

1. The next stage is the creation of the HttpContext, HttpRequest & HttpResponse by the web server.
2. The HttpContext is just the container for the HttpRequest and HttpResponse objects.
3. The HttpRequest object contains information about the current request, including cookies and browser information.
4. The HttpResponse object contains the response that is sent to the client.

### Stage 3: HttpApplication Creation

1. An instance of the HttpApplication object is created and assigned to the request.
2. This object is created by the web server. It is this object that is used to process each subsequent request sent to the application. For example, consider 2 web applications. One is a greeting shop application, and the other is a songs website. For each application, there would have 2 HttpApplication objects created. Any further requests to each website would be processed by each HttpApplication respectively.

### Stage 4: Dispose

This event is called before the application instance is destroyed. During this time, one can use this method to manually release any unmanaged resources.

### Stage 5: Application End

This is the final part of the application. In this part, the application is finally unloaded from memory.

### 2. ASP.NET Page Life Cycle

![](img/3005a4307e6d8f3bb7e76eea28a92357_691_0.png)

Fig. 21.10.2 ASP.NET page life cycle

1. A requested page is loaded into the server memory, processed, and sent to the browser. After sending it is unloaded from the memory. At each of these steps, methods and events are available, which could be overridden according to the need of the application. Required code can be written by overriding the default code.
2. The Page class creates a hierarchical tree of all the controls on the page. All the components on the page, except the directives, are part of this control tree.
3. The page life cycle phases are:
   - Initialization
   - Instantiation of the controls on the page
   - Restoration and maintenance of the state
   - Execution of the event handler codes
   - Page rendering
4. Understanding the page cycle helps in writing specific codes, writing custom controls and initializing them at right time, populate their properties with view-state data and run control behavior code.

### 5. Stages of an ASP.NET page

1. **Page request** - When ASP.NET gets a page request, it decides whether to parse and compile the page, or there would be a cached version of the page; accordingly the response is sent.
2. **Starting of page life cycle** - At this point, the Request and Response objects are set. If the request is an old request or post back, the IsPostBack property of the page is set to true. The UICulture property of the page is also set.
3. **Page initialization** - During this stage, the controls on the page are assigned unique ID by setting the UniqueID property and the themes are applied. For a new request, postback data is loaded and the control properties are restored to the view-state values.
4. **Page load** - In this, control properties are set using the view state and control state values.
5. **Validation** - Validate method of the validation control is called and on its successful execution, the IsValid property of the page is set to true.
6. **Postback event handling** - If the request is a postback (old request), the related event handler is invoked.
7. **Page rendering** - In this, view state for the page and all controls are saved. The page calls the Render method for each control and the output of rendering is written to the OutputStream class of the Response property of page.
8. **Unload** - The rendered page is sent to the client and page properties, such as Response and Request, are unloaded and all cleanup done.

### 6. ASP.NET Page Life Cycle Events

1. At each stage of the page life cycle, the page raises some events, for which the code can be written. An event handler is a subroutine, bound to the event, using declarative attributes such as OnClick or handle.
2. **Page life cycle events**
   - **PreInit** - It is the first event in page life cycle. It checks the IsPostBack property and determines whether the page is a postback. It sets the themes and master pages, creates dynamic controls, and gets and sets profile property values. This event can be handled by overloading the OnPreInit method or creating a Page_PreInit handler.
