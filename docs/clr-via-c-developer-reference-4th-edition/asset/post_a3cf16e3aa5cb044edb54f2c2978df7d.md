
> Note It is possible to run NGen.exe in update mode. This tells the tool to run NGen.exe on all of the assemblies that had previously been NGen'd. Whenever an end user installs a new service pack of the .NET Framework, the service pack's installation program will run NGen.exe in update mode automatically so that NGen'd files are kept in sync with the version of the CLR installed.

- **Inferior execution-time performance** When compiling to code, NGen can't make any assumptions about the execution environment as the JIT compiler can. This causes NGen to produce inferior code. For example, NGen won't optimize the use of certain CPU instructions; it adds indirections for static field access because the actual address of the static fields isn't known until runtime. NGen inserts code to call class constructors everywhere because it doesn't know the order in which the code will execute and if a class constructor has been called. (See Chapter 8, "Methods," for more about class constructors.) Some NGen'd applications actually perform about 5 percent slower when compared to their JIT-compiled counterpart. So, if you're considering NGen.exe to improve the performance of your application, you should compare NGen'd and non-NGen'd versions to be sure that the NGen'd version doesn't actually slow! For some applications, the reduction in working set improves performance, so using NGen can be a net win.

Due to all of the issues listed, you should be very when considering the use of NGen.exe. Server-side applications, NGen.exe makes little or no sense because only the first client request experiences a performance hit; future client requests run at high speed. In addition, for most server applications, only one instance of the code is required, so there is no working set benefit.

For client applications, NGen.exe might make sense to improve startup time or to reduce working set if an assembly is used by multiple applications simultaneously. Even in case that an assembly is used by multiple applications, NGen'ing an assembly could improve working set. Moreover, if NGen.exe is used for all of a client application's assemblies, the CLR will not need to load the JIT compiler at all, reducing working set even further. For, if just one assembly isn't NGen'd or if an assembly's NGen'd file can't be used, the JIT compiler will load, and the application's working set increases.

For large applications that experience long startup times, Microsoft provides a Managed Guided Optimization tool (MPGO.exe). This tool analyzes the execution of your application to see what it needs at startup. This information is then fed to the NGen.exe tool in order to better optimize the resulting image. This allows your application to start faster and with a reduced working set. When you're ready to ship your application, launch it via the MPGO tool and then exercise your application's common tasks. Information about the parts of the code that is executed written to a profile, which is embedded within your assembly file. The NGen.exe tool uses this profile to better optimize the native image it produces.

# The Framework Class Library

.NET Framework includes the Framework Class Library (FCL). The FCL is a set of DLL assemblies that contain several thousand type definitions in which each exposes some functionality. Microsoft is producing additional libraries such as the Windows Azure SDK and the DirectX SDK. Additional libraries provide even more types, exposing even more functionality for your use. In fact, Microsoft is producing many libraries at a phenomenal rate, making it easier than ever for developers to use various Microsoft technologies.

Here are just of the kinds of applications developers can create using these assemblies:

- **Web services** Methods can process message sent over the Internet very easily using Microsoft's ASP.NET XML Web Service technology or Microsoft's Communication Foundation (WCF)
- **Web Forms/MVC** HTML-based applications (websites) Typically, ASP.NET will make database queries and web service calls, combine and filter the returned information, and then present that information in a browser by using any HTML-based user interface.
- **Rich Windows GUI applications** Instead of a webpage to create your UI, you can use the more powerful, high-performance functionality offered by Windows Store, Windows Presentation Foundation (WPF), or Windows Forms technologies. GUI applications can take advantage of controls, menus, and touch, style, and keyboard events, and they can exchange information directly with the underlying operating system. Rich Windows applications can also make database queries and consume web services.
- **Windows console applications** For very simple UI demands, a console application provides a quick and easy way to build an application. Compilers, utilities, and tools are typically implemented as console applications.
- **Windows services** Yes, it is possible to build service applications that are controllable via the Windows Service Control Manager (SCM) by using the .NET Framework.
- **Database stored procedures** Microsoft's SQL Server, IBM's DB2, and Oracle's database servers allow developers to write their stored procedures using the .NET Framework.
- **Component library** The .NET Framework allows you to stand-alone assemblies (components) containing types that can be easily incorporated into any of the previously mentioned applications.

> Important Visual Studio allows you to create a Portable Class Library project. This project type you to create a single class library assembly that works with various application types, including the .NET Framework proper, Silverlight, Windows Phone, Windows Store apps, and Xbox 360.

The FCL contains thousands of types, a set of related types is presented to the developer within a single namespace. For example, the System namespace (which you should become most familiar contains the Object base type, from which other types ultimately derive. In addition, the System namespace contains types for integers, characters, strings, exception handling, and console I/O as well as a bunch of utility types that convert safely between data types, format data types, generate random numbers, and perform various math functions. All applications will use types from the System namespace.

To access any of the framework's features, you need to know which namespace contains the types that expose the facilities you're after. A lot of types allow you to customize your behavior; you do so by simply deriving your own type from the desired FCL type. The object-oriented nature of the platform is how the .NET Framework presents a consistent programming paradigm to software developers. Also, developers can easily create their own namespaces containing their own. These namespaces and types merge seamlessly into the programming paradigm. Compared to Win32 programming paradigms, this new approach greatly simplifies software development.

Most of the namespaces in the FCL present types that can be used for any kind of application. Table 1-3 lists some of the more general namespaces and briefly describes what the types in that namespace are used for. This is a very small sampling of the namespaces available. Please see the documentation that accompanies the various Microsoft SDKs to gain familiarity with the ever-growing set of namespaces that Microsoft is producing.

| Namespace | Description of Contents |
| :--- | :--- |
| System | All of the basic types used by every application |
| System.Data | Types for communicating with a database and processing data |
| System.IO | Types for doing I/O and walking directories and files |
| System.Net | Types that allow for low-level network communications and working with some common protocols |
| System.Runtime.InteropServices | Types that allowed access to unmanaged operating system facilities such as COM components and functions in Win32 or custom DLLs |
| System.Security | Types used for protecting data and resources |
| System.Text | Types to work with different encodings, such as ASCII and Unicode |
| System.Threading | Types used for asynchronous operations and synchronization access to resources |
| System.Xml | Types used for processing Extensible Markup Language (XML) schemas and data |

This book is about the CLR and the general types that interact closely with the CLR. The content of this book is about all programmers writing applications or components that target the CLR. Many other books exist that cover specific application types such as Web Services, Web Forms/MVC, Windows Presentation Foundation, etc. These other books will give you an excellent start at helping you build your application. I tend to think of these application-specific books as helping you learn from the top down because they concentrate on the application type and not on the development platform. In this book, I'll offer information that will help you learn from the bottom up. After reading this book and an application-specific book, you should be able to easily and efficiently build any kind of application you desire.
