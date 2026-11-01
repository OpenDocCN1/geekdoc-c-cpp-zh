
## ViewName Route Parameter

In the examples of URL routing discussed so far, the action parameter has always matched the name of the page template configured to handle it, such as the Details.aspx page template, which handled the Details page action, and the List.aspx page template, which handled the List action. Having a page template implement a single action makes it focused and easy to maintain. Compared to a traditional ASP.NET WebForms approach (where a single page often tries to support all three item-level actions—Insert, Edit, and Details), single-action page templates are usually simpler. However, you are not limited to having one-to-one relationships between actions and page templates.

If this makes sense in your application, you can have a single page template handle multiple actions. Visual Studio project templates for Dynamic Data web applications include an example of such a page template called ListDetails.aspx. This template combines a GridView control similar to the one in the List page template and a FormView control that displays details of the row currently selected in the grid. This page template can be registered to handle both List and Details actions as shown in this example:

```
RouteTable.Routes.Add(new DynamicDataRoute("{table}")
{
    Action = PageAction.List,
    ViewName = "ListDetails"
});

RouteTable.Routes.Add(new DynamicDataRoute("{table}")
{
    Action = PageAction.Details,
    ViewName = "ListDetails"
});
```

It is actually the ViewName property of the DynamicDataRoute class that determines the name of the page template that will be used to handle the request. If the ViewName was not provided by the route definition, Dynamic Data will assume it to be the same as the Action parameter. Separation of Action from ViewName allows Dynamic Data web applications to change implementation of page templates without breaking the navigation in existing ASPX pages.

## Page Template Lookup Rules

Figure 6.10 summarizes the algorithm Dynamic Data uses to find an appropriate page template and handle an incoming web request. Most of the power and flexibility in this process comes from the ASP.NET routing.

generate a web page. Dynamic page templates typically rely on special controls, such as *DynamicEntity* and *DynamicFilter*, to generate user interface based on metadata information describing the entity type. When dynamically generated user interface is not sufficient, custom page templates can be used to create a unique user interface required for a particular entity type. Page templates do not replace the regular, custom ASP.NET web pages that still need to be used for screens such as home page, login, dashboards, and so on.

Compared to the traditional multi-purpose WebForms pages, which tend to be verbose and have a large number of simple controls, Dynamic Data page templates are typically much smaller and rely on a number of advanced controls, such as *DynamicEntity*, *DynamicFilter*, and *QueryExtender*. By their nature, dynamic controls are much more abstract than the traditional TextBox and DropDownList and therefore can be harder to understand for developers who are new to Dynamic Data.

*Dynamic* page templates work well for applications that need to display a large number of similar-looking pages, which tends to be the case for internal enterprise applications. *Custom* page templates, on the other hand, are better suited when unique functionality is required for a particular entity type, such as when implementing a public-facing web site.

![](img/11b373b78859e17d318fd76939a0df9d_208_0.png)

**FIGURE 7.1** Metadata API at a glance.

At the highest level, the Metadata API represents a *meta model*—metadata information specific to Dynamic Data. This information is most relevant to Dynamic Data web applications and is exposed using APIs (classes, properties, and methods) designed specifically for this purpose. However, presenting *all* information required by Dynamic Data applications in special APIs would mean recreating `System.Reflection` and `System.ComponentModel` APIs, which are well designed and well known, even if not very easy to use. Instead, Dynamic Data tries to strike a balance between creating an API relevant to dynamic web applications and reusing the existing .NET framework APIs.

The next level down includes the metadata information provided by the *data model*. The data access frameworks, such as LINQ to SQL and Entity Framework, provide metadata information you could use to discover entity classes and access their data. Dynamic Data wraps these APIs in a framework-agnostic *provider model* defined in the `System.Web.DynamicData.Providers` namespace. The provider model is also available through the Metadata API. However, this is an advanced topic that requires special attention. You can find a detailed discussion of this subject in Chapter 13, “Building Dynamic List Pages.”

At the lowest level of abstraction is metadata information provided by the .NET runtime. The `Type` class in the `System` namespace provides information about classes, properties, methods, and attributes; it is an incredibly powerful but low-level tool. The `TypeDescriptor` class in the `System.ComponentModel` namespace works at a slightly higher level and has built-in understanding of data annotations. However, using these APIs directly in a

## SOAP API vs REST API

SOAP (Simple Object Access Protocol) and REST (Representational State Transfer) are both popular web service communication protocols. The debate over which one is better — SOAP vs REST — remains a contentious topic in the developer community.

Let's explore them so you can decide which is best for your needs.

- **SOAP:**
  - SOAP is an XML-based protocol for exchanging structured data in web services.
  - It relies on WSDL (Web Services Description Language) to describe the service.
  - It has built-in error handling and security (WS-Security).
- **REST:**
  - REST is an architectural style that uses standard HTTP methods (GET, POST, PUT, DELETE).
  - It can return data in multiple formats, such as JSON, XML, or plain text.
  - It is known for its simplicity, scalability, and performance.

| Feature | SOAP | REST |
|---------|------|------|
| Protocol | XML-based protocol | Architectural style (uses HTTP) |
| Data Format | XML only | JSON, XML, HTML, plain text |
| Security | WS-Security (built-in) | HTTPS (for transport) |
| Performance | Slower (heavy XML payloads) | Faster (lightweight JSON) |
| Use Case | Enterprise, banking, telecom | Web apps, mobile apps, IoT |

**Key Differences:**

- **Flexibility:** REST is more flexible than SOAP as it supports multiple data formats.
- **State:** SOAP is stateless, but REST can be stateless or stateful.
- **Caching:** REST supports extensive caching; SOAP does not.

```
// Example REST request and response
GET /api/users/1 HTTP/1.1
Host: example.com
Accept: application/json

HTTP/1.1 200 OK
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com"
}
```

```xml
<!-- Example SOAP request -->
<?xml version="1.0"?>
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
  <soap:Body>
    <GetUser xmlns="http://example.com">
      <ID>1</ID>
    </GetUser>
  </soap:Body>
</soap:Envelope>
```

## The MetaModel Class

The MetaModel class serves as a root access point for Dynamic Data components to find information about the tables. In particular, the dynamic URL routing functionality relies on the MetaModel to determine if the incoming request is valid and route it to the appropriate page template. Although multiple instances are supported, a typical Dynamic Data application contains a single MetaModel, created and initialized in the Global.asax as shown in the following example:

```
public class Global : HttpApplication
{
    public static readonly MetaModel DefaultModel = new MetaModel();
    void Application_Start(object sender, EventArgs e)
    {
        DefaultModel.RegisterContext(typeof(NorthwindEntities));
    }
}
```

## Data Model Registration

The MetaModel instance is initially empty and requires a call to one of the RegisterContext methods to populate it with MetaTable objects:

```
public void RegisterContext(Type contextType);
public void RegisterContext(Func<object> contextFactory);
public void RegisterContext(DataModelProvider dataModelProvider);
```

In the simplest case, you can initialize the MetaModel by calling the RegisterContext method that takes a type object such as typeof(NorthwindEntities) in the example just shown. MetaModel has built-in support for Entity Framework and LINQ to SQL and expects a type derived from ObjectContext or DataContext, respectively. Using this type, Dynamic Data creates a new instance of the context class whenever a context is required at run time. Any context class registered this way must have a default constructor.

If your context class doesn't have a default constructor or if you need to perform additional initialization steps, you can use the RegisterContext method that takes a context factory delegate as a parameter:

```
public static readonly MetaModel DefaultModel = new MetaModel();
void Application_Start(object sender, EventArgs e)
{
    DefaultModel.RegisterContext(this.CreateContext);
}

private object CreateContext()
{
    NorthwindEntities context = new NorthwindEntities();
```
