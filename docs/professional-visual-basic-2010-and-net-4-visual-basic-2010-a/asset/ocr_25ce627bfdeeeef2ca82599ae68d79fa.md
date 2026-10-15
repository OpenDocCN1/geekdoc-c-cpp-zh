available to Visual Basic developers. Additionally, as long as you develop using managed code — code that runs in the CLR — you’ll find that it doesn’t matter whether your application is installed on a Windows XP client, a Vista client, or a Windows 7 client; your application will run. The CLR provides an abstraction layer separate from the details of the operating system.

This chapter gets down into the belly of the application runtime environment — not to examine how .NET enables this abstraction from the operating system, but instead to look at some specific features related to how you build applications that run against the CLR. This includes an introduction to several basic elements of working with applications that run in the CLR, including the following:

+   > Elements of a .NET application
+   > Versioning and deployment
+   > Integration across .NET languages
+   > Microsoft intermediate language (MSIL)
+   > Memory management and the garbage collector (GC)

# ELEMENTS OF A .NET APPLICATION

A .NET application is composed of four primary entities:

+   > **Classes** — The basic units that encapsulate data and behavior
+   > **Modules** — The individual files that contain the intermediate language (IL) for an assembly
+   > **Assemblies** — The primary unit of deployment of a .NET application
+   > **Types** — The common unit of transmitting data between modules

Classes, covered in the preceding two chapters, are defined in the source files for your application or class library. Upon compilation of your source files, you produce a module. The code that makes up an assembly’s modules may exist in a single executable (.exe) file or as a dynamic link library (.dll). A module, is in fact, a Microsoft intermediate language (MSIL) file, which is then used by the CLR when your application is run. However, compiling a .NET application doesn’t produce only an MSIL file; it also produces a collection of files that make up a deployable application or assembly. Within an assembly are several different types of files, including not only the actual executable files, but also configuration files, signature keys, and, most important of all, the actual code modules.

# Modules

A module contains Microsoft intermediate language (MSIL, often abbreviated to IL) code, associated metadata, and the assembly’s manifest. By default, the Visual Basic compiler creates an assembly that is composed of a single module containing both the assembly code and the manifest.

IL is a platform-independent way of representing managed code within a module. Before IL can be executed, the CLR must compile it into the native machine code. The default method is for the CLR to use the JIT (just-in-time) compiler to compile the IL on a method-by-method basis. At runtime, as each method is called by an application for the first time, it is passed through the JIT compiler for compilation to machine code. Similarly, for an ASP.NET application, each page is passed through the JIT compiler the first time it is requested, to create an in-memory representation of the machine code that represents that page.

Additional information about the types declared in the IL is provided by the associated metadata. The metadata contained within the module is used extensively by the CLR. For example, if a client and an object reside within two different processes, then the CLR uses the type’s metadata to marshal data between the client and the object. MSIL is important because every .NET language compiles down to IL. The CLR doesn’t care about or even need to know what the implementation language was; it knows only what the IL contains. Thus, any differences in .NET languages exist at the level where the IL is generated; but once generated, all .NET languages have the same runtime characteristics. Similarly, because the CLR doesn’t