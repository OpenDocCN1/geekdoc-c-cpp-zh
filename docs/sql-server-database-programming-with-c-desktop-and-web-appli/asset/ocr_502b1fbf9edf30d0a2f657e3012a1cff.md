# SQL Server Database Programming with C#

The function of each component is listed below:

XML is a text-based storage language which uses a series of tags to define and store data. The so-called tags are used to mark up data to be exchanged between applications. The marked data can then be recognized and used by different applications without any problem. As you know, the Web services platform is XML + HTTP (Hypertext Transfer Protocol) and the HTTP protocol is the most popular Internet protocol. The XML provides a kind of language that can be used between different platforms and programming languages to express complex messages and functions. In order to make the codes used in the Web services to be recognized by applications developed in different platforms and programming languages, the XML is used for coding in the Web services to make up them by line.

SOAP is a communication protocol used for communications between applications. Essentially, SOAP is a simple XML-based protocol to help applications developed in different platforms and exchange information over HTTP. SOAP is a platform-independent and language-independent protocol, which means that it can run at any operating systems with any programming languages. In essence, SOAP works as a carrier to transfer data or requests between applications. Whenever a request is made to the Web server to receive a request, this request is first wrapped in a SOAP message and sent over the Internet to the Web server. Similarly, the Web service returns the target information to the client, the returned information is also wrapped in a SOAP message and sent over the Internet to the client browser.

WSDL is an XML-based language for describing Web services and how to access them. In WSDL terminology, each Web service is defined as an endpoint or a Port and each method is defined as an abstract operation. Each operation or method can contain some SOAP messages to be transferred between applications. Each message is constructed using the SOAP protocol as a represent method from the client. WSDL defines two styles for how a Web service can be formatted in a SOAP message: Remote Procedure Call (RPC) and Document-style messages can be used to communicate with a Web Service using a WSDL.

A single endpoint can contain a group of Web methods and that group of methods can be defined as an abstract set of operations called a Port Type. Therefore, WSDL is an XML format for describing web services as a set of endpoints on SOAP messages containing either document-oriented or procedure-oriented information. The operations and messages are described abstractly, and bound to a concrete network protocol and message format to define the endpoint.

UDDI is an XML-based directory for businesses to list themselves on the Internet and the goal of this is to enable companies to find one another on the Web and make their systems interoperable for e-commerce. UDDI is often considered as a telephone book's yellow and white pages. By using those pages, it allows businesses to list them by name, products, locations, or the Web services they offer.

Summary, based on these components and their roles discussed above, we can conclude:

+   - XML is used to tag the data to be transferred between applications.
- SOAP is used to wrap and pack the data in the XML format into the messages represented by the SOAP protocol.
- WSDL is used to map a concrete network protocol and message format to an abstract endpoint, and describe the Web services available in a WSDL document format.
- UDDI is used to list all Web services that are available to users and businesses.