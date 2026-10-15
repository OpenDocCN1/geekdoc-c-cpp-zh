
## Part IV: Internet Applications

- **Chapter 20:** Silverlight and Services
- **Chapter 21:** Working with ASP.NET
- **Chapter 22:** ASP.NET Advanced Features
- **Chapter 23:** ASP.NET MVC
- **Chapter 24:** SharePoint 2010 Development

### Chapter 20: Silverlight and Services

### What You Will Learn in This Chapter

- ASMX Web Service
- ADO.NET Data Services
- WCF RIA Services
- Model-View-ViewModel

As you have seen in the previous chapter, Silverlight offers developers a familiar environment for developing applications. However, Silverlight offers a lot more than the capability to make great-looking websites. Silverlight has rich line-of-business applications too. With Silverlight 3, Microsoft enabled developers to easily create a variety of business applications, including new DataForm controls and Validation controls. Silverlight 4, now in beta and soon to be released, will continue to strengthen Silverlight’s line-of-business support by adding additional features such as trusted offline capabilities and finer control on the offline.

Throughout this chapter you will learn both how to leverage existing Web service technologies and how to use some of the newer technologies targeted toward Silverlight. As with all line-of-business applications, it is important to be able to get to data and then update it back on the server. Silverlight can do this through existing Web services like SOAP or WCF with little modification, or you can use some of the new offerings of ADO.NET Data Services and RIA Services.

This chapter also offers a high-level overview of a commonly suggested best practice for developing Silverlight line-of-business applications called Model-View-ViewModel (MVVM). This suggested best practice is ideal for creating software that is easy to test and maintain.

### Services and Silverlight

In previous chapters, you saw how to use various Web service technologies to get data into Windows Forms applications, and we will continue to use these concepts with regard to Silverlight. For the most part, this chapter is a review of what you already learned in the previous service chapters, but it points out the differences between calling these services in Silverlight compared to any other type of application.

### ASMX Web Service

One of the first Web service types made available in .NET was the ASMX Web service sometimes referred to as SOAP. This simple protocol uses XML to send messages back and forth between the server and the client. ASMX Web services are designed to handle synchronous calls between the client and the server, but with Silverlight you must take a slightly different approach because all calls in Silverlight have to be asynchronous in order to prevent your web browser from locking up while waiting on the Silverlight application to get a response from the server.

To get started, we’ll create a new Silverlight application in Visual Studio and then add a new Web service to the ASP.NET project by right-clicking the project and selecting Add New Item. From the list that appears, select Web Service as shown in Figure 20-1.

![Figure 20-1](img/d99870e80390742f93963da7be0b2e61_707_0.png)

Once you have created a Web service you will be presented with the following code:

```vb
Imports System.Web.Services
Imports System.Web.Services.Protocols
Imports System.ComponentModel

' To allow this Web Service to be called from script,
' using ASP.NET AJAX, uncomment the following line.
' <System.Web.Script.Services.ScriptService()> _
<System.Web.Services.WebService(Namespace:="http://tempuri.org/")> _
<System.Web.Services.WebServiceBinding(ConformsTo:=WsiProfiles.BasicProfile1_1)> _
<ToolboxItem(False)> _
Public Class WebService1
    Inherits System.Web.Services.WebService

    <WebMethod()> _
    Public Function HelloWorld() As String
        Return "Hello World"
    End Function

End Class
```

This is about as basic as you can get for a Web service — a simple HelloWorld function that returns a string. The next step is to reference the Web service from your Silverlight application. Right-click the Silverlight project and select Add Service Reference. The Add Service Reference dialog shown in Figure 20-2 will appear.

![Figure 20-2](img/d99870e80390742f93963da7be0b2e61_708_0.png)

Build your project, then click the Discover button on the right side. When it finds the Web service you just created, click OK. Once you have done this, your Silverlight project will now contain a reference to your service, as well as a new file called `ServiceReferences.ClientConfig` that contains similar code:

```xml
<configuration>
    <system.serviceModel>
        <bindings>
            <basicHttpBinding>
                <binding name="WebService1Soap" maxBufferSize="2147483647"
                    maxReceivedMessageSize="2147483647">
                    <security mode="None" />
                </binding>
            </basicHttpBinding>
        </bindings>
        <client>
            <endpoint address="http://localhost:38588/WebService1.asmx"
                binding="basicHttpBinding"
                bindingConfiguration="WebService1Soap"
                contract="ServiceReference1.WebService1Soap"
                name="WebService1Soap" />
        </client>
    </system.serviceModel>
</configuration>
```

This file is added when using most of the various Web services. As shown in the code, it defines the endpoint address as your local test Web server. When moving a Silverlight application from development to production, you need to change that property to point to your production address.

In addition, when creating a Web service reference, Visual Studio auto-generates a proxy class to make calling the Web service much easier. In this example it is called `WebService1SoapClient` and you can reference it by `ServiceReference1.WebService1SoapClient`. This works the same as adding Web services to other project types except that it generates a function called `<functionname>Async` for every function that is exposed in the Web service, as well as an event called `<functionname>Completed`. This event is where you will receive the results from the Web service function call.

To call that from the Silverlight application, open the code view of the MainPage.xaml and create the following code:

```vb
Private WithEvents svc As New ServiceReference1.WebService1SoapClient

Private Sub MainPage_Loaded(ByVal sender As Object,
ByVal e As System.Windows.RoutedEventArgs) Handles Me.Loaded
    TestSoapCall()
End Sub

Private Sub TestSoapCall()
    svc.HelloWorldAsync()
End Sub

Private Sub svc_HelloWorldCompleted(ByVal sender As Object,
ByVal e As ServiceReference1.HelloWorldCompletedEventArgs) Handles svc.HelloWorldCompleted
    MessageBox.Show(e.Result)
End Sub
```

*Code snippet from WebService1SoapClient*

Unlike calling the Web service from another type of application, with Silverlight you need to create an event handler to handle the `HelloWorldCompleted` event, due to the asynchronous limitations of Silverlight. This is a little different from what you may have done with other Web services, and it does require keeping some things in mind when using this method. This includes updating your user interface to notify the user that you are waiting on something from the server, and disabling buttons that may require the data you are getting back from the server.

With an ASMX Web service, you can also pass more complex objects than just strings to Silverlight. This opens a large set of possibilities for passing data from a database or other server system. While ASMX Web services are simple, they are not always the optimal way of sending data back and forth, as each object is serialized to XML and is not compressed. As you will see in the next example, WCF services offer some of these options with no special configuration or coding.

### WCF Service

The WCF service is almost identical to the ASMX Web service method of creating a connection to the server, but it offers many performance and security benefits over ASMX Web services.

Begin by creating another service: Right-click your ASP.NET application and select Add New Item. Under the Silverlight category you will find a Silverlight-enabled WCF service, as shown in Figure 20-3.

![Figure 20-3](img/d99870e80390742f93963da7be0b2e61_709_0.png)

Creating a Silverlight-enabled WCF service is nearly identical to creating a normal WCF service; the only difference is the following option:
