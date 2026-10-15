
```
obj = New Customer()
obj.FirstName = "Douglas"
obj.LastName = "Adams"
col.Add(obj.Name, obj)
obj = New Customer()
obj.FirstName = "Andre"
obj.LastName = "Norton"
col.Add(obj.Name, obj)
Dim item As Generic.KeyValuePair(Of String, Customer)
Dim sb As New System.Text.StringBuilder
For Each item In col
    sb.AppendLine(item.Value.Name)
Next
MsgBox(sb.ToString)
End Sub
```

This code simply creates a couple of `Customer` objects, sets their `FirstName` and `LastName` properties, and inserts them into a generic `SortedDictionary` object from the `System.Collections.Generic` namespace.

Items in a `SortedDictionary` are sorted based on their key value, and you are using the `Name` property to provide that key, meaning that your entries will be sorted by name. Because your `Name` property is implemented to return first name first and last name second, your entries will be sorted by first name.

If you run the application, the dialog will display the following:

```
Andre Norton
Douglas Adams
```

However, you can change the implementation of your Contact class — not directly changing or affecting either the Customer class or your code in `Form1` — to return last name first and first name second, as shown here:

```
Public ReadOnly Property Name() As String
    Get
        Return mLastName & ", " & mFirstName
    End Get
End Property
```

While no other code requires changing, and no syntax errors are flagged, the behavior of the application is changed. When you run it, the output will now be as follows:

```
Adams, Douglas
Norton, Andre
```

Maybe this change is inconsequential. Maybe it totally breaks the required behavior of your form. The developer making the change in the Contact class might not even know that someone was using that property for sort criteria.

This illustrates how dangerous inheritance can be. Changes to implementation in a base class can cascade to countless other classes in countless applications, having unforeseen side effects and consequences of which the base-class developer is totally unaware.

## SUMMARY

This chapter demonstrated how Visual Basic enables you to create and work with classes and objects. Visual Basic provides the building blocks for abstraction, encapsulation, polymorphism, and inheritance.

You have learned how to create both simple base classes as well as abstract base classes. You have also explored how you can define formal interfaces, a concept quite similar to an abstract base class in many ways.

You also walked through the process of subclassing, creating a new class that derives both interface and implementation from a base class. The subclass can be extended by adding new methods or altering the behavior of existing methods on the base class.

By the end of this chapter, you have seen how object-oriented programming flows from the four basic concepts of abstraction, encapsulation, polymorphism, and inheritance. The chapter provided basic information about each concept and demonstrated how to implement them using Visual Basic.

By properly applying object-oriented design and programming, you can create very large and complex applications that remain maintainable and readable over time. Nonetheless, these technologies are not a magic bullet. Improperly applied, they can create the same hard-to-maintain code that you might create using procedural or modular design techniques.

It is not possible to fully cover all aspects of object-oriented programming in a single chapter. Before launching into a full-blown object-oriented project, we highly recommend looking at other books specifically geared toward object-oriented design and programming.

## The Common Language Runtime

**WHAT YOU WILL LEARN IN THIS CHAPTER**
- Elements of a .NET Application
- Versioning and Deployment
- Understanding the Common Language Runtime
- IL Disassembler
- Memory Management
- Namespaces
- The My Keyword

You’ve learned how to create simple applications and looked at how to create classes. Now it’s time not only to start tying these elements together, but also to learn how to dispose of some of the classes that you have created. The architects of .NET realized that all procedural languages require certain base functionality. For example, many languages ship with their own runtime that provides features such as memory management, but what if, instead of each language shipping with its own runtime implementation, all languages used a common runtime? This would provide languages with a standard environment and access to all of the same features. This is exactly what the common language runtime (CLR) provides.

The CLR manages the execution of code on the .NET platform. .NET provided Visual Basic developers with better support for many advanced features, including operator overloading, implementation inheritance, threading, and the ability to marshal objects. Building such features into a language is not trivial. The CLR enabled Microsoft to concentrate on building this plumbing one time and then reuse it across different programming languages. Because the CLR supports these features and because Visual Basic is built on top of the CLR, Visual Basic can use these features. As a result, going forward, Visual Basic is the equal of every other .NET language, with the CLR eliminating many of the shortcomings of the previous versions of Visual Basic.

Visual Basic developers can view the CLR as a better Visual Basic runtime. However, this runtime, unlike the old standalone Visual Basic runtime, is common across all of .NET regardless of the underlying operating system. Thus, the functionality exposed by the CLR is available to all .NET languages; more important, all of the features available to other .NET languages via the CLR are

available to Visual Basic developers. Additionally, as long as you develop using managed code — code that runs in the CLR — you’ll find that it doesn’t matter whether your application is installed on a Windows XP client, a Vista client, or a Windows 7 client; your application will run. The CLR provides an abstraction layer separate from the details of the operating system.

This chapter gets down into the belly of the application runtime environment — not to examine how .NET enables this abstraction from the operating system, but instead to look at some specific features related to how you build applications that run against the CLR. This includes an introduction to several basic elements of working with applications that run in the CLR, including the following:

- Elements of a .NET application
- Versioning and deployment
- Integration across .NET languages
- Microsoft intermediate language (MSIL)
- Memory management and the garbage collector (GC)

### ELEMENTS OF A .NET APPLICATION

A .NET application is composed of four primary entities:

- **Classes** — The basic units that encapsulate data and behavior
- **Modules** — The individual files that contain the intermediate language (IL) for an assembly
- **Assemblies** — The primary unit of deployment of a .NET application
- **Types** — The common unit of transmitting data between modules

Classes, covered in the preceding two chapters, are defined in the source files for your application or class library. Upon compilation of your source files, you produce a module. The code that makes up an assembly’s modules may exist in a single executable (.exe) file or as a dynamic link library (.dll). A module, is in fact, a Microsoft intermediate language (MSIL) file, which is then used by the CLR when your application is run. However, compiling a .NET application doesn’t produce only an MSIL file; it also produces a collection of files that make up a deployable application or assembly. Within an assembly are several different types of files, including not only the actual executable files, but also configuration files, signature keys, and, most important of all, the actual code modules.

### Modules

A module contains Microsoft intermediate language (MSIL, often abbreviated to IL) code, associated metadata, and the assembly’s manifest. By default, the Visual Basic compiler creates an assembly that is composed of a single module containing both the assembly code and the manifest.

IL is a platform-independent way of representing managed code within a module. Before IL can be executed, the CLR must compile it into the native machine code. The default method is for the CLR to use the JIT (just-in-time) compiler to compile the IL on a method-by-method basis. At runtime, as each method is called by an application for the first time, it is passed through the JIT compiler for compilation to machine code. Similarly, for an ASP.NET application, each page is passed through the JIT compiler the first time it is requested, to create an in-memory representation of the machine code that represents that page.

Additional information about the types declared in the IL is provided by the associated metadata. The metadata contained within the module is used extensively by the CLR. For example, if a client and an object reside within two different processes, then the CLR uses the type’s metadata to marshal data between the client and the object. MSIL is important because every .NET language compiles down to IL. The CLR doesn’t care about or even need to know what the implementation language was; it knows only what the IL contains. Thus, any differences in .NET languages exist at the level where the IL is generated; but once generated, all .NET languages have the same runtime characteristics. Similarly, because the CLR doesn’t
