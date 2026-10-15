As shown in Figure 1.9, DLR adds the following sets of services to CLR for supporting the dynamic languages:

+   - Expression trees – Allows you to define variable assignments and function loops
+   - Call site caching – Allows DLR to cache information about method calls so that in case of any subsequent calls to the method, the DLR can use the cache history information
+   - Dynamic object interoperability – Refers to the set of classes that can be used to create dynamic objects

The binder helps DLR to communicate with not only the .NET Framework but also with other infrastructure and services, such as Silverlight and Office. The binder informs the DLR about the language and how to perform operations in a call site by using expression trees.

# Managed Extensibility Framework

The Managed Extensibility Framework (MEF) is a new library included in the .NET Framework 4.0 version to create lightweight and extensible applications. MEF also helps in reusing the extensions not only within but across the applications also. The System.ComponentModel.Composition namespace is included in .NET Framework 4.0, which provides classes that constitute the core of MEF.

Earlier, while creating an application that needed a plug-in model, you need to create the infrastructure of the application. In this method, the plug-ins created were application-specific and cannot be reused across multiple applications. The MEF library, however, provides extensions that can be reused in multiple applications. With the help of MEF, the application can not only locate the extension but also load it in the application.

# Parallel Computing

Parallel computing is a process in which a large problem is divided into small units and then these units are solved parallelly. Sometimes personal computers and workstations have two or three Central Processing Units (CPUs) that enable multiple threads to be executed simultaneously. In such a situation, a new programming model is provided by .NET Framework 4.0 that allows the developers to develop multithreaded and asynchronous code. This new programming model is known as parallel computing, which is supported by new runtime, class library types, and diagnostic tools. In parallel computing, you need to distribute the code for execution across multiple processors. Note that to implement parallel computing, you need to import the System.Threading.Tasks namespace, which is introduced with the .NET Framework 4.0 version.

# In-Process Side-by-Side Execution

The In-Process Side-by-Side Execution feature supports the loading and starting of multiple versions of .NET Framework by an application within the same process. For example, you can execute an application, which loads the components developed in .NET Framework 3.0 and .NET Framework 4.0 in the same process.

# Improved Security Model

A new and improved security model is introduced with .NET Framework 4.0. Many useful classes and services introduced in CLR and .NET Framework help the developers to write secure code and implement cryptography and role-based security. The following are the two major changes introduced in .NET Framework 4.0 security system:

+   - There is no machine-wide security policy, although the user permissions system remains the same.
+   - The default enforcement mechanism is changed to security transparency.

# Networking Improvements

The following are the various networking improvements implemented in .NET Framework 4.0:

+   - Improvements in classes for Windows authentication, such as System.Net.HttpWebRequest, System.Net.HttpListener, System.Net.Mail.SmtpClient, and System.Net.Security.NegotiateStream
+   - Improvements in support for Network Address Translation (NAT) traversal using IPv6 and Teredo
+   - Introduction of new networking performance counters that provide information about HttpWebRequest objects
+   - Introduction of AddRange method in the System.Net.HttpWebRequest class