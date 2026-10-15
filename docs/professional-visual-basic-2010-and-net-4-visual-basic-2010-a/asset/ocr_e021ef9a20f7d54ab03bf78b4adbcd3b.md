Web services are remarkably easy to deploy. The power of Web services comes from the use of the WSDL contract. In addition, Web services are inherently cross-platform, even when created with Microsoft products. The standard XML schemas are part of the WSDL specification.

The key is that even though this protocol may not be as efficient or fast as some of the binary protocols of the past, its implementation-agnostic contracts make it more useful. Given that you can create a communication protocol that is either available for use by 50% of users and which runs superfast versus one that is available to 100% of users and runs fast, the tendency will be to adopt the solution with greater reach. Thus, Web services became the interoperability baseline for service communication.

For this reason, they best represent where the Internet is heading — toward an architecturally neutral collection of devices, rather than millions of PCs surfing the World Wide Web. Encapsulating code so that you can simply and easily enable cell phones to use your logic is a major boon to developers, even if they do not realize it yet.

# How This All Fits Together

Microsoft’s support for Web services really took off with the introduction of .NET. However, support was available to have Web services run on older operating systems like Windows NT4 SP6, with the SOAP Toolkit installed.

The .NET Framework encapsulated the Web service protocol into objects. This was great initially, but as noted earlier, over time it was generally agreed that not every communication needed to be put up as a HTTP/HTTPS-based service. WCF was the result of Microsoft taking a look at the common concepts from all of the preceding communication technologies and seeking a unified solution.

While Web services remain one of the most common underlying implementations for WCF services, the reality is that they are now a subset of what you can do with WCF. Things like the WS-* protocols become configuration settings; similarly, you can have a single interface that supports multiple different communication protocols. Thus, the same service that is used with a client that supports a binary transfer protocol like Remoting can communicate via HTTP protocol for a client that doesn’t support those binary protocols.

WCF is now an integrated part of the service-oriented architecture strategy. Historically, the starting place on MSDN for Web Services was http://msdn.microsoft.com/webservices, but that link now takes you directly to http://msdn.microsoft.com/wcf. It’s not that Web services have gone away or become less important, it’s simply that Web services are a subset of the complete WCF communication framework.

The goal of WCF is to provide a loosely coupled, ubiquitous, universal information exchange format. Toward that end, SOAP is not the only mechanism for communicating with WCF services.

# What Makes a WCF Service

A WCF service consists of three parts: the service, one or more endpoints, and an environment in which to host the service.

A service is a class that is written in (or in the case of Interop, wrapped by) one of the .NET-compliant languages. The class can contain one or more methods that are exposed through the WCF service. A service can have one or more endpoints, which are used to communicate through the service to the client.

Endpoints themselves are also made up of three parts. These parts are usually defined by Microsoft as the “ABC” of WCF. Each letter of WCF means something in particular in the WCF model. Similarly,

+   - “A” is for address
+   - “B” is for binding
+   - “C” is for contract