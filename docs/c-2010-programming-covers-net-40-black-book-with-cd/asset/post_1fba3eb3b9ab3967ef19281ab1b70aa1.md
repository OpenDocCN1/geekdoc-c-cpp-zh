
- Scalability – Reduces the traffic on the database and saves the resources resulting in more efficiency of the database in meeting the demands of the user. ADO.NET helps in scalability while working with datasets. All database operations are performed on the dataset instead of on the database.

- Transfer of Data in XML Format – Transfers data from a database into a dataset and from the dataset to another component using XML. XML is the standard format used for transferring data in ADO.NET. You can also use an XML file as a data source and store the data from it into a dataset.

- Interaction with the Database through Data Commands – Specifies that database operations are performed by executing the data commands. All operations on database, such as retrieving, modifying, or updating of data are performed using data commands. A data command is either a Structured Query Language (SQL) statement or a stored procedure.

## WF

WF is a technology introduced by Microsoft, which provides a programming model for building workflow-based applications on Windows. It includes activities, workflow runtime, workflow designer, and a rules engine. WF introduced in Framework 3.0 and we see lots of improvement in the Framework 3.5 and 4.0 version. The most important feature of WF is that it provides separation between the business process code and the actual implementation code. WF consists of the following parts:

- Activities – Receive some parameters from the developer, execute its actions, and then the flow is transferred to the next activity. Activities are easily created by writing code or by creating them from other activities, for example the Code or IfElse activities.

- Workflow Designer – Designs workflows by placing activities within the workflow model. One interesting feature of the Workflow designer is that it can be re-hosted within any Windows Forms application.

- Workflow Runtime – Executes the activities in a workflow. It is a light-weight and extensible engine that resides within .NET process, facilitating the developers to bring workflow to anything from a Windows Forms application to an ASP.NET website or a Windows Service.

- Rules Engine – Enables declarative, rule-based development for workflows and for any .NET application to be used.

WF follows a layered architecture within any application in which it is integrated.

Figure 1.5 shows the WF architecture:

![](img/e073a4882197be4ab61103cbe0bcb394_52_0.png)

Figure 1.5: Displaying the WF Architecture

In Figure 1.5, you can see that the top layer is the Model layer where the developers build their code to run in the workflow. This layer provides the developer to add built-in activities, create custom activities, and enable the engine to build rules. It also connects the activities together. The second layer in the architecture is the Runtime layer, which ensures the timely execution of processes, such as tracking, scheduling, and managing state lifecycle and activation.

## Chapter 1

The last layer in the architecture is the Hosting layer, which connects the engine and the executing process. It also provides a set of services, such as persistence, timer, tracking, communication, transactions, and threading required for managing and controlling the workflow. WF also contains built-in services that provide the interfaces required to work with .NET Framework 2.0 and its advanced versions.

## WPF

Microsoft’s WPF (formerly codenamed as Avalon) provides the base for building applications and a clear separation between the user interface and the business logic. WPF helps in building interfaces that include documents, media, two and three-dimensional graphics, animations, and Web-like characteristics. It helps in creating Windows client applications with visually stunning user experiences. You can use WPF for creating both standalone and browser-hosted applications. Some examples of WPF applications are the Yahoo Messenger, the New York Times Reader, and the Contoso Healthcare Sample Application. WPF introduces eXtensible Application Markup Language (XAML), which is a language based on XML, to design interfaces of WPF based applications. Even Microsoft comes with Expression studio that uses XAML for developing user interface for any Web- or Windows-based application.

Figure 1.6 shows the architecture of WPF:

![](img/e073a4882197be4ab61103cbe0bcb394_53_0.png)

As shown in Figure 1.6, WPF provides document services, such as XML Paper Specification (XPS) documents and visual appearance of a page. The WPF namespace, System.IO.Packaging, helps in organizing data, content, and resources of your application into a single, portable, easy to access, and distributable .zip document. WPF aims at unifying several user interface services, such as application services, controls, layout, data-binding, and deployment services. It provides shape primitives for 2-D graphics with in-built brushes, pens, and geometries. WPF supports most video formats, such as Windows Media Video (WMV), Moving Picture Experts Group (MPEG), and some Audio Video Interleave (AVI) files. It also supports some common image formats, and animations.

## WCF

WCF (formerly codenamed as Indigo) is one of the new technologies introduced by Microsoft in .NET Framework 3.0 for building and running connected systems. WCF is a service-oriented technology for developing applications. The service-oriented design results in a distributed system that runs between the services and clients. If you are familiar with concepts, such as Web services, remoting, distributed transactions, and message queuing, then understanding WCF becomes easier since it is an enhanced technology for providing the same functions with better features with minimum time taken to develop the distributed system.

WCF-based applications are interoperable with any process as these communicate through Simple Object Access Protocol (SOAP) messages. When a WCF process connects with a non-WCF process, it uses XML-based encoding for SOAP messages, but when it connects with another WCF process, the SOAP messages are encoded into a binary format. WCF makes use of pluggable encoding system, which allows programmers to write their own encoders. With .NET Framework 3.5, JavaScript Object Notation (JSON) was released that supports the serialization format to WCF. JSON helps WCF service endpoints to process service requests from AJAX-powered Web pages.

The enhancements of WCF as compared to the previous technologies are as follows:

- Merges technologies, such as Web services, remoting, distributed transactions, and message queuing in one place and reduces development time
- Consists of many powerful enterprise features
- Integrates easily with other technologies to increase interoperability

Figure 1.7 shows the WCF architecture:

![](img/e073a4882197be4ab61103cbe0bcb394_54_0.png)

Figure 1.7: Displaying the WCF Architecture

The WCF architecture is composed of the following five layers:

- Application — Refers to the first layer of the WCF architecture that represents the location of the application.
- Contracts — Consists of service, data, and message contracts as well as bindings and policies. The Contracts layer gives you information about the different features of the message system. The Message system involves sending and receiving the messages from one end to another.
- Service Runtime — Provides information about different behaviors that take place at runtime. This layer loads all the services.
- Messaging — Provides information about different channels, which are required at the time of processing a message. This layer deals with the message content that needs to be communicated.
- Activation and Hosting Services — Refers to the last layer of the WCF architecture. In this layer, any service can be hosted using the IIS or Windows Activation Service. Services can also be manually deployed in an executable form.
