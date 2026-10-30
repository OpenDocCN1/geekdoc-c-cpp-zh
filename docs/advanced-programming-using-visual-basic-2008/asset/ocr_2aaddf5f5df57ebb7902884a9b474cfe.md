sometimes referred to as just **IL**. MSIL is a platform-independent set of instructions that is combined with the metadata to form a file called a *portable executable* (PE) file, which has an .exe or .dll extension. When your program runs, MSIL is converted to the native code of the specific machine only as it is needed, using a just-in-time (JIT) compiler, which is part of the CLR (Figure 1.1).

![](bbox=[0.075, 0.18, 0.95, 0.315])

# Assemblies

An assembly is a basic unit of code that may be a single PE file or multiple files. Each of your applications will be contained in a single assembly, which is the smallest deployable piece of code. An assembly has an **assembly manifest** that contains metadata about the version, a table describing all of the files needed for the assembly, and an “assembly reference list” that specifies all of the external files needed, such as DLLs created by someone else. An assembly is similar to an .exe or a .dll file written in earlier versions of Visual Basic—it contains all of the necessary information to run the application or component.

Recall that the .NET Framework class library is not one big file but rather a collection of files. The classes are stored in many files with the extension .dll and referred to as DLLs (for dynamic link libraries). Each of the DLLs in the class library is one assembly. As your program begins execution, only the needed assemblies are loaded into memory. When you want to use a type that is not already referenced, you must add a reference to the DLL (assembly).

# Attributes

**Attributes** are tags containing information about parts of a program such as types or methods. The system defines many attributes of your assembly, such as the name, version, culture, and security. The attributes are part of the metadata in a .NET assembly. The process of examining the metadata in an assembly’s attributes is called *reflection*.

Later in this chapter, you will learn to retrieve and use the custom attributes in a project’s assembly information, which is stored in the Assembly-Info.vb file.

# The References Collection

A **reference object** is used to connect a Visual Basic project to external components. The two types of reference objects are assemblies and COM objects. A reference to another project is an assembly reference and is called a *project-to-project reference*. COM objects are components written in versions of VB prior to .NET, or other non-CLS-compliant languages.