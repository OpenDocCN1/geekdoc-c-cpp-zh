
// Set text of the document
Word::Range^ range=doc->Content;
range->default="Datasim Education BV";
}
catch(System::Runtime::InteropServices::COMException^ ex)
{
    Console::WriteLine("HRESULT: {0}\n{1}",
    ex->ErrorCode, ex->Message);
}

## 27.11.3 COM Callable Wrapper (CCW)

For some applications we may wish to use .NET components from non .NET applications, for example creating Office add-ins in .NET or accessing .NET code from VBA. To this end, the runtime automatically creates a COM proxy class around a .NET class. The design is shown in Figure 27.8. Some salient features of this design are:

- The runtime creates exactly one CCW for a managed object irrespective of the number of COM clients requesting its services.
- Multiple COM clients hold a reference to the CCW that exposes an interface.
- The CCW holds a single reference that implements the interface. It is garbage collected.
- CCWs are invisible to other classes running in the .NET Framework.
- CCWs marshal calls between managed and unmanaged code. They also manage the object identity and object lifetime of the managed objects that they wrap.

For more details on the topics in this section, see Bovey et al. (2009).

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_893_0.png)

FIGURE 27.8 COM Callable Wrapper (CCW)

## 27.12 ASSEMBLIES AND NAMESPACES FOR C++/CLI

When developing applications in native C++ we have to decide how to distribute the code to clients. There are several options. First, the supplier can deliver the code as a collection of header-only files (as in the majority of libraries in *Boost*, for example) or as a combination of source files and (static) library files (as with *QuantLib*, for example). We have already discussed how to create static libraries in Chapter 8.

We now create applications in .NET by deploying assemblies. An *assembly* is the basic *unit of deployment* in .NET. It contains compiled types, *Intermediate Language* (IL) code, run-time resources and information relating to versioning, security and the referencing of other assemblies. At file level, an application is an assembly with a .exe extension while a reusable library is an assembly with a .dll extension.

An assembly contains the following entities:

- *Assembly manifest*: this is a description of the contents of the assembly such as the list of types, resources and files that make up the assembly, the list of assemblies referenced by this assembly and the required permissions to run the code in the assembly. It also contains the name of the assembly, its version and *culture* (a culture represents a particular human language; .NET supports the RFC 1766 standard that represents cultures and subcultures as two-letter codes. For example, the codes for English and German cultures are en and de, respectively, while Australian English and Austrian German have the codes en-AU and de-AT, respectively).
- *Application manifest*: this provides information to the operating system on how the assembly should be deployed. The application manifest is an XML file that imparts information concerning the assembly to the operating system.
- *Compiled code*: the IL code and metadata of the types and methods in the assembly. The presence of metadata implies that the assembly is *self-describing*.
- *Resources*: additional data and non-executable code such as strings, bitmaps and localisable text.

### 27.12.1 Assembly Types

Assemblies are similar to traditional DLLs because both are units of deployment. But in contrast to DLLs, assemblies do not need to define *Windows Registry* settings. Furthermore, assemblies support version control while DLLs do not and multiple assembly versions can be installed in applications.

The two major assembly types are called *private* and *shared assemblies*. A *private assembly* is one that can only be used by a single application. The corresponding .dll file is stored in the application directory. To create an assembly DLL we create a *Class Library* project in Visual Studio, add relevant classes to the project and then we compile and build the project. Having done that, we use this assembly DLL as part of an application by adding it as a *reference* to a Windows or Console application project. We note that the assembly DLL must be in the same directory as, or in a sub-directory of, the directory in which the main .exe file resides. A typical example of a private assembly is one that contains classes for dates, day count conventions and calendars. It can be used in many fixed-income applications.

From a software design viewpoint, we can design a software system as a set of loosely coupled subsystems. We package each subsystem as a separate assembly and each assembly can be designed and tested independently of the other assemblies. Having done that, we can deploy these assemblies as reusable components in various applications and they can be separately versioned. Finally, assemblies can be loaded at run-time, which improves performance and interoperability.

A shared assembly is one that can be used by many applications. It must be stored in a special directory called the Global Assembly Cache (GAC), which is a central repository for centralising version-based assemblies. As developer, it is possible to create shared assemblies and place them in the GAC but a discussion of this topic is outside the scope of this book. However, we do need to understand the structure of the GAC and how assembly versioning and security are realised. To this end, we give a short introduction to strong names that uniquely identify an assembly in the GAC.

A strong name is generated from the following components:

- The assembly ‘simple’ name (this is a string).
- The version number (of the form a.b.c.d containing numeric values).
- The culture.
- The assembly’s public key.

Each assembly has a version number of the form a.b.c.d where a represents a major release, b a minor release, c is a build number and d is a revision. The default value is 0.0.0.0. The GAC can contain multiple versions of a shared assembly and different assembly versions can be instantiated at the same time. The client decides which version to use.

We can view the contents of the GAC by examining the contents of the directory C:\Windows\assembly. When creating Visual Studio projects you can add an assembly from the GAC by using the Add Reference option. We can choose between .NET and .COM components. For example, we use the GAC to include Excel interop into an application, thus allowing us to access the Excel object model.

### 27.12.2 Specifying Assembly Attributes in AssemblyInfo.cs

It is possible to control the contents of an assembly to a large extent by setting the values of the attributes in a file called AssemblyInfo.cs (or AssemblyInfo.cpp) that is automatically created with each new C# or C++/CLI project. It contains default values which you can change to suit your needs.

Some relevant attributes are:

- AssemblyTitle: a friendly name for the assembly.
- AssemblyDescription: a description of the assembly.
- AssemblyConfiguration: specifies if the assembly is for debug or release mode.
- AssemblyCompany: specifies the creator of the assembly.
- AssemblyProduct: specifies the name of the product.
- AssemblyCopyright: a copyright information string.
- AssemblyTrademark: specifies trademark information.
- AssemblyCulture: this attribute specifies the supported language; we leave it empty if the assembly is language neutral.

An example of the assembly file is:

```
using System.Reflection;
using System.Runtime.CompilerServices;
using System.Runtime.InteropServices;

// General Information about an assembly is controlled through the
// following set of attributes. Change these attribute values to modify
// the information associated with an assembly.
[assembly: AssemblyTitle("LoadDateLibrary")]
[assembly: AssemblyDescription("Dates and Day Counts")]
[assembly: AssemblyConfiguration("release")]
[assembly: AssemblyCompany("Datasim Education BV")]
[assembly: AssemblyProduct("Germani and Duffy")]
[assembly: AssemblyCopyright("Copyright © Datasim Education BV 2010")]
[assembly: AssemblyTrademark("TM Duffy Germani")]
[assembly: AssemblyCulture("")]

// Setting ComVisible to false makes the types in this assembly not
// visible to COM components. If you need to access a type in this
// assembly from COM, set the ComVisible attribute to true on that type.
[assembly: ComVisible(false)]

// The following GUID is for the ID of the typelib if this
// project is exposed to COM
[assembly: Guid("ec444bce-76db-4935-9017-78f5aed1e693")]

[assembly: AssemblyVersion("2.0.0.0")]
[assembly: AssemblyFileVersion("2.0.0.0")]
```

### 27.12.3 An Example: Dynamically Loading Algorithms from an Assembly

We have seen how to create C++ static libraries in Section 8.9. They resolve the problem of having to provide source code to clients. This solution is not very flexible as static libraries tend to be large monolithic beasts and they cannot be replaced by other libraries at run-time. The .NET Framework on the other hand supports configurable assemblies. To show how effective the use of assemblies is we take a model example from CAD (computer aided design) in which we create geometrical objects. In particular, we create flexible algorithms (Strategy design pattern) to calculate the distance between two points.

The UML class diagram is shown in Figure 27.9, which was originally discussed in Duffy and Germani (2013) and programmed in C#. What we do is to reuse the C# code from that book which implements the distance algorithms and we test them by encapsulating them in an
