**Service compatibility that is based upon policy** — The final principle enables services to define policies (decided at runtime) that are required to consume the service. These policies are usually expressed through WS-Policy. A policy provides consumers with an understanding of what is actually required to consume a service.

If your own organization is considering establishing an SOA, the WCF is a framework that works on these principles and makes it relatively simple to implement. The next section looks at what the WCF offers. Then you can dive into building your first WCF service.

As stated, the Windows Communication Foundation is a means to build distributed applications in a Microsoft environment. Though the distributed application is built upon that environment, this does not mean that the consumers are required to be Microsoft clients; nor is any Microsoft component or technology necessary to accomplish the task of consumption. Conversely, building WCF services means you are also building services that abide by the principles set forth in the aforementioned SOA discussion, and that these services are vendor-agnostic — that is, they can be consumed by almost anyone.

WCF is part of the .NET Framework and is available to applications targeting .NET 3.0 or later.

# Capabilities of WCF

WCF provides you with the capability to build all kinds of distributed applications. You can build Web services just as you could previously in earlier .NET Framework releases. This means that your services will support SOAP, and therefore will be compatible with older .NET technologies, older Microsoft technologies, and even non-Microsoft technologies (such as any Java-based consumers).

WCF is not limited to pure SOAP over a wire; you can also work with an InfoSet, and create a binary representation of your SOAP message that can then be sent along your choice of protocol. This is for folks who are concerned about the performance of their services and have traditionally turned to .NET Remoting for this binary-based distribution system.

The WCF framework can also work with a message through its life cycle, meaning that WCF can deal with transactions. Along with distributed transactions, WCF can deal with the queuing of messages, and it allows for the intermittent connected nature that an application or process might experience across the web. Of course, what WCF truly provides is a framework to communicate with tools that support many of these capabilities. It’s not that WCF provides a message store and forward capability so much as it supports the protocols used in message store and forward.

When you need to get messages from one point to another, the WCF is the big gun in your arsenal to get the job accomplished. For instance, many developers might consider using WCF primarily to communicate ASP.NET Web Service-like messages (SOAP) from one disparate system to another, but you can use WCF for much more than this. For instance, WCF can be used to communicate messages to components contained on the same machine on which the WCF service is running.

This means you can use WCF to communicate with components contained in different processes on the same machine. For example the same service might be called by a WPF application using a binary format within your organization, while the same service may expose an endpoint hosted on a web server and accessible over the Web via HTTP and SOAP. You use WCF to communicate with components on the same machine or on another machine — even accepting calls from a client that is not a Microsoft-based machine.

# Contracts and Metadata

Probably the biggest and most exciting part of the WCF model is that it enables you to develop a service once and then expose that service via multiple endpoints (even endpoints on entirely different protocols) via simple configuration changes. These changes start with the interface definition. As part of creating a service you’ll be able to define an Interface and that interface has two top level contracts.

From an implementation standpoint a contract is an attribute that is associated with either an interface or a class definition. The `<Service Contract>` is used as part of an interface definition. That interface will expose a series of `<OperationContract>` method definitions, which describe what services this service provides.