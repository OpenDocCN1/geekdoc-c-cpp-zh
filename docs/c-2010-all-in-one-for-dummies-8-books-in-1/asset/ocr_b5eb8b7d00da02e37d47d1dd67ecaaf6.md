# Changing a WCF Service to Use ReST 763

```
List<Conference> conferencesAtLocation(int locationID);
}
```

What does that do for us? It tells the runtime compiler when a URI can call this directly. You can check out the binding itself by looking at the test client, as shown in Figure 4-1.

![](bbox=[0.235, 0.285, 0.861, 0.588])

Figure 4-1:
A ReST binding.

Service added successfully.

Book VII
Chapter 4

Building Web
with ReST

That's not all there is to it, though. We need to create a WebServiceHost.

# Returning data in different ways

The WebServiceHost is a servicehost class that happens to handle ReST very well, so we can use it for that purpose. There are a few ways to do this, just like there are in WCF. These include the following:

+   - .NET application running on a box can be a host. A Windows service, console application, or running WCF application can host it as long as it has access to the network device, it should work.

+   - IIS can host the application, and you can configure it in this code. This involves using a WebWebService object in the service codebehind, and decorating the class with attributes for configuration.

+   - The Web.config file can be set up to define an endpoint. This is the easiest way, and how we do it in Chapter 3. If configured this way, adding other endpoints to the code is a straightforward forward change.