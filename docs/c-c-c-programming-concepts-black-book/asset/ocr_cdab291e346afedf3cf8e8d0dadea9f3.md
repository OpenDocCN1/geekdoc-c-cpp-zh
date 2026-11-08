# Class Library

Generally, the .NET class library is referred to as the .NET Framework Class Library (FCL), whose subset is Base Class Library (BCL). FCL contains a huge set of reusable classes and interfaces as well as value types that provide prefabricated functionalities from reading an XML file to designing a graphic interface. In addition, FCL helps the developers to optimize their development process and provide access to the system functionality. Those who are already familiar with Java may know about the class library. However, .NET class library provides a much broader set of functionalities than any other language can provide. Languages that are supported by .NET architecture can refer to these defined in FCL.

FCL is organized in a hierarchical manner using namespaces, which represent a collection of functionalities that specify a single logical task. Consistent base types provided by FCL are used by all the .NET-supported languages. The namespaces access these base type classes and the assemblies in turn hold these namespace references.

The System namespace is the root namespace that contains the Object base types from which all the other value and reference types are derived. The namespace also provides the main types, such as integer, string, and character, which are mostly used in an application. Other than this, it provides functionalities, such as exception handling, console I/O operations, and math operations, as well as utility types that convert different data types safely. However, to use the utility classes, we need to know which namespace to refer. Therefore, developers can create their own customized namespaces that refer the FCL or they can directly refer to the FCL namespaces into their application. Table 16.1 represents some of the commonly used namespaces of FCL:

**Table 16.1: Commonly used Namespaces of FCL**

| Namespace | Description |
|---|---|
| Microsoft.CSharp | Consists of the classes that are used for compilation and code generation using C#. |
| Microsoft.JScript | Consists of the classes that are used for compilation and code generation using JavaScript. |
| Microsoft.VisualBasic | Consists of the classes that are used for code generation using Visual Basic.NET (VB.NET). |
| System | Consists of the fundamental and base classes that define data types, events, event handlers, interfaces, attributes, and exception handling. |
| System.CodeDom | Consists of the classes that are used for the elements as well as the source code document structure. The elements are used to structure a source code document that will output as a source code in a specified .NET supported language by using System.CodeDom.Compiler. |
| System.CodeDom.Compiler | Consists of the types that are used to handle the generation and compilation of the source code in the specified supported language. |
| System.Collection | Consists of the interfaces and classes that are used to manage the collection of objects, such as Stack, Queue, and Hashtables. |
| System.Configuration | Contains the classes that are used to manage the .NET Framework configuration as well as to name the .config file in an application. |
| System.Data | Contains the classes that support ADO.NET architecture. |
| System.Diagnostics | Contains the classes that interact with system processes, event log, and performance counter; thereby, allowing us to debug an application. |
| System.Drawing | Contains the classes that help in drawing 2D images in an application. |