# REST AND WCF

Representational State Transfer (REST) is a style of accepting requests where information is put into the URI for the request. The basic advantages of RESTful services are simplicity, support for caching endpoints, and support for interoperability. Also, REST is lightweight when compared to SOAP, it doesn't need too much XML markup code.

Note that REST is, in itself, a combination of standards, including the following:

+   - HTTP
- URL
- HTML
- XML

WCF provides excellent support for designing and implementing REST-based services through the use of a new binding WebBinding. Support for REST-based services was initially provided in the 3.5 release of WCF.

Following is an example that illustrates how you can use WCF to implement RESTful services in your applications:

```
[ServiceContract]
interface IEmployeeDataService
{
[OperationContract]
[HttpGet]
int GetEmployeeID(string employeeName);
}
```

It is simple to add the [HttpGet] attribute to your method to make it available via a REST format. WCF 4.0 provides greater control over the structure/format of the URL string by expanding the WebGet attribute to allow for a UriTemplate to be specified.

For example, to define a UriTemplate for subtraction with two values being passed, you could use something similar to the following:

```
[WebGet(UriTemplate = "Sub?x=(x)&y=(y)")]
```

If you are creating a WCF service that should be accepting values via an HTTP Post request, you would use the WebInvoke attribute rather than the WebGet. Both attributes are contained in the System.Service.Model.namespace.

# IMPLEMENTING A WCF SERVICE DECLARATIVELY

A declarative WCF service is one that you can implement using a configuration-based, flexible, extensible model. You typically use XML to store a declarative WCF service. Declarative services are those that are defined declaratively in XAML. You can define what you would want your service