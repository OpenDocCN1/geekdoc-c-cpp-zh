
# ASP.NET Web Services 513

![](img/d59a47501d0a20fc0460a49c469c6fb7_541_0.png)

FIGURE 9.1 A typical process of a web service.

Figure 9.1 shows a diagram to illustrate these components and their roles in an ASP.NET Web service process.

By now, we have obtained the fundamental knowledge about the ASP.NET Web services and their components, now let's see how to build a Web service.

## 9.2 PROCEDURES TO BUILD A WEB SERVICE

Different methods and languages can be used to develop different Web services such as the C# Web, Java services and Perl Web services. In this section we only concentrate on developing the ASP.NET Web services using the Visual C#.NET. Before we can start to build a real Web service project, let's take a closer look at the structure of a Web service project.

### 9.2.1 The Structure of a Typical Web Service Project

A typical Web service project contains the following components:

- 1 A new Web service project is created, two pages and one folder are created under this new project. The folder App_Data is used to store all project data.
- 2 The code-behind page .svc.IService1.cs. This page contains the real C#.NET codes for a simple Web service. Visual Developer includes two declarations to help users to develop Web services on the top of this page, which are:
    * using System.Runtime.Serialization;
    * using System.ServiceModel;
- 3 Another file is named Service1.svc. As we know, WCF hosted in IIS are represented as special content files or .svc files inside the IIS application. This method is similar to the way in which ASMX pages are represented inside of an application as .asmx files. A .svc file contains the WCF-specific processing directive that allows the WCF hosting infrastructure to activate hosted services in response to incoming messages.
- 4 The configuration file Web.config, which is an XML-based file, is used to set up a configuration for the new created Web service project, as the namespaces for all kinds of Web components, Connection string and default authentication mode. Each Web service project has its own configuration file.

Of all files and folders discussed above, the code-behind page is the most important file since Visual C#.NET codes related to building a Web service are located in this page and our major coding development will be concentrated on this page.

### 9.2.2 THE REAL CONSIDERATIONS WHEN BUILDING A WEB SERVICE PROJECT

Based on the structure of a typical Web service project, some issues related to the building of an actual Web service project are emphasized here, and these issues are very important should be followed carefully to successfully create a Web service in the Visual Studio.NET environment.

As a request is made and sent from Windows or Web form control over the Internet to the server, the request is packed into a SOAP message and sent to the Information Services (IIS) on the client computer, which works as a pseudo server. The IIS will pass the request to the ASP.NET to get processed in terms of the extension asmx of the main service page. ASP.NET checks the page to make sure that the code-behind page contains the necessary codes to perform the Web Service, exactly to trigger the Web methods to search, find, and retrieve the information required by the client, pack it to the SOAP message and return it to the client.

During this process, the following detailed procedures must be performed:

- 1) When ASP.NET checks the received request represented in SOAP message, the ASP.NET will make sure that the names and identifiers used in the SOAP message be unique, in other words, those names and identifiers cannot conflict with any name and identifiers used by any other message. To make names and identifiers unique, we need to use our specific namespace to parse and hold our SOAP message.
- 2) In general, a request contains a set of information, to retrieve those pieces of information, we need to create a Web service proxy class to consume Web services. In other words, we do not want to develop a separate Web method to query each piece of information, and that will make our project's size too large if we need a lot of information. A good solution is to implement an object based on that class and integrate those pieces of information into that object. All information can be embedded into that object and can be returned if that. Another choice is to design a Web method to return it a DataSet. This is a convenient way to return all data.
- 3) As a professional approach, we need to handle the exceptions to make our Web service as perfect as possible. In that case, we need to create a base class to handle some error checking to protect our real class that will be instantiated to an object that contains all the information we need, so this real class should be a child class inherited from the base class.
- 4) Since the Web services did not provide any GUI, we need to develop some GUIs in either Windows-based or Web-based applications to interface to the Web services to display returned information on GUIs.

Starting from .NET Framework 4.0, a good platform, Windows Communication Foundation (WCF), is provided to support build Web Services projects. First let's have a basic understanding this new tool.

## 9.2.3 INTRODUCTION TO THE WINDOWS COMMUNICATION FOUNDATION (WCF)

As the advanced development of the service-oriented communications, the software development has been significantly changed. When the message is done with SOAP or in some other way, applications that interact through services have become the norm. For Windows developers, this change is made possible by using the Windows Communication Foundation (WCF). First released as part of the .NET Framework 3.0 in 2006, updated in the .NET Framework 3.5, and the most recent version of the technology is included in the .NET Framework 4.8. For a substantial share of new software built on .NET, WCF is the foundation.

### 9.2.3.1 What is the WCF?

The Windows Communication Foundation (WCF) is a framework for building service-oriented applications. Using WCF, you can send data as asynchronous messages from one service endpoint to another. A service endpoint can be part of a continuously available service hosted by IIS, or be hosted in an application. An endpoint can be a client of a service that requests data from a service endpoint.

WCF is a unified framework for creating secure, reliable, transacted, and interoperable applications. In earlier versions of Visual Studio, several technologies could be used for communicating between applications.

If you wanted to share information in a way that it could be accessed from any platform, you would use a Web service (also known as ASMX Web service). If you wanted to move data between a client and server that are running on the Windows operating system, you would use .NET Remoting. If you wanted transferred communications, you would use Enterprise Services (DCOM), and if you wanted to create a model you would use Message Queuing (MSMQ).

WCF brings together the functionality of all those technologies under a unified model. This simplifies the development of distributed applications. In fact, WCF is implemented as a set of classes on the top of .NET Framework's Common Language Runtime (CLR). This allows .NET developers to build service-oriented applications easily. In addition, WCF allows the creation of clients that access services in a mutual way, which means that the client and the service can run in the same way. WCF doesn't define a required host. When they run, clients and services can interact via SOAP, or a WCF-specific binary protocol, and in others.

### 9.2.3.2 WCF Data Services

WCF Data Services, formerly known as ADO.NET Data Services, is a component of the .NET Framework that enables you to create services using the Open Data Protocol (OData) to consume data from the Web or internet using the semantics of relational state. OData exposes resources that are addressable by URIs. Data is accessed and changed by using standard HTTP verbs GET, PUT, POST, and DELETE. OData uses the entity-relationship conventions of the Entity Data Model to expose resources as sets of entities that are related by associations.

Data originates from various sources using OData feeds. Visual Studio makes it easier for you to create an OData-based service using an ADO.NET Framework data model. You can also create OData feeds based on common language runtime (CLR) classes and either late-bound or un-typed data.

WCF Data Services also includes a set of client libraries, for general .NET Framework applications and another specifically for Silverlight-based applications.

### 9.2.3.3 WCF Services

A WCF service is based on an interface that defines the contract between the service and the client. It is marked with a OperationContract attribute, as piece of code shown in Figure 9.2.
