+   - Multi-user communication applications that allow users to communicate and exchange data directly rather than through a server
+   - Distributed processing applications, as an alternative to supercomputing applications that process enormous amounts of data
+   - Web 2.0 applications that combine some or all the above in dynamic, next-generation web applications

# MICROSOFT WINDOWS PEER-TO-PEER NETWORKING

The Microsoft Windows Peer-to-Peer Networking platform is Microsoft's implementation of P2P technology. It is part of Windows XP SP2, Windows Vista, and Windows 7, and is also available as an add-on for Windows XP SP1. It includes two technologies that you can use when creating .NET P2P applications:

+   - The Peer Name Resolution Protocol (PNRP), which is used to publish and resolve peer addresses
+   - The People Near Me server, which is used to locate local peers (currently for Vista and Windows 7 only)

In this section you learn about these technologies.

# Peer Name Resolution Protocol (PNRP)

You can of course use any protocol at your disposal to implement a P2P application, but if you are working in a Microsoft Windows environment (and, let's face it, if you're reading this book you probably are) it makes sense to at least consider PNRP. There have been two versions of PNRP released to date. PNRP version 1 was included in Windows XP SP2, Windows XP Professional x64 Edition, and Windows XP SP1 with the Advanced Networking Pack for Windows XP. PNRP version 2 was released with Windows Vista, and was made available to Windows XP SP2 users through a separate download (see KB920342 at support.microsoft.com/kb/920342). Windows 7 also uses version 2. Version 1 and version 2 of PNRP are not compatible, and this chapter covers only version 2.

In itself, PNRP doesn't give you everything you need to create a P2P application. Rather, it is one of the underlying technologies that you use to resolve peer addresses. PNRP enables a client to register an endpoint (known as a peer name) that is automatically circulated among peers in a cloud. This peer name is encapsulated in a PNRP ID. A peer that discovers the PNRP ID is able to use PNRP to resolve it to the actual peer name, and can then communicate directly with the associated client.

For example, you might define a peer name that represents a WCF service endpoint. You could use PNRP to register this peer name in a cloud as a PNRP ID. A peer running a suitable client application that uses a discovery mechanism that can identify peer names for the service you are exposing might then discover this PNRP ID. Once discovered, the peer would use PNRP to locate the endpoint of the WCF service and then use that service.

![](bbox=[0.65, 0.8, 0.92, 0.98])