

Listing 18.9 demonstrates how to get the name of the Web server by using the Server property:

## Listing 18.9: Example of the Server Property

```
<%@ webService Language="C#" Class="Util" %>
using System.Web.Services;
public class Util: WebService
{
    [WebMethod(Description="Get The Computer Name of the Web server",EnableSession=false)]
    public string GetComputerName()
    {
        return Server.MachineName;
    }
}
```

## Session Property

The Session property of the WebService class is used to obtain the HttpSessionState instance for the current request. The syntax of this property is:

```
[BrowsableAttribute(false)]
public HttpSessionState Session
{
    get;
}
```

Listing 18.10 demonstrates how to count the number of times the NumberOfSessions method of a Web service has been accessed by a particular session by using the Session property:

## Listing 18.10: Example of the Session Property

```
<%@ webService Language="C#" Class="Util" %>
using System.Web.Services;
public class Util: WebService
{
    [WebMethod(Description="Number of Sessions",EnableSession=true)]
    public int NumberOfSessions()
    {
        if (Session["SessionNumber"] == null) {
            Session["SessionNumber"] = 1;
        }
        else {
            Session["SessionNumber"] = ((int) Session["SessionNumber"]) + 1;
        }
        return ((int) Session["SessionNumber"]);
    }
}
```

Next, let’s find out how to use ASP.NET AJAX with Web services.

## ASP.NET AJAX and Web Services

You can use ASP.NET AJAX to create ASP.NET AJAX enabled Web services. These Web services can be accessed through a client-side scripting language, such as JavaScript. The Web service communication layer enables Web pages to transport data to and from the server. This layer uses AJAX technology to call a Web service. The exchange of data between the client and the server happens in asynchronous mode in the JavaScript Object Notation (JSON) format.

The ASP.NET AJAX Web services architecture is categorized as follows:

- ASP.NET AJAX client architecture for Web services
- ASP.NET AJAX server architecture for Web services

Now, let’s describe them one by one.

## ASP.NET AJAX Client Architecture for Web Services

The browser uses proxy classes to call a Web service method. A proxy class is a script generated when a Web page is loaded. The client’s object of the proxy class represents the exposed messages of a Web service. When a user calls a Web service, the client script calls the related Web methods of the proxy class. These calls are made asynchronously through the XMLHttpRequest object. You have to enable proxy classes to make a call to a Web service through the library script types contained in the Web service communication layer present in the ASP.NET AJAX client architecture for Web services. The following two approaches are used to call a Web service:

- Using the HTTP-POST Protocol — Consists of a body containing the data that the client’s browser sends to the server. There is restriction on the amount of data to be transmitted. Therefore, whenever the transmitted data exceeds the size limit of the GET request, you can use the POST request. The transmission of data starts from the client’s browser, when the client serializes the request into the JSON format and sends it as POST data to the server. When the server gets the request, it first de-serializes the data in the JSON format into the .NET Framework compatible type and then makes the actual call to the Web service. In response, the server serializes the return values and passes them back to the client, and the client de-serializes these values into JavaScript objects for processing.

- Using the HTTP-GET Protocol — Consists of a query string to send the request parameters to the server. The GET request uses the ScriptMethodAttribute attribute to call a configured method of a Web service. The size of the data to be transmitted is restricted to the length of the URL allowed by the client’s browser.

Figure 18.2 shows the ASP.NET AJAX client architecture for Web services:

![](img/e073a4882197be4ab61103cbe0bcb394_959_0.png)

Figure 18.2: ASP.NET AJAX Client Architecture for Web Services

As shown in Figure 18.2, the elements of the ASP.NET AJAX client architecture are as follows:

- Custom Service Proxies WCF and ASMX — Contains the client script that the server automatically generates and downloads to the client’s browser.

- Application Service Proxies Authentication, Profile, Roles — Enables you to log on or log off the Web browser using the JavaScript language without making a round trip to the server. The server authentication application service generates the AuthenticationService proxy class. The Role proxy class enables you to make a group of the users of Web services and treat each group as a single user through the JavaScript language, without making round trips to the server. The server roles application service generates the RoleService proxy class. This approach can be useful to grant or deny the access rights of resources on the server. The Profile proxy class enables clients to get information about the current user’s profile through the JavaScript language without making round trips to the server. The server profile application service generates the ProfileService class.

- Page Methods Proxy – Provides scripting infrastructure for the client script, which enables you to call static methods as if they are the methods of a Web service.

- Web Service Communication Layer – Enables clients to communicate with Web services on the server. This element is a library of client script types. The Web service communication layer consists of the following elements:
  - WebRequest – Provides the functionality to the client script to make a Web request
  - WebRequestManager – Manages the flow of requests when the WebRequest object issues two or more requests for Web services
  - XmlHttpExecutor – Uses the browser's XMLHTTP support to make asynchronous network requests
  - JSON Serialization – Provides the serialization of JavaScript objects into the JSON format
  - XMLHttp – Used to send HTTP request to the server and load the response

## ASP.NET AJAX Server Architecture for Web Services

The ASP.NET AJAX server consists of ASP.NET Web server controls and components that manage the user interface and execution flow of an application. It also manages serialization, validation, and control extensibility. There are also ASP.NET Web services that enable you to access ASP.NET application services for forms authentication, roles, and user profiles.

Figure 18.3 shows the ASP.NET AJAX server architecture of a Web service in which the elements that enable communication with client applications are included:

![](img/e073a4882197be4ab61103cbe0bcb394_960_0.png)

Figure 18.3: ASP.NET AJAX Server Architecture for Web Services

As shown in Figure 18.3, the elements of the ASP.NET AJAX server architecture are as follows:

- Custom Services WCF and ASMX – Provides the functionality to a Web service and returns suitable response to the client.

- Application Service Authentication, Profile, Roles – Enables you to log on or log off through the client JavaScript. The authentication service generates the Authentication proxy class. There is no need to instantiate the authentication service as it is always available to the user of the Web service. The Role service generates the roles information of the currently authenticated user accessed by the client's JavaScript of the role proxy class. The Profile service generates a profile proxy class to get and set the profile properties of the user associated with the current request.

- Page Methods – Enables a method in an ASP.NET page to be called as if it is a Web service method. This element must be defined in the page that performs the page method call.

- Web Service Communication Layer – Enables a server to communicate with the Web services. This element is a library of server script types. The Web service communication layer consists of the following elements:
  - XML Serialization – Performs SOAP requests and returns XML types from a JSON request in Web services.

