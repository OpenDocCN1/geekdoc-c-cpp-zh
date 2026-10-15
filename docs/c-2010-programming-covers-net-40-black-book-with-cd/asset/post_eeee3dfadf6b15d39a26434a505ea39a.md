
You can deploy an assembly in the GAC using any one of the following:

- An installer that is designed to work with the GAC
- The GAC tool known as Gacutil.exe
- The Windows Explorer to drag assemblies into the cache

## Strong Name Assemblies

A strong name is a hash token that contains the assembly's identity, i.e. the information about the assembly's name, version number, culture, public key, and digital signature. Using the private key, the assembly file containing the manifest generates the strong name. You can provide a strong name to an assembly using the Microsoft Visual Studio .NET and other development tools. Using strong names for assemblies has the following benefits:

- Provides uniqueness to the names by generating a private key
- Ensures that the version of the assembly you are using comes from the same publisher who has created the version the application was built with
- Facilitates integrity check that ensures that the contents of the assembly do not change since its last build

## Private and Shared Assemblies

An assembly is called as a private assembly, if it is used by only a single application. For example, if you have created a DLL containing information about your business logic, then this DLL can be used by your Client application only. In order to run the application, the DLL must be included in the same folder in which the Client application has been installed. This makes the assembly private to your application.

Shared assemblies are those assemblies that are placed in the GAC so that they can be used by multiple applications. Consider a scenario where the DLL needs to be reused in different applications. In this case, instead of transferring a copy of the DLL at each and every Client application, the DLL can be directly placed in the GAC, by using the Gacutil.exe tool, from where the DLL application can be accessed by any Client application.

## Side-by-Side Execution

The process of executing multiple versions of an application or a component on a computer is known as side-by-side execution. The .NET Framework supports side-by-side execution of multiple versions of CLR, applications, components, compilers, and runtime. It allows multiple versions of an assembly or application to be installed on the same computer at the same time.

Figure 1.4 shows side-by-side execution:

![](img/e073a4882197be4ab61103cbe0bcb394_49_0.png)

Figure 1.4: Displaying Side-By-Side Execution

Now, let’s discuss about the .NET Framework class library.

## .NET Framework Class Library

.NET Framework consists of classes, interfaces, and value types that help in speeding up the development process and provide access to system functionality. .NET Framework provides the interoperability between languages, because the data types are CLS-compliant and can be used from any programming language whose compiler conforms to the CLS.

.NET applications, components, and controls are built on the foundation of .NET Framework types. These entities perform the following functions:

- Representing base data types and exceptions
- Encapsulating data structures
- Performing input/output operations
- Accessing information about loaded types
- Calling .NET Framework security checks
- Facilitating data access, rich client-side Graphical User Interface (GUI), and server-controlled client-side GUI

The Framework Class Library (FCL) is a huge library of reusable types meant to be used by managed codes. It is an object-oriented library that is used in component-based applications. The FCL is made up of a hierarchy of namespaces that expose classes, structures, interfaces, enumerations, and delegates. The namespaces are logically defined by their functionality. For example, the System.Data namespace contains the functionality available for accessing databases. This namespace is further broken down into two namespaces – System.Data.SqlClient and System.Data.OleDb. The System.Data.SqlClient namespace exposes the functionality specific to SQL Server; whereas, the System.Data.OleDb namespace exposes the functionality for accessing Object Linking and Embedding DataBase (OLEDB) data sources.

The following points need to be remembered while using the FCL:

- The classes, interfaces, structures, and enumerated values are collectively referred to as types. The different types in the framework are arranged in a hierarchy of namespaces. This solves the problem faced in name collisions. Namespaces are arranged in a hierarchy that has words separated by periods. You may write a code that uses a Stream class or a Form class; however, in IL, these classes are represented as System.IO.Stream and System.Windows.Forms.Form, respectively.
- The System namespace is the root namespace for fundamental types in .NET Framework. This namespace includes classes that represent the base data types used by all applications, such as Object, Byte, Char, Array, Int32, and String. Many of these types correspond to the primitive data types that the programming languages use.
- All the data types are derived from their base types, and these base types are derived from the System.Object class. For instance, int data type is derived from the System.Int32 class, which in turn is derived from the System.Object class. This is because, the System.Object class the base type for all types in .NET Framework. If you create a class that does not explicitly declare a base class, then the compiler explicitly declares its base class to the Object class.

## Windows Forms

Windows Forms is the graphical representation of any window displayed in an application. It is included as a part of Microsoft’s .NET Framework. You can create Windows Forms applications in any CLR supported language. A Windows Form is used either to accept input from a user or to display information to the user. In Windows Forms, you add controls to the forms and raise events, such as mouse-click, which is handled by event handlers in an application.

## ASP.NET and ASP.NET AJAX

ASP.NET is a Web development model, which is used to deliver interactive, data-driven Web applications over the Internet. It also consists of a large number of controls, such as text boxes, buttons, and labels for assembling, configuring, and manipulating code to create Hyper Text Markup Language (HTML) pages. You can create

ASP.NET application using any CLR compliant language, such as Visual Basic and C#. The main features of ASP.NET are as follows:

- **Better Performance**—Provides the cached copy of the output of the code for any subsequent calls to the same Web page. When you request a Web page for the first time, the CLR compiles the code of the Web page and stores the cached copy of the result. Now, for any subsequent calls to the same page, the cached copy of the result is retrieved instead of going back to the server.
- **Improved Security**—Provides the following four methods of authentication:
  - **Forms authentication**—Redirects unauthenticated requests to an HTML form. In forms authentication, a user provides credentials and submits the form. If the request is authenticated by an application, a cookie is issued by the system containing the credentials for reacquiring the identity.
  - **Passport authentication**—Specifies a centralized authentication service that provides a logon and core profile services for member sites.
  - **Windows authentication**—Works in combination with Microsoft Internet Information Services (IIS) authentication. IIS uses one of the ways of authentication from basic, digest, or Integrated Windows Authentication.
- **Greater Scalability**—Enables cross-server sessions between multiple Web servers. This is because, the session states in ASP.NET are maintained in a separate process on a different machine or database.
- **Cookie-less Sessions**—Stores the session state even when the cookies in a Web browser are disabled.

Asynchronous JavaScript and XML (AJAX), formerly code-named as Atlas, is an extension of ASP.NET for developing and implementing AJAX functionality. ASP.NET AJAX enables both client-side and server-side components that allow the developers to create Web applications that are capable to update the data on a website without a complete reload of the page. The following are the advantages of using AJAX:

- **Asynchronous**—Enables asynchronous calls to the Web server without making the users wait for the data.
- **Minimal transfer of data**—Helps in sending only a part of the modified data to the Web server, minimizing the network traffic, and performing the operations quicker. This feature is useful in sites where restricted pipes are allowed for data transfer resulting in improved network performance.
- **Minimal processing on the Web server**—Minimizes the processing on the Web server as only the necessary data needs to be sent.
- **Context**—Reduces burden on the server by sending a request back to the server through the client-side script. AJAX-based applications implement partial page postbacks instead of full page postbacks, which reduce the data traffic between the client and server.

## ADO.NET

ADO.NET is a technology used for working with data and databases. You can use ADO.NET to connect to data sources for retrieving, manipulating, and updating data.

Some features of the ADO.NET technology are as follows:

- **Disconnected Data Architecture**—Implies that applications connect to the database only when data needs to be retrieved or modified. After the database operation has been performed, the connection to the database is closed. To perform any database operation again, the connection with the database needs to be re-established. Applications that do not follow the disconnected data architecture waste a lot of valuable system resources and time because these applications need to maintain a connection with the database even when it is not required.
- **Cached Data in Datasets**—Follows a disconnected architecture for accessing or modifying data. Therefore, the cached data in datasets is not required for the applications to connect to the database for processing each record. Therefore, the data is accessed and later stored in the datasets. A dataset is a cached set of database records, i.e. a dataset is not dependent on the data source. Even when you are disconnected from the database on which you are working, you can still make modifications in it.
