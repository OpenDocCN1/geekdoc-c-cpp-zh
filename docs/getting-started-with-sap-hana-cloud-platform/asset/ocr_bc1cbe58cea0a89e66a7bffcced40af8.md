also prepared a destination file in the book's source code bundle that you can upload called northwind.http. If you prefer to configure the destination manually, then you can do so by plugging in the service URL: http://services.odata.org/V3/Northwind/Northwind.svc.

![](bbox=[0.05, 0.2, 0.85, 0.62])

Figure 7.26: Defining an HTTP Destination Pointing to the Northwind Service

# Defining a Route to the HTTP Destination in the Application Descriptor File

Once the HTTP destination is defined, the next step is to open your HTML5 application's descriptor file and create a route that binds a resource path to the destination. At runtime, the shared dispatcher service will use this route definition to determine when and where to reroute service requests through the Connectivity Service.

The descriptor excerpt contained in Listing 7.5 shows how to define a route that binds the HTTP destination with a resource path. As you can see, this route definition looks rather similar to the one you used to access the sapui5 service.