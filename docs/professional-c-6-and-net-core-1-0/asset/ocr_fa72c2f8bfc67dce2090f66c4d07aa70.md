REST architectural style with a service that makes use of SOAP to see these constraints.

Both REST services and services making use of the SOAP protocol make use of a client-server technology. SOAP services can be stateful or stateless; REST services are always stateless. SOAP defines its own message format with a header and body to select a method of the service. With REST, HTTP verbs such as GET, POST, PUT, and DELETE are used. GET is used to retrieve resources, POST to add new resources, PUT to update resources, and DELETE to delete resources.

This chapter takes you through a journey covering various important aspects of ASP.NET Web API—creating a service, using different routing methods, creating a client, using OData, securing the service, and using custom hosts.

> **NOTE** *SOAP and WCF are covered in Chapter 44, “Windows Communication Foundation.”*

# # Creating Services

Let’s start with creating a service. Using the new .NET Core framework, you need to start with an ASP.NET web application and select the ASP.NET Core 1.0 Template Web API (see [Figure 42.1]). This template adds folders and references needed with ASP.NET Web API. You can also use the template Web Application in case you need both web pages and services.