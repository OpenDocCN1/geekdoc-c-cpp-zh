The manifest can be stored in a separate file or in one of the modules. By default, for most applications, it is part of the .dll or .exe file, which is compiled by Visual Studio. For Web applications, you will find that although there is a collection of ASPX pages, the actual assembly information is located in a DLL referenced by those ASPX pages.

# Types

The type system provides a template that is used to describe the encapsulation of data and an associated set of behaviors. It is this common template for describing data that provides the basis for the metadata that .NET uses when applications interoperate. There are two kinds of types: reference and value. The differences between these two types are discussed in Chapter 1.

Unlike COM, which is scoped at the machine level, types are scoped at either the global level or the assembly level. All types are based on a common system that is used across all .NET languages. Similar to the MSIL code, which is interpreted by the CLR based upon the current runtime environment, the CLR uses a common metadata system to recognize the details of each type. The result is that all .NET languages are built around a common type system, unlike the different implementations of COM, which require special notation to enable translation of different data types between different .exe and .dll files.

A type has fields, properties, and methods:

+   > **Fields** — Variables that are scoped to the type. For example, a Pet class could declare a field called Name that holds the pet's name. In a well-engineered class, fields are often kept private and exposed only as properties or methods.
+   > **Properties** — Properties look like fields to clients of the type but can have code behind them (which usually performs some sort of data validation). For example, a Dog data type could expose a property to set its gender. Code could then be placed behind the property so that it could be set only to “male” or “female,” and then this property could be saved internally to one of the fields in the Dog class.
+   > **Methods** — Methods define behaviors exhibited by the type. For example, the Dog data type could expose a method called Sleep, which would suspend the activity of the Dog.

The preceding elements make up each application. Note that some types are defined at the application level, and others are defined globally. Under COM, all components are registered globally; and certainly if you want to expose a .NET component to COM, you must register it globally. However, with .NET it is not only possible but often encouraged that the classes and types defined in your modules be visible only at the application level. The advantage of this is that you can run several different versions of an application side by side. Of course, once you have an application that can be versioned, the next challenge is knowing which version of that application you have.

# VERSIONING AND DEPLOYMENT

Components and their clients are often installed at different times by different vendors. For example, a Visual Basic application might rely on a third-party grid control to display data. Runtime support for versioning is crucial for ensuring that an incompatible version of the grid control does not cause problems for the Visual Basic application.

In addition to this issue of compatibility, deploying applications written in previous versions of Visual Basic was problematic. Fortunately, .NET provides major improvements over the versioning and deployment offered by COM and the previous versions of Visual Basic before .NET.

# Better Support for Versioning

Managing component versions was challenging in previous versions of Visual Basic. The version number of the component could be set, but this version number was not used by the runtime. COM components are