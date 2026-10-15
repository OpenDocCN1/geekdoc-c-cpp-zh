ASP.NET AJAX server architecture for Web services

Now, let’s describe them one by one.

# ASP.NET AJAX Client Architecture for Web Services

The browser uses proxy classes to call a Web service method. A proxy class is a script generated when a Web page is loaded. The client’s object of the proxy class represents the exposed messages of a Web service. When a user calls a Web service, the client script calls the related Web methods of the proxy class. These calls are made asynchronously through the XMLHttpTP object. You have to enable proxy classes to make a call to a Web service through the library script types contained in the Web service communication layer present in the ASP.NET AJAX client architecture for Web services. The following two approaches are used to call a Web service:

+   Using the HTTP-POST Protocol — Consists of a body containing the data that the client’s browser sends to the server. There is restriction on the amount of data to be transmitted. Therefore, whenever the transmitted data exceeds the size limit of the GET request, you can use the POST request. The transmission of data starts from the client’s browser, when the client serializes the request into the JSON format and sends it as POST data to the server. When the server gets the request, it first de-serializes the data in the JSON format into the .NET Framework compatible type and then makes the actual call to the Web service. In response, the server serializes the return values and passes them back to the client, and the client de-serializes these values into JavaScript objects for processing.

+   Using the HTTP-GET Protocol — Consists of a query string to send the request parameters to the server. The GET request uses the ScriptMethodAttribute attribute to call a configured method of a Web service. The size of the data to be transmitted is restricted to the length of the URL allowed by the client’s browser.

Figure 18.2 shows the ASP.NET AJAX client architecture for Web services:

![](bbox=[0.28, 0.65, 0.78, 0.75])

Figure 18.2: ASP.NET AJAX Client Architecture for Web Services

As shown in Figure 18.2, the elements of the ASP.NET AJAX client architecture are as follows:

+   Custom Service Proxies WCF and ASMX — Contains the client script that the server automatically generates and downloads to the client’s browser.

+   Application Service Proxies Authentication, Profile, Roles — Enables you to log on or log off the Web browser using the JavaScript language without making a round trip to the server. The server authentication application service generates the AuthenticationService proxy class. The Role proxy class enables you to make a group of the users of Web services and treat each group as a single user through the JavaScript language, without making round trips to the server. The server roles application service generates the RoleService proxy class. This approach can be useful to grant or deny the access rights of resources on the server. The Profile proxy class enables clients to get information about the current user’s profile through the JavaScript language without making round trips to the server. The server profile application service generates the ProfileService class.