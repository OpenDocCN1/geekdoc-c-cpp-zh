
Table 13.3: Phases of the Life Cycle of ASP.NET Applications on IIS 7.5 Integrated Mode

| Phase | Description |
|---|---|
|  | managed-code. Earlier in IIS 6.0 these processes require manual configuration due to two separate pipelines. |
| The unified pipeline receives the first user request. | Specifies that when a request for an application resource is received for the first time, an application domain is created by using the object of the ApplicationManager class. The application domain is a process that isolates the applications from each other and enables the processing of the user requests. In this phase, the information about an application can also be accessed when the HostingEnvironment object is created within the application domain. |
| For each user request, response objects are created | Refers to the phase in which the response objects, such as HttpContext, HttpRequest, and HttpResponse are created. The HttpContext class has objects, such as the HttpRequest and HttpResponse objects. These objects are valid only to the current user request. Now, the HttpRequest object holds information about the current request. The HttpResponse object holds information sent to the user such as cookies and the final output. |
| An object of the HttpApplication class is created and allocated to the request | Refers to the phase in which the application is started when an object of the HttpApplication class is created. However, if a Global.asax file exists, then an object of the Global.asax class is created instead of the HttpApplication class. The Global.asax class derives from the HttpApplication class and represents an ASP.NET application. The modules that need to be invoked depend on the parent application’s managed-code modules. In addition, it also depends on the modules defined in the Web.config file. You can add or remove modules by specifying the module names in the Web.config file within the modules element of the system.webServer section. |
| The HttpApplication class processes the user request. | Specifies that the HttpApplication class performs the following tasks to process the user request: 1. Validates the user request to confirm that it does not contain any malicious markup. 2. Performs URL mapping to confirm whether any URLs are specified in the UrlMappingsSection section of the Web.config file. 3. Invokes the following events and methods in the same order as displayed: - BeginRequest - AuthenticateRequest - PostAuthenticateRequest - AuthorizeRequest - PostAuthorizeRequest - ResolveRequestCache - PostResolveRequestCache - MapRequestHandler - PostMapRequestHandler - AcquireRequestState - PostAcquireRequestState - PreRequestHandlerExecute - Calls the ProcessRequest method of the IHttpHandler class for the request - PostRequestHandlerExecute - ReleaseRequestState - PostReleaseRequestState - Performs response filtering only if the Filter property for the HttpResponse class is defined. - UpdateRequestCache - PostUpdateRequestCache - LogRequest - PostLogRequest - EndRequest - PreSendRequestHeaders - PreSendRequestContent |

## ASP.NET Page Life Cycle

When a user requests for an ASP.NET Web page, the page passes through a number of stages that is collectively called the life cycle of an ASP.NET Web page. For example, the life cycle of a page begins when a user requests for a Web page and ends when the page is rendered completely to the browser. When you want a specific action to take place at a particular stage of a page, you should completely understand the page life cycle. Moreover, if you are creating any custom control for your project, you should have a thorough knowledge of the page life cycle as a control’s life cycle depends on the page’s life cycle.

Let’s now understand about the different stages involved in a page’s life cycle.

## Different Stages of an ASP.NET Page

In general, an ASP.NET Web page passes through 8 stages. Table 13.4 lists these stages:

Table 13.4: Different Stages of an ASP.NET Web Page

| Stage | Description |
|---|---|
| Page request | Refers that the page’s life cycle begins when a user requests for a Web page. When a user requests for a page for the first time, ASP.NET ascertains whether the request is new or an old one. If request is a new one then the page is compiled and executed. However, if the request is an old one then a cached copy of the page is sent without executing the page. |
| Start | Refers to the stage in which the Request and Response properties of the page are configured. The page also ascertains if the request is an old or a new one by using the IsPostBack property. At this stage, the page’s UICulture property is also configured. |
| Page initialization | Refers to the stage in which each control on the page is assigned a unique ID by setting the UniqueID property. At this stage, if there are any themes, they are added to the page. If the request is an old one, then the postback data is not loaded and control property values still need to be restored to the view state values. |
| Load | Refers to the stage in which if the current request is an old one, the properties of controls on the page are loaded with data from the view state and control state. |
| Postback event handling | Refers that if the request made is an old one, then any event handler can be invoked. |
| Validation | Refers to the stage in which the validation controls used on the page invoke the Validate method. |
| Rendering | Refers that prior to rendering the page, the view state and all the controls on the page are saved. While rendering the page, it invokes the Render method for each control on the page and writes the output of the rendering stage to the OutputStream object of the page’s Response property. |
| Unload | Refers that at this stage the Response and Request properties of the page are unloaded and any cleanup operation, if required, is performed. |

## ASP.NET Pages Life Cycle Events

At each stage of the life cycle of a page, the page raises some events that you can handle by running your own code. For handling control events, you bind the event handler to the specified event by using declarative attributes, such as onclick or handle within code.

ASP.NET Web pages also support automatic event wire-up. This implies that when certain events are raised ASP.NET searches for methods that correspond to that event and automatically executes those methods. If the AutoEventWireup attribute of the @ Page directive is True, page events are automatically bound to the methods used to handle these events. The following are the most common page events:

- Preinit – Refers to the first event that occurs during the life cycle of an ASP.NET Web page. It is used to check the IsPostBack property of the page to determine whether the page is being processed for the first time. It also creates or recreates dynamic controls. It sets the Theme property and master page dynamically. In addition, it gets and sets profile property values.
- Init – Refers to the event that is raised after the initialization of all the controls and applying skin settings. It is used to read or initialize control properties.
- Load – Refers to the OnLoad event method that is called to set the properties of controls and establish database connections. The Page class first calls the OnLoad event method on the Web page and after that calls the event for each child control, until the page is loaded.

### Preinit event

Preinit is the first event that occurs during the page life cycle. It is used to check the IsPostBack property of the page to determine whether the page is being processed for the first time. It also creates or recreates dynamic controls. It sets the Theme property and master page dynamically. In addition, it gets and sets profile property values.

> NOTE
> If the request made is a postback, the control values are not yet restored from view state. When you set a control property at this stage, the value might be overwritten in the next event.

### Init event

This event is raised after the initialization of all the controls and after any skin settings have been applied. It is used to read or initialize control properties.

### Load event

The OnLoad event method is called to set the properties of controls and establish database connections. The Page class calls the OnLoad event method on the Web page and then recursively does the same for each child controls until the page and all controls are loaded.

Let’s now see in detail how the code is parsed and compiled into one or more assemblies.

## Compilation in ASP.NET 4.0

ASP.NET first compiles code into one or more assemblies that are nothing but the files with the extension .dll. You can select multiple languages, such as VB and C#, to write ASP.NET code. When the code is compiled, it is converted into a language-independent and CPU-independent language called Microsoft Intermediate Language (MSIL). Compilation enhances performance, security, stability, and interoperability of a Web application. At runtime, MSIL is translated into CPU-specific instructions, which are specific to the processors of computers running the applications. The advantages of compilation in ASP.NET 4.0 are as follows:

- Improves performance as the complied code does not require additional parsing as the system can identify the precompiled code better.
- Provides security as it lacks readability and abstraction; therefore, the compiled code cannot be reversed.
- Provides stability as during compilation the code is checked for any type of syntax errors, type safety, or any other problem.
