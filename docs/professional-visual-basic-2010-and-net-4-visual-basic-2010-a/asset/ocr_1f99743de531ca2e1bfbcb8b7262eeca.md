```
ByVal e As ServiceReference1.HelloWorldCompletedEventArgs) Handles svc.HelloWorldCompleted
    MessageBox.Show(e.Result)
End Sub
```

Code snippet from WebService1SoapClient

Unlike calling the Web service from another type of application, with Silverlight you need to create an event handler to handle the HelloWorldComplete function, due to the asynchronous limitations of Silverlight. This is a little different from what you may have done with other Web services, and it does require keeping some things in mind when using this method. This includes updating your user interface to notify the user that you are waiting on something from the server, and disabling buttons that may require the data you are getting back from the server.

With an ASMX Web service, you can also pass more complex objects than just strings to Silverlight. This opens a large set of possibilities for passing data from a database or other server system. While ASMX Web services are simple, they are not always the optimal way of sending data back and forth, as each object is serialized to XML and is not compressed. As you will see in the next example, WCF services offer some of these options with no special configuration or coding.

# WCF Service

The WCF service is almost identical to the ASMX Web service method of creating a connection to the server, but it offers many performance and security benefits over ASMX Web services.

Begin by creating another service: Right-click your ASP.NET application and select Add New Item. Under the Silverlight category you will find a Silverlight-enabled WCF service, as shown in Figure 20-3.

![](bbox=[0.09, 0.49, 0.75, 0.855])

FIGURE 20-3

Creating a Silverlight-enabled WCF service is nearly identical to creating a normal WCF service; the only difference is the following option: