
As shown in Figure 1.9, DLR adds the following sets of services to CLR for supporting the dynamic languages:

- Expression trees – Allows you to define variable assignments and function loops
- Call site caching – Allows DLR to cache information about method calls so that in case of any subsequent calls to the method, the DLR can use the cache history information
- Dynamic object interoperability – Refers to the set of classes that can be used to create dynamic objects

The binder helps DLR to communicate with not only the .NET Framework but also with other infrastructure and services, such as Silverlight and Office. The binder informs the DLR about the language and how to perform operations in a call site by using expression trees.

## Managed Extensibility Framework

The Managed Extensibility Framework (MEF) is a new library included in the .NET Framework 4.0 version to create lightweight and extensible applications. MEF also helps in reusing the extensions not only within but across the applications also. The System.ComponentModel.Composition namespace is included in .NET Framework 4.0, which provides classes that constitute the core of MEF.

Earlier, while creating an application that needed a plug-in model, you need to create the infrastructure of the application. In this method, the plug-ins created were application-specific and cannot be reused across multiple applications. The MEF library, however, provides extensions that can be reused in multiple applications. With the help of MEF, the application can not only locate the extension but also load it in the application.

## Parallel Computing

Parallel computing is a process in which a large problem is divided into small units and then these units are solved parallelly. Sometimes personal computers and workstations have two or three Central Processing Units (CPUs) that enable multiple threads to be executed simultaneously. In such a situation, a new programming model is provided by .NET Framework 4.0 that allows the developers to develop multithreaded and asynchronous code. This new programming model is known as parallel computing, which is supported by new runtime, class library types, and diagnostic tools. In parallel computing, you need to distribute the code for execution across multiple processors. Note that to implement parallel computing, you need to import the System.Threading.Tasks namespace, which is introduced with the .NET Framework 4.0 version.

## In-Process Side-by-Side Execution

The In-Process Side-by-Side Execution feature supports the loading and starting of multiple versions of .NET Framework by an application within the same process. For example, you can execute an application, which loads the components developed in .NET Framework 3.0 and .NET Framework 4.0 in the same process.

## Improved Security Model

A new and improved security model is introduced with .NET Framework 4.0. Many useful classes and services introduced in CLR and .NET Framework help the developers to write secure code and implement cryptography and role-based security. The following are the two major changes introduced in .NET Framework 4.0 security system:

- There is no machine-wide security policy, although the user permissions system remains the same.
- The default enforcement mechanism is changed to security transparency.

## Networking Improvements

The following are the various networking improvements implemented in .NET Framework 4.0:

- Improvements in classes for Windows authentication, such as System.Net.HttpWebRequest, System.Net.HttpListener, System.Net.Mail.SmtpClient, and System.Net.Security.NegotiateStream
- Improvements in support for Network Address Translation (NAT) traversal using IPv6 and Teredo
- Introduction of new networking performance counters that provide information about HttpWebRequest objects
- Introduction of AddRange method in the System.Net.HttpWebRequest class
- Implementation of Secure Socket Layer (SSL) support for System.Net.Mail.SmtpClient class
- Improvement in support for mail headers in the System.Net.Mail.MailMessage class

## Improved Core ASP.NET Services

Along with the .NET Framework, the following features are introduced in ASP.NET to improve the core ASP.NET services:

- Introduction of the properties to set meta tags by using the Page.MetaKeywords and Page.MetaDescription page properties
- Improvements in working with browser capabilities by making it easier
- Introduction of ASP.NET routing with Web forms
- Introduction of the new ASP.NET Chart control
- Introduction of the new QueryExtender control, which provides filtering support for data source controls
- Implementation of more control over HTML code in the FormView and ListView controls

## Improvements in WPF

In .NET Framework 4.0, the following changes have been introduced in many areas of WPF, which includes controls, graphics, and XAML:

- Introduction of new controls, such as DataGrid, Calendar, and DatePicker
- Introduction of VisualStateManager class and supporting classes to define the appearance of a control according to its visual state
- Introduction of UIElement, UIElement3D, and ContentElement classes to expose the events that occur on a touch-enabled screen, when a user touches an element
- Introduction of changes related to text, such as new text rendering stack, the SelectBrush property to highlight a selected text, and the CaretBrush property to change the brush that paints the cursor
- Introduction of changes and improvements related to binding

## Improved Entity Framework

In .NET Framework 4.0, you need to do less amount of coding in Entity Framework. The new features introduced in Entity Framework are as follows:

- Creation of conceptual models in which the columns with foreign keys in the database correspond to entity types
- Introduction of new methods in the System.Data.Objects namespace so that the N-tier applications are developed easily
- Introduction of the EntityDataSource control support for the QueryExtender control
- Creating, reading, updating, and deleting operation on entity objects as the ObjectContext class now returns typed ObjectSet<TEntity> objects
- Executing store commands from the ObjectContext class directly
- Introduction of deferred loading (lazy loading), with the help of which the related objects are automatically loaded from a data source, when the navigation property is accessed

## Integration of WCF and WF

.NET Framework 4.0 has introduced new features and improvements in WCF, which includes simplifying the user experience by providing integration of WCF and WF. The integration between WCF and WF provides a rich and declarative programming model to help the developers build a variety of applications. This integration is very helpful, as WF provides you with a framework for implementing long-running applications.

Figure 1.10 displays the integration of WCF and WF in .NET Framework 4.0.

![](img/e073a4882197be4ab61103cbe0bcb394_60_0.png)

## Figure 1.10: Displaying the WCF and WF Integration

The advantage of integrating WCF and WF is that you can use the best of both in a single application. You not only get a declarative programming model by using WF services but also a rich communication flexibility provided by WCF.

Let’s move on to explore the Microsoft Visual Studio 2010 IDE. It provides a single environment for developing all types of .NET applications and provides many options and rich features to create interactive Web applications by using ASP.NET 4.0.

## Section II – Introduction to Visual Studio 2010 IDE

Microsoft Visual Studio is an Integrated Development Environment (IDE) provided by Microsoft to create and develop Windows-based, Web-based, Console-based, and Mobile-based applications for .NET Framework. These applications can be created by using different languages, such as Visual Basic, Visual C#, and Visual C++. Earlier, these applications were created using a Notepad and then compiled to convert the programming language into machine language. Now, you might be wondering if a Notepad can create all these applications, why do we need Visual Studio as an editor? The answer is that Microsoft Visual Studio provides various benefits to design and create the applications, as compared to a Notepad. For example, you need to memorize all the language syntax in case you are using a Notepad. However, in case of Visual Studio, you do not need to remember the syntax. You just need to type the first few letters of a command and Visual Studio would prompt you with the available options for the command.

The following are some of the benefits of using Visual Studio 2010:

- Helps in minimizing the development time
- Simplifies the process of testing applications
- Provides different toolsets for integrating graphic designers into the overall development process
- Supports multiple versions of the .NET Framework
- Enhancements in data retrieval and data binding
- Inspects code to find sections of code that need to be refactored
- Provides support for Web, mobile, client, Vista, and Office application development
- Integrates with the .NET Framework 4.0
- Simplifies the process of designing the applications

Now, let’s explore Visual Studio 2010 and its new features.

## New Features of Visual Studio 2010

As compared to Visual Studio 2008, Visual Studio 2010 provides an IDE for writing, compiling, and debugging the code of an application. The Visual Studio 2010 IDE contains a complete set of development tools for building Windows applications, websites, Web services, and mobile applications.

The new features and enhancements made in Visual Studio 2010 IDE are listed as follows:

- Enhanced docking
