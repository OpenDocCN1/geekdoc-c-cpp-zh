
required by the application. In other words, the VES provides the services and infrastructure to abstract both platform and language differences.

As part of the loading and compilation process, the VES performs various validation and verification checks to ensure that the file format, assembly metadata, and CIL are consistent and that the CIL instructions themselves do not allow illegal memory access. This ensures that an application can access only memory or other resources to which it has been explicitly granted access. This restricted environment can be thought of as a **sandbox**.

If the VES provides a runtime environment and executes assemblies containing CIL, are those assemblies interpreted or compiled? Remember, one of the goals for the .NET Framework is to provide a runtime environment that minimizes or eliminates the performance problems of scripted or interpreted languages. This would imply that the CIL code is compiled, but when does that compilation happen?

One of the services the VES provides is the **Just-In-Time (JIT) compiler**. Just-In-Time compilation is the process of taking the partially compiled CIL code and generating executable object code, or native code, at runtime.

### *Did you know? Just-In-Time Compilation*

> The process of Just-In-Time compilation is called **jitting** and the JIT compiler is also called the **jitter**.

By compiling the code in this manner, the .NET Framework gains a considerable speed improvement over traditional interpreted languages. Just-In-Time compilation also has benefits over regular (static) compilation, as it can enforce security guarantees at runtime and recompile the code at runtime to gain additional optimizations. The .NET Framework JIT compiler is highly optimized for compiling CIL code into highly efficient object code, runs on demand, and caches the compiled code for future use.

## Memory Management and Garbage Collection

Proper memory management is a classic problem in many unmanaged programming languages and is a potential source for some common errors. In these languages, the developer is responsible for allocating and deallocating memory at the correct times. The .NET Framework resolves this problem by controlling these memory allocations and deallocations automatically as part of the VES.

It is this automatic memory management, also known as **garbage collection**, which makes C# (and the other .NET languages) a **garbage-collected language**. Garbage collection frees you from having to worry as much about releasing memory when it is no longer needed. This enables you to create applications that are more stable by preventing many of those common programming errors and focusing your time on the business logic your application requires.

Even with automatic memory management, it is still important to understand how the garbage collector interacts with your program and the types you create. An in-depth discussion on garbage collection is well outside the scope of this book, but we talk a little bit more about it in Hour 22, “Memory Organization and Garbage Collection.”

## Framework Class Library

Although the CLR forms the core of the .NET Framework, the framework class library (FCL) actually gives it substance. The class library is similar to Java's class libraries, the C++ Standard Template Library (STL), Microsoft's Active Template Library (ATL), the Microsoft Foundation Classes (MFC), Borland's Object Windows Library (OWL), or any of the various other class libraries available today.

Just like those class libraries, the FCL is a rich set of reusable types enabling you to achieve a high level of developer productivity by simplifying many common programming tasks.

Figure 1.2 shows some of the types available in the FCL, grouped by functional area.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_33_0.png)

### Figure 1.2
**Framework Class Library**

*By the Way*
The framework class library is the best example in the .NET Framework of making the simple things easy and the hard things possible.
Although it is possible to create an application without using the types provided by the FCL, it is impractical to do so.

At the lowest level are the **Base Class Libraries (BCL)** that serve as the standard run-time for any .NET language and provide types that represent the intrinsic CLR types, collections, streams, string manipulation, basic file access, and a variety of other operations or data structures. In total, there are 172 publicly available types in the BCL and 331 total public types in what is considered the Standard Library as defined by the Standard Ecma-335: Common Language Infrastructure (CLI), 4th Edition/June 2006.

### Did you Know?

### What Is Ecma?

Ecma International is an international standards association founded in 1961 that aims to help develop standards for the use of information communication technology and consumer electronics.

The C# Language Specification along with the Common Language Infrastructure (CLI) were accepted as an Ecma standard on December 14, 2001.

The CLI is an open source version of the Common Language Runtime. It has fostered several open source versions of C# and the .NET Framework, including DotGNU and Mono. Of these, Mono is probably the most well known and provides an implementation of the .NET development platform on Linux, BSD, UNIX, Mac OS X, Solaris, and Windows operating systems.

It is the open source standards provided by Ecma and projects such as DotGNU and Mono that enable development skills and applications to be used on virtually any platform.

The remaining classes in the FCL are focused on specific functional areas, such as providing data access, XML support, globalization support, diagnostics, configuration, networking, communication, business workflow support, web applications, and Windows desktop applications, to name just a few.

## Namespaces

With thousands of classes in the .NET Framework class library, there needs to be a way to prevent ambiguity between type names and to provide a convenient hierarchical grouping mechanism. The .NET Framework uses the concept of **namespaces** to accomplish this. A namespace is simply a collection of types and has no effect on the accessibility of a type. Namespaces can be split across multiple assemblies. The .NET Framework uses the hierarchical nature of namespaces to provide a progressive framework, creating a powerful and easy-to-use development platform.

### Namespaces and Type Names

Namespaces use a dotted syntax to denote a hierarchical grouping, with each level in the hierarchy separated by a dot (.).

Given a type's full name, everything up to the rightmost dot is the namespace whereas the last part (after the rightmost dot) is the type name. For example, System.Printing.PrintDriver is the full name for the PrintDriver type in the System.Printing namespace.

Namespaces, however, are only conveniences supported by the .NET programming languages. In the CLR, a type is always identified by its full name, which contains both the name of the type and its containing namespace.

Almost 400 namespaces exist in the .NET Framework class library, although you will probably never interact with some of them. As you become more familiar with the class library, you will find certain namespaces that you use more frequently than others, which might be a different set than ones your co-workers or peers use.

The most commonly used namespaces are shown in Table 1.1.

### TABLE 1.1 Commonly Used Namespaces

| Namespace | Description |
| :--- | :--- |
| System | The base, or root, namespace for .NET; contains classes that define the commonly used data types, exceptions, and events |
| System.Collections.Generic | Contains classes that define various generic collections, enabling you to create strongly typed collections |
| System.Data | Contains classes that form the majority of the ADO.NET library, enabling you to manage data from multiple data sources |
| System.Diagnostics | Contains classes that enable you to interact with event logs and performance counters, debug your application, and trace the execution of your code |
| System.Globalization | Contains classes that represent culture-related information, including the language, country/region, calendars in use, sort order for strings, and format patterns for dates, currency, and numbers |
| System.IO | Contains classes that enable synchronous and asynchronous reading and writing on data streams and files |
