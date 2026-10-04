systems. Because web services are based on solid and well-understood standards, they make it easy to exchange data between different types of platforms and systems. For example, with a web service it's possible to exchange data between an ASP.NET website running on Microsoft Windows and a PHP-based site running on Linux. But at the same time, it's also possible to exchange data between an ASP.NET or PHP website and a client browser using JavaScript.

WCF service methods are the topic of the next section.

#  Introducing WCF

To build web services in an ASP.NET website, you use Windows Communication Foundation (WCF), Microsoft's platform for service-oriented applications using the .NET Framework. In previous versions of ASP.NET you could also use of so-called ASMX web services, but these have now been deprecated in favor of WCF. However, this isn't really a problem because WCF can do anything ASMX services could and much more.

WCF supports a variety of differing network communication technologies such as HTTP, .NET Remoting, Microsoft Message Queuing, and Enterprise Services. This makes it an ideal platform for the exchange of data in a variety of scenarios such as locally on a machine, on a corporate network, or over the Internet. For public-facing websites such as the Planet Wrox site, HTTP or HTTPS (the secured version of HTTP) is the natural choice which will work cross-browser and across frameworks.

For information about the supported technologies, check out this article on the MSDN website at http://microsoft.com/library/dd94056.aspx or get a copy of Professional WCF 4: Windows Communication Foundation with .NET 4 by Pablo Cibraro, Kurt Claays, Fabio Cozzolino, Johann Grabnerer; Wrox, 2010; ISBN: 978-0-470-56314-4.

To build a web service, you add a WCF service (with an .svc extension) to your project. As you see, you have a few different templates available, each serving a different purpose. Inside this service file you define a Service Contract and an Operation Contract. The Service Contract defines the overall service and the Operation Contract defines the various methods that are available on the service. The following snippet shows a simple WCF service with a simple method: