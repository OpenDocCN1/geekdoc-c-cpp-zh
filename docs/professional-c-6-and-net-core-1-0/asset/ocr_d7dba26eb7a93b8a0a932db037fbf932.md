![](bbox=[0.1, 0.06, 0.9, 0.44])

# Figure 44.1

The client invokes a method on the proxy. The proxy offers methods as defined by the service but converts the method call to a message and transfers the message to the channel. The channel has a client-side part and a server-side part that communicate across a networking protocol. From the channel, the message is passed to the dispatcher, which converts the message to a method call invoked with the service.

WCF supports several communication protocols. For platform-independent communication, web services standards are supported. For communication between .NET applications, faster communication protocols with less overhead can be used.

Chapter 42 describes communication across HTTP using REST programming style passing objects in a JavaScript Object Notation (JSON) format, and a description of the service API with Swagger. With WCF, some other technologies are important: SOAP, a platform-independent protocol that is the foundation of several web service specifications to support security, transactions, and reliability, and the Web Services Description Language (WSDL) that offers metadata to describe the service.

# SOAP

For platform-independent communication, you can use the SOAP protocol; it is directly supported from WCF. SOAP originally was shorthand for Simple Object Access Protocol, but since SOAP 1.2 this is no longer the case. SOAP no longer is an object access protocol because