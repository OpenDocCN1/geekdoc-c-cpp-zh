| Table 13.3: Phases of the Life Cycle of ASP.NET Applications on IIS 7.5 Integrated Mode |
| Phase | Description |
|  | - PostUpdateRequestCache
- LogRequest
- PostLogRequest
- EndRequest
- PreSendRequestHeaders
- PreSendRequestContent |

# ASP.NET Page Life Cycle

When a user requests for an ASP.NET Web page, the page passes through a number of stages that is collectively called the life cycle of an ASP.NET Web page. For example, the life cycle of a page begins when a user requests for a Web page and ends when the page is rendered completely to the browser. When you want a specific action to take place at a particular stage of a page, you should completely understand the page life cycle. Moreover, if you are creating any custom control for your project, you should have a thorough knowledge of the page life cycle as a control’s life cycle depends on the page’s life cycle.
Let’s now understand about the different stages involved in a page’s life cycle.

# Different Stages of an ASP.NET Page

In general, an ASP.NET Web page passes through 8 stages. Table 13.4 lists these stages:

| Table 13.4: Different Stages of an ASP.NET Web Page |
| Stage | Description |
| Page request | Refers that the page’s life cycle begins when a user requests for a Web page. When a user requests for a page for the first time, ASP.NET ascertains whether the request is new or an old one. If request is a new one then the page is compiled and executed. However, if the request is an old one then a cached copy of the page is sent without executing the page. |
| Start | Refers to the stage in which the Request and Response properties of the page are configured. The page also ascertains if the request is an old or a new one by using the IsPostBack property. At this stage, the page’s UICulture property is also configured. |
| Page initialization | Refers to the stage in which each control on the page is assigned a unique ID by setting the UniqueID property. At this stage, if there are any themes, they are added to the page. If the request is an old one, then the postback data is not loaded and control property values still need to be restored to the view state values. |
| Load | Refers to the stage in which if the current request is an old one, the properties of controls on the page are loaded with data from the view state and control state. |
| Postback event handling | Refers that if the request made is an old one, then any event handler can be invoked. |
| Validation | Refers to the stage in which the validation controls used on the page invoke the Validate method. |
| Rendering | Refers that prior to rendering the page, the view state and all the controls on the page are saved. While rendering the page, it invokes the Render method for each control on the page and writes the output of the rendering stage to the OutputStream object of the page’s Response property. |
| Unload | Refers that at this stage the Response and Request properties of the page are unloaded and any cleanup operation, if required, is performed. |