

The routes attribute specifies a couple of route definitions that the shared dispatcher service will use to map external resources (SAPUI5-related resources in this case) onto simple paths, such as /resources.

```json
{
  "welcomeFile": "index.html",
  "routes": [
    {
      "path": "/resources",
      "target": {
        "type": "service",
        "name": "sapui5",
        "entryPath": "/resources"
      },
      "description": "SAPUI5 Resources"
    },
    {
      "path": "/test-resources",
      "target": {
        "type": "service",
        "name": "sapui5",
        "entryPath": "/test-resources"
      },
      "description": "SAPUI5 Test Resources"
    }
  ]
}
```

### Listing 7.2 Sample neo-app.json Application Descriptor File

We'll be looking more closely at some of the other types of attributes you can specify in the upcoming sections. In addition to this overview, you can find a complete outline of the application descriptor file's schema in the SAP HANA Cloud Documentation available online at http://help.hana.ondemand.com. From the landing page, expand HTML5 Applications Development • Developer's GUIDE • APPLICATION DESCRIPTOR FILE to access the detailed syntax diagram and overview.

## 7.3.2 Integrating SAPUI5 Content

Even though SAP HCP allows you to develop your HTML5 application content using the framework(s) of your choice, there are a lot of compelling reasons to standardize around SAPUI5. If you're working with the SAP Web IDE, then there's usually nothing you have to do to prepare for SAPUI5 development; the SAP Web IDE handles all of this up front whenever you create development projects. On the other hand, if you're working with an external IDE, then there is a trick to incorporating SAPUI5 content into your applications.

For a variety of technical reasons, the preferred method of access to the SAPUI5 library files is through a shared service called sapui5. You can access this service within your HTML5 application by specifying a route definition in the application's deployment descriptor. The syntax for specifying such a route is demonstrated in Listing 7.3. Here, the path attribute indicates that any requests containing the /resources path will be processed by the sapui5 service, which will serve up the SAPUI5 content dynamically.

```json
{
  ...
  "routes": [
    {
      "path": "/resources",
      "target": {
        "type": "service",
        "name": "sapui5",
        "entryPath": "/resources"
      },
      "description": "SAPUI5 Resources"
    }
  ]
}
...
```

### Listing 7.3 Defining a Route to the SAPUI5 Library in the Application Descriptor

Once you define a route in the application descriptor, you can use the configured path in your HTML markup, as shown in the excerpt contained in Listing 7.4. At runtime, whenever this HTTP request is triggered, the shared dispatcher service will proxy the request through the sapui5 service and deliver the library content automatically.

```html
<html>
<head>
  <script src="resources/sap-ui-core.js"
    id="sap-ui-bootstrap"
    data-sap-ui-libs="sap.ui.commons"
    data-sap-ui-theme="sap_bluecrystal">
  </script>
  ...
</head>
<...>
</html>
```

### Listing 7.4 Accessing the SAPUI5 Library via the Configured Route Definition

Aside from the upfront route setup, everything from here on out is SAPUI5 development as per usual. As you might expect, this transparency can come in handy whenever you need to port preexisting SAPUI5 apps or content into SAP HCP.

## 7.3.3 Accessing External Resources

Most of the time, the HTML5 applications that you develop on SAP HCP will need to consume data from RESTful services that are not directly accessible from the public Internet. Examples of the types of services you might want to access here include the following:

- OData services developed using other application models supported by SAP HCP, such as Java or SAP HANA XS
- RESTful services hosted by third-party partners or service providers
- On-premise services exposed via the SAP HANA Cloud Connector or SAP HANA Cloud Integration (SAP HCI)

To facilitate these kinds of requests, you can once again turn to the Connectivity Service that we covered in Chapter 6. In order to understand how this works, it’s helpful to look at a demonstration that shows how all the pieces fit together. With that in mind, in the upcoming sections we’ll walk you through a scenario in which you’ll hook up an SAPUI5 application to a sample OData service called “Northwind” that’s hosted on the official OData site. This service defines a handful of intuitive entity types, such as customers, sales order, and so on. You’ll use these entities to create a simple application that allows users to scroll through a customer’s sales orders.

### Creating an HTTP Destination

To get things started, you first need to create an HTTP destination that points to your target OData service. As demonstrated in Chapter 6, this can be achieved by opening the SAP HCP Cockpit and clicking on the DESTINATIONS tab. From here, you can create a new destination by clicking on the NEW DESTINATION... button and filling in the details, as shown in Figure 7.26. For your convenience, we’ve also prepared a destination file in the book's source code bundle that you can upload called northwind.http. If you prefer to configure the destination manually, then you can do so by plugging in the service URL: http://services.odata.org/V3/Northwind/Northwind.svc.

![](img/cf7012644082c115a2181376d9b7486d_313_0.png)

### Figure 7.26: Defining an HTTP Destination Pointing to the Northwind Service

### Defining a Route to the HTTP Destination in the Application Descriptor File

Once the HTTP destination is defined, the next step is to open your HTML5 application's descriptor file and create a route that binds a resource path to the destination. At runtime, the shared dispatcher service will use this route definition to determine when and where to reroute service requests through the Connectivity Service.

The descriptor excerpt contained in Listing 7.5 shows how to define a route that binds the HTTP destination with a resource path. As you can see, this route definition looks rather similar to the one you used to access the sapui5 service. However, in this case, the route target's type property is assigned the value destination, because you're pointing at an HTTP destination.

```json
{
  ...
  "routes": [
    {
      "path": "/resources",
      "target": {
        "type": "service",
        "name": "sapui5",
        "entryPath": "/resources"
      },
      "description": "SAPUI5 Resources"
    },
    {
      "path": "/Northwind.svc",
      "target": {
        "type": "destination",
        "name": "northwind_http"
      },
      "description": "HTTP Destination to Northwind"
    }
  ],
  ...
}
```

### Listing 7.5 Defining a Route to Point to the HTTP Destination

### Using the Route Definition to Access the Backend Service

After you establish your route definition, you can use the configured resource path to proxy access the backend service. This is demonstrated in the SAPUI5 code excerpt contained in Listing 7.6. Here, you're creating an sap.ui.model.odata.ODataModel object to encapsulate access to the Northwind service. As you navigate through entities in the application, you can append various query options on the end of the relative /Northwind.svc path, just like you would if you were hitting the service directly via your browser. At runtime, the dispatcher service will translate these requests and proxy them through the backend service automatically.

```javascript
sap.ui.core.UIComponent.extend("hcbook.chp07.demo.Component", {
  init: function() {
    ...
  }
});

// Define the application's data model:
var oModel =
new sap.ui.model.odata.ODataModel("/Northwind.svc", true);
this.setModel(oModel);
});
```

### Listing 7.6 Using a Route Definition in an SAPUI5 OData Model

## 7.3.4 Configuring Application Security

As you've observed throughout the course of this chapter, the bulk of HTML5 application content is static in nature. Although this simplifies the development process in many ways, it also introduces some challenges when it comes to application security. After all, if users can get their hands on the code, then they can glean insight into what’s going on behind the scenes and potentially discover holes in security.

To prevent these kinds of vulnerabilities, you need to make sure that you lock down access to sensitive resources. This starts with determining who the user is (authentication) and then making sure that the user is authorized to access particular resources (authorization). With these two constraints in place, you can ensure that only authorized users can access HTML5 content and, by extension, the more sensitive resources (e.g., REST-based services) that the HTML5 applications access behind the scenes.

Within the HTML5 programming model, these kinds of checks are configured in the application descriptor file. Here, using a few lines of code, you can declaratively define the appropriate constraints. For example, Listing 7.7 shows how you can turn on authentication in an HTML5 application. Once this change is activated, users will have to log on with their SAP HCP user account in order to access the application.

```json
{
"authenticationMethod": "saml",
"welcomeFile": "index.html",
...
```

### Listing 7.7 Turning on Authentication in the Application Descriptor File

