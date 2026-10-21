
## Assembly Manifest

An assembly manifest contains metadata pertaining to an assembly. It is due to the assembly manifest that an assembly becomes self-describing in nature. It acts as an interface for the outside world to interact with the assembly. The contents of an assembly manifest contain the following information:

- The name of the assembly
- The version of the assembly
- The strong name attributes, that is public key and digital signature
- The list of files belonging to the assembly
- Reference information used by the CLR for referencing assembly types
- Information pertaining to the other assemblies that are referenced by the current assembly

A programmer can manipulate the information contained in the assembly manifest with the help of assembly attributes, such as AssemblyCultureAttribute and AssemblyVersionAttribute.

You can view the assembly manifest for an assembly with the help of the ILDasm disassembler tool. Figure D.1 shows a sample assembly manifest:

![](img/bae4ee2c7c29c052feb3b9a9c5659998_475_0.png)

## Types of Assemblies

The various types of assemblies are the following:

- Multi-module Assembly As the name suggests, a multi-module assembly comprises of multiple modules contained in different files. The assembly manifest keeps track of the information pertaining to different modules. In addition, each module has a manifest of its own for storing module-specific information. In case of multi-module assemblies, the assembly manifest may exist either independently in a separate file or inside one of the modules.
- **Private Assembly** If an assembly is created as private then it can only be used by the application for which it is created. Other applications do not have access to private assemblies. Unless explicitly specified, the C# compiler creates private assemblies when an application is compiled.
- **Shared Assembly** In contrast to private assemblies, the shared assemblies can be used by different non-related applications. For facilitating sharing of assemblies, it is necessary to give them a strong name. A strong name makes use of assembly name, version number, public key and digital signature to allocate a globally unique name to the assembly. It is also required for a shared assembly to be registered in the Global Assembly Cache (GAC).

## D.2 VERSIONING

As already explained, versioning of assemblies helps in their identification by the CLR. An assembly version assumes the format of a four part numerical string, as shown below:

```
<major version number>.<minor version number>.<build version number>.<revision number>
```

For example, version 2.5.11.1 represents an assembly with 1 as the revision number, 11 as the build version number, 5 as the minor version number and 2 as the major version number. If no version number is assigned to an assembly then by default it assumes the value 0.0.0.0. The version information is typically used along with the public key to allocate a strong name to the assembly.

The assembly version is set with the help of the AssemblyVersionAttribute attribute. The following is an example of using AssemblyVersionAttribute for setting the assembly version in C#:

```
[assembly:AssemblyVersionAttribute("1.2.5.0")]
```

Two different assemblies with the same name can exist in the system provided they have different version numbers. This situation may arise if a newer version of the assembly is created with the subsequent release of an application. However, the older assembly versions are also retained for ensuring backward compatibility.

## D.3 ATTRIBUTES

Attributes are objects that help associate data or information with various elements of a program. The information is stored as metadata and retrieved by the CLR at runtime. The program elements with which attributes are attached are referred as attribute targets.

Some of the examples of attribute targets are

- Assembly
- Class
- Interface
- Method
- Property
- Module
- All

There are two types of attributes: intrinsic and custom. As the name suggests, intrinsic attributes are the built-in attributes of .NET that are meant for certain pre-specified purposes. Custom attributes, on the other hand, are the user-defined attributes used for adding custom information to the targets.

## Intrinsic Attributes

.NET comes with a number of built-in or pre-defined attributes that are used for varied purposes during runtime. Table D.1 lists some of these intrinsic attributes along with their targets and functionality.

## Table D.1 C# Compiler Options

| ATTRIBUTE | TARGET | DESCRIPTION |
|---|---|---|
| DllImportAttribute | Method | Is used to specify the location of the dll from where a method is to be imported. |
| ObsoleteAttribute | All program elements excluding assemblies, modules, parameters and return values | Is used to mark the target as obsolete so that it can not be used in future. |
| SerializableAttribute | Class, struct, enum, and delegate | Is used to mark the target as serializable. |
| ConditionalAttribute | Method | Is used to instruct the compiler to ignore the method calls unless the relevant conditional compilation symbol is defined. |
| CLSCompliantAttribute | All program elements | Is used to specify whether the target is Common Language Specification (CLS) compliant or not. |

## Specifying Attributes

The specification of attributes is done inside an attribute section that is placed just before the target element declaration. The attribute section comprises of comma-separated attribute specifications placed inside square brackets, as shown below:

```
[Attribute1, Attribute2(Value2), Attribute3]
```

Let us now consider an example to demonstrate how attribute specification works. The following code represents a simple console based application that uses two classes:

## Program D.1 A SIMPLE CONSOLE-BASED APPLICATION USING TWO CLASSES

```
//ConsoleApplication1.cs
using System;
using System.Collections.Generic;
using System.Text;

namespace ConsoleApplication1
{
    public class ClassA
    {
        public void display ()
        {
            Console.WriteLine("Hello! We are in ClassA");
        }
    }
    class ClassB
    {
        public static void Main(string[] args)
        {

ClassA A = new ClassA();
A.display();
System.Console.Read();
}
}
```

The output of the above code is shown in Figure D.2:

![](img/bae4ee2c7c29c052feb3b9a9c5659998_478_0.png)

Now, let’s add a slight modification to the code as shown below:

```
{
[Obsolete]
public class ClassA
{
```

Here, we have used the Obsolete attribute to mark ClassA as obsolete. Now, when we compile the application again, the compiler throws a warning message, as shown in Figure D.3:

![](img/bae4ee2c7c29c052feb3b9a9c5659998_478_1.png)

> Note: You may have noticed that in Table D.1, we have used the term ObsoleteAttribute to refer to the Obsolete attribute while in the code above we have only used the word Obsolete. Even though, the class implementation of attributes suffixes the word 'Attribute' at the end (e.g., ObsoleteAttribute); the C# compiler allows the specification of attributes only by their names (e.g., Obsolete).

## Custom Attributes

As already explained, custom attributes are the user-defined attributes used for adding custom information to the targets. To create a custom attribute you need to first create the corresponding class derived from the System.Attribute class. Then, you need to specify the types of targets that are associated with the custom attribute. This is done with the help of another attribute called AttributeUsage. Finally, you can use the newly created custom attribute just like the pre-defined .NET attributes.

To understand the concept of custom attributes with the help of an example, let us consider a scenario where you are required to identify all those classes and methods in your application that meet certain predefined coding conventions. You decide to create a custom attribute named CodeChecked to tag all those classes and methods that are compliant with the coding conventions. The following code modifies the previous ConsoleApplication1.cs program to create and use CodeChecked attribute:

## Program D.2

## USING CODE CHECKED ATTRIBUTE

```
//ConsoleApplication2.cs
namespace ConsoleApplication2
{
using System;
using System.Collections.Generic;
using System.Text;
using System.Reflection;

[AttributeUsage(AttributeTargets.Class |AttributeTargets.Method, AllowMultiple = false)]
public class CodeCheckedAttribute : System.Attribute
{
public CodeCheckedAttribute (string codestatus)
{
this.codestatus = codestatus;
}
public string codestatus
{
get
{
return codestatus;
}
set
{
codestatus = value;
}
}
}
public class ClassA
{
public void display()
{
Console.WriteLine("Hello! We are in ClassA");
}
}
[CodeChecked ("01247 Coding Convention Compliant")]
