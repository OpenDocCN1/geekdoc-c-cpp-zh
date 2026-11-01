# What Are Web Services?

Web services are essentially methods that you can call over the Internet and that can optionally return data to the calling code. This makes them ideal for exchanging data between different systems. Because web services are based on solid and well-understood standards, they make it easy to exchange data between different types of platforms and systems. For example, with a web service it's possible to exchange data between an ASP.NET website running on Microsoft Windows and a PHP-based site running on Linux. But at the same time, it's also possible to exchange data between an ASP.NET or PHP website and a client browser using JavaScript.

# Introducing WCF

To build web services in an ASP.NET website, you use Windows Communication Foundation (WCF), Microsoft's platform for service-oriented applications using the .NET Framework. In previous versions of ASP.NET you could also make use of so-called ASMX web services, but these have now been deprecated in favor of WCF. However, this isn't really a problem because WCF can do anything that ASMX web services could do and much more.

WCF supports a number of different underlying network communication technologies such as HTTP, .NET Remoting, Microsoft Message Queuing, and Enterprise Services. This makes it an ideal platform for the exchange of data in a variety of scenarios such as locally on a single machine, on a corporate network, or over the Internet. For public-facing websites such as the Planet Wrox site, HTTP or HTTPS (the secured version of HTTP) is the natural choice because it will work cross-browser and across firewalls.

For information about the other supported technologies, check out this article on the MSDN website at http://msdn.microsoft.com/library/dd943056.aspx or get a copy of Professional WCF 4: Windows Communication Foundation with .NET 4 (Wrox, ISBN: 978-0-470-56314-4).

To build a WCF web service, you add a WCF service (with an .svc extension) to your project. As you see later, you have a few different templates available, each serving a different purpose. Inside this service file you define a Service Contract and an Operation Contract. The Service Contract defines the overall service and the Operation Contract defines the various methods that are available on the service. The following snippet shows a simple WCF service with a single method:

# VB.NET

```
```vbnet
<ServiceContract(Namespace:="")>
<AspNetCompatibilityRequirements(
    RequirementsMode:=AspNetCompatibilityRequirementsMode.Allowed)>
Public Class NameService
    <OperationContract()>
    Public Function HelloWorld(name As String) As String
        Return String.Format("Hello {0}", name)
    End Function
End Class
```
```

# C#

```
```csharp
[ServiceContract(Namespace = "")]
[AspNetCompatibilityRequirements(
```
```