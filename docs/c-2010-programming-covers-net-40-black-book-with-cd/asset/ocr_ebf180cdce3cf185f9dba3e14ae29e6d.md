services and clients. If you are familiar with concepts, such as Web services, remoting, distributed transactions, and message queuing, then understanding WCF becomes easier since it is an enhanced technology for providing the same functions with better features with minimum time taken to develop the distributed system.

WCF-based applications are interoperable with any process as these communicate through Simple Object Access Protocol (SOAP) messages. When a WCF process connects with a non-WCF process, it uses XML-based encoding for SOAP messages, but when it connects with another WCF process, the SOAP messages are encoded into a binary format. WCF makes use of pluggable encoding system, which allows programmers to write their own encoders. With .NET Framework 3.5, JavaScript Object Notation (JSON) was released that supports the serialization format to WCF. JSON helps WCF service endpoints to process service requests from AJAX-powered Web pages.

The enhancements of WCF as compared to the previous technologies are as follows:

+   - Merges technologies, such as Web services, remoting, distributed transactions, and message queuing in one place and reduces development time
+   - Consists of many powerful enterprise features
+   - Integrates easily with other technologies to increase interoperability

Figure 1.7 shows the WCF architecture:

![](bbox=[0.2, 0.45, 0.8, 0.73])

Figure 1.7: Displaying the WCF Architecture

The WCF architecture is composed of the following five layers:

+   - Application — Refers to the first layer of the WCF architecture that represents the location of the application.
+   - Contracts — Consists of service, data, and message contracts as well as bindings and policies. The Contracts layer gives you information about the different features of the message system. The Message system involves sending and receiving the messages from one end to another.
+   - Service Runtime — Provides information about different behaviors that take place at runtime. This layer loads all the services.
+   - Messaging — Provides information about different channels, which are required at the time of processing a message. This layer deals with the message content that needs to be communicated.
+   - Activation and Hosting Services — Refers to the last layer of the WCF architecture. In this layer, any service can be hosted using the IIS or Windows Activation Service. Services can also be manually deployed in an executable form.