
```
<AspNetCompatibilityRequirements(
RequirementsMode:=AspNetCompatibilityRequirementsMode.Allowed)>
```

Just as you did earlier for the ASMX Web service, make a HelloWorld function in your WCF service as shown here:

```
Imports System.ServiceModel
Imports System.ServiceModel.Activation

<ServiceContract(Namespace:="")>
<AspNetCompatibilityRequirements(
RequirementsMode:=AspNetCompatibilityRequirementsMode.Allowed)>
Public Class Service1

    <OperationContract()>
    Public Function HelloWorld() As String
        Return "Hello from WCF Service"
    End Function

End Class
```

Code snippet from Service1

As you can see, there is very little difference between the ASMX and WCF services so far, and you also add the reference the same way.

Now add the WCF service by right-clicking the Silverlight application, selecting Add Service Reference, and then clicking the Discover button, as you did before. You will see both services on the ASP.NET project: Service1.svc and WebService1.asmx. Select Service1.asmx and click OK. Now add the following code to the MainPage.xaml.vb:

```
Partial Public Class MainPage
    Inherits UserControl

    Public Sub New()
        InitializeComponent()
    End Sub

    Private WithEvents svc As New ServiceReference1.WebService1SoapClient
    Private WithEvents svc2 As New ServiceReference2.Service1Client
    Private Sub MainPage_Loaded(ByVal sender As Object,
        ByVal e As System.Windows.RoutedEventArgs) Handles Me.Loaded
        TestSoapCall()
    End Sub

    Private Sub TestSoapCall()
        svc.HelloWorldAsync()
        svc2.HelloWorldAsync()
    End Sub

    Private Sub TestWCFCall()
        TestWCFCall()
    End Sub

    Private Sub svc_HelloWorldCompleted(ByVal sender As Object,
        ByVal e As ServiceReference1.HelloWorldCompletedEventArgs)
        Handles svc.HelloWorldCompleted
        MessageBox.Show(e.Result)
    End Sub
```

```
Private Sub svc2_HelloWorldCompleted(ByVal sender As Object,
    ByVal e As ServiceReference2.HelloWorldCompletedEventArgs)
    Handles svc2.HelloWorldCompleted
    MessageBox.Show(e.Result)
End Sub
End Class
```

Code snippet from MainPage.xaml

This appears to be exactly the same as the ASMX Web service, but this is only an appearance of similarities. The way the code is actually executed is in fact much different because of the way in which WCF binds to the Web service. You can see where it defines this in the ServiceReferences.ClientConfig:

```
<configuration>
    <system.serviceModel>
        <bindings>
            <basicHttpBinding>
                <binding name="WebService1Soap" maxBufferSize="2147483647" maxReceivedMessageSize="2147483647">
                    <security mode="None" />
                </binding>
            </basicHttpBinding>
            <customBinding>
                <binding name="CustomBinding_Service1">
                    <binaryMessageEncoding />
                    <httpTransport maxReceivedMessageSize="2147483647" maxBufferSize="2147483647" />
                </binding>
            </customBinding>
        </bindings>
        <client>
            <endpoint address="http://localhost:38588/WebService1.asmx" binding="basicHttpBinding" bindingConfiguration="WebService1Soap" contract="ServiceReference1.WebService1Soap" name="WebService1Soap" />
            <endpoint address="http://localhost:38588/Service1.svc" binding="customBinding" bindingConfiguration="CustomBinding_Service1" contract="ServiceReference2.Service1" name="CustomBinding_Service1" />
        </client>
    </system.serviceModel>
</configuration>
```

Code snippet from ServiceReferences.ClientConfig

Unlike the basicHttpBinding that the ASMX service assigned to its endpoint, WCF-based services bind using a customBinding. The customBinding is actually defined slightly above the endpoints, and you can see that it is defined to use binaryMessageEncoding. This is what tells Silverlight to use binary messaging to communicate with the Web service, but this only half the story; this binding is also defined in the web.config, as shown here:

```
<?xml version="1.0"?>
<configuration>
    <system.web>
        <compilation debug="true" strict="false" explicit="true" targetFramework="4.0" />
    </system.web>
    <system.webServer>
        <modules runAllManagedModulesForAllRequests="true"/>
    </system.webServer>
```

```
<system.serviceModel>
    <behaviors>
        <serviceBehaviors>
            <behavior name="">
                <serviceMetadata httpGetEnabled="true" />
                <serviceDebug includeExceptionDetailInFaults="false" />
            </behavior>
        </serviceBehaviors>
    </behaviors>
    <bindings>
        <customBinding>
            <binding name="ProVB_SLservices.Web.Service1.customBinding0">
                <binaryMessageEncoding />
                <httpTransport />
            </binding>
        </customBinding>
    </bindings>
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true" />
    <services>
        <service name="ProVB_SLservices.Web.Service1">
            <endpoint address="" binding="customBinding" bindingConfiguration="ProVB_SLservices.Web.Service1.customBinding0" contract="ProVB_SLservices.Web.Service1" />
            <endpoint address="mex" binding="mexHttpBinding" contract="IMetadataExchange" />
        </service>
    </services>
</system.serviceModel>
</configuration>
```

Code snippet from web.config

This not only converts your message to binary, but gives you a significant boost to performance, as the binary objects are also compressed. This method also results in a slight security improvement because the objects are not sent across in plain text, where a network monitoring tool could see the data. It is not, however, secure enough to rely on this as your only method of security — you would still want to rely on SSL and other levels of security for highly secured applications.

While both WCF and ASMX Web services provide a great way to access your data, you still have to define all your function calls between the server and the client. For smaller applications this is not an issue, but imagine applications for which you may have 300 or more database tables that you need to send data back and forth. These types of situations lead us into the next type of service.

## ADO.NET Data Service

Now that you have seen the two most classic examples of Web services, this section looks at one of the latest Microsoft technologies for getting to your data. Microsoft has created ADO.NET Data Services to provide a REST-based Web service to expose LINQ to SQL, Entity Framework, or other ORM technology classes. REST (Representational state transfer) uses traditional Web-based standards to expose data for create, read, update, and delete (CRUD) operations. To do this with WCF, you would have to build your own CRUD operations for every table in your database, which for a large application can be impractical to implement.

To get started with ADO.NET Data Services, we’ll set up a few things in our project that we will use throughout the rest of the chapter. Rather than use the traditional Northwind database, we are going to build our own. We are going to create a basic “issue management system” where we keep track of customers and their issues. To begin, first add a SQL Server Database to the ASP.NET project as shown in Figure 20-4.

![](img/d99870e80390742f93963da7be0b2e61_713_0.png)

## FIGURE 20-4

Visual Studio will create an App_Data folder and place your database in it. Now double-click your database and add two tables, beginning with the Customers table shown in Table 20-1.

## TABLE 20-1: Customers

| COLUMN NAME | TYPE | DESCRIPTION |
|---|---|---|
| CustomerID | Int | Unique identity for customers |
| Name | Varchar (50) | Name of customer |
| PhoneNumber | Varchar (50) | Phone number of customer |
| EMailAddress | Varchar (50) | E-mail address of customer |
| Address | Varchar (50) | Address of customer |
| City | Varchar (50) | City of customer |
| State | Varchar (50) | State of customer |

Now that we have a customer table, we’ll also add an Issues table to keep track of issues for the customer. This will build a basic issue-tracking database. Add the structure for the Issues table as shown in Table 20-2.

## TABLE 20-2: Issues

| COLUMN NAME | TYPE | DESCRIPTION |
|---|---|---|
| IssueID | Int | Unique identity for issues |
| CustomerID | Int | ID of customer to whom the issue belongs |
| IssueDate | Datetime | Date of issue |
| ResolvedDate | Datetime | Date the issue was resolved |
| Description | Varchar (5000) | Description of issue |
| Resolution | Varchar (5000) | Resolution of issue |
