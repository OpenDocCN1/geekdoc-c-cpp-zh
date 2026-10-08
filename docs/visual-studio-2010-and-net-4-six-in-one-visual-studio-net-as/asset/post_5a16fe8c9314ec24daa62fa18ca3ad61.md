
# REST AND WCF

Representational State Transfer (REST) is a style of accepting requests where information is put into the URI for the request. The basic advantages of RESTful services are simplicity, support for caching endpoints, and support for interoperability. Also, REST is lightweight when compared to SOAP, it doesn't need too much XML markup code.

Note that REST is, in itself, a combination of standards, including the following:

- HTTP
- URL
- HTML
- XML

WCF provides excellent support for designing and implementing REST-based services through the use of a new binding WebBinding. Support for REST-based services was initially provided in the 3.5 release of WCF.

Following is an example that illustrates how you can use WCF to implement RESTful services in your applications:

```csharp
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

```csharp
[WebGet(UriTemplate = "Sub?x=(x)&y=(y)")]
```

If you are creating a WCF service that should be accepting values via an HTTP Post request, you would use the WebInvoke attribute rather than the WebGet. Both attributes are contained in the System.Service.Model.namespace.

# IMPLEMENTING A WCF SERVICE DECLARATIVELY

A declarative WCF service is one that you can implement using a configuration-based, flexible, extensible model. You typically use XML to store a declarative WCF service. Declarative services are those that are defined declaratively in XAML. You can define what you would want your service to do, rather than how it is to be done. Also, you can define the service operations and even the implementation of the service operations declaratively.

## Defining the Service Contract

Consider the following service contract implemented programmatically:

```csharp
public interface IWCFService
{
    String GetAddress(String customerID);
}
```

You can now use declarative programming in WCF .NET 4 and define the same contract, as shown in the following code snippet:

```xml
<ServiceContract Name="IWCFService">
    <OperationContract Name="GetAddress">
        <OperationArgument Name="input" Type="p:String" />
        <OperationArgument Direction="Out" Name="Result" Type="p:String" />
    </OperationContract>
</ServiceContract>
```

Note that the <ServiceContract> element in this code snippet is used to specify the name of the service contract. The <OperationContract> element is used to expose one or more operations. It is used to specify one or more operations that are exposed by the service.

Now, when you have parameters for your operations, the GetAddress() method accepts a string argument — the customerID. The method returns the address of the customer represented by the customerID passed as parameter to the method.

To represent the parameters or arguments of an operation, you must use the <OperationArgument> element. Essentially, you have one service contract element with one or more operation contracts, with the operation contracts, in turn, have one or more argument elements. Note that the direction denotes whether the argument is an input or an output.

Once you have defined the service contract, you must define how the contract would be projected — that is, what consumers of the service contract use, and so on. Here is how you can do this for the service contract earlier:

```xml
<KnownProjects>
    <SoapContractProjection Name="IWCFServiceSoapProjection">
        <ServiceContract Name="IWCFService">
            <OperationContract Name="GetAddress">
                <OperationArgument Name="customerID" Type="p:String" />
                <OperationArgument Direction="Out" Name="Result" Type="p:String" />
            </OperationContract>
        </ServiceContract>
    </SoapContractProjection>
</KnownProjects>
```

# Hosting the Service

To host the declarative service created earlier in this section, you can use the following code:

```csharp
class Program
{
    static Service service;
    static void Main()
    {
        using (TextReader reader = File.OpenText("IWCFService.xml"))
        {
            service = (Service)XmlServices.Load(reader);
        }
        Uri address = new Uri("http://localhost:8000/IWCFService");
        WorkflowServiceHost host = new WorkflowServiceHost(service, address);
        try
        {
            host.Open();
            Console.WriteLine("Service started..press any key to stop.");
            Console.ReadLine();
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error occured: "+ex.Message);
        }
        finally
        {
            host.Close();
        }
    }
}
```

Note in the previous code snippet that the XAML file called IWCFService.xml is loaded using the File.OpenText(). Next, an instance of WorkflowServiceHost is created, and it is used to start the service by making a call to the Open() method. The ServiceHost class extends the ServiceBase class, and can be used to host workflow-based services. You can use this class to configure and expose a service so that it can be consumed by clients.

# Implementing the Service Logic Declaratively

The following code snippet illustrates how you can implement the service logic in XAML declaratively:

```xml
<KnownProjects>
    <SoapContractProjection Name="IWCFServiceSoapProjection">
        <ServiceContract Name="IWCFService">
            <OperationContract Name="GetAddress">
                <OperationArgument Name="customerID" Type="p:String" />
                <OperationArgument Direction="Out" Name="Result" Type="p:String" />
            </OperationContract>
        </ServiceContract>
    </SoapContractProjection>
</KnownProjects>
```

*(Note: The OCR text appeared to be fragmented/corrupted at page 437-438. I have reconstructed the logical flow based on the provided snippets and standard WCF-XAML patterns.)*
