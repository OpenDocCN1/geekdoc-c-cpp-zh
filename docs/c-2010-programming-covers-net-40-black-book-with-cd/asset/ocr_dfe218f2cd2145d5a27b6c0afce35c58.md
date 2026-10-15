# In Depth

In today’s world of computer programs, reflection is considered as an important technique of programming, as it is used to extract every detail of a program at runtime. In .NET Framework 4.0, a program is said to be reflected on itself when it extracts metadata (self information) from its assembly and uses this metadata for finding assemblies, modules, and type information at runtime.

Reflection is of great significance while developing large applications due to its capability to collect and manipulate the data present in the assemblies and metadata of the applications. It is also necessary for adequate versioning, dynamic loading of classes, and proper security handling of applications. In addition, reflection helps you to get the information of the classes, functions, and types existed in the Dynamically Linked Libraries (DLLs) files. Moreover, in C# 2010, you can implement reflection by using the classes contained in the System.Reflection namespace. Some examples of these classes are Assembly, Module, MethodInfo, and ConstructorInfo.

In this chapter, you learn about the importance of reflection process in C# 2010. This chapter starts with exploring the reflection process, wherein you learn the need and use of the reflection process. Next, you learn about dynamic loading of assemblies using reflection. In the Immediate Solutions section, you learn to use reflection to obtain class and type information from an assembly, and how to obtain member information from a class. Finally, this chapter explains how to use reflection for verifying and dumping the methods and parameters of a class.

Let’s start with exploring the reflection process.

# Exploring the Reflection Process

Reflection is defined as the process of finding out the internal elements, such as metadata, assemblies, modules and types, of an application without accessing the source code. You can also use reflection to find all classes in an assembly, and all the methods, properties, and events that might be supported by each of these classes. Reflection also allows you to search for all kinds of information about a class, such as the base class from which it is derived and the interfaces it supports, and to explore the Common Language Runtime (CLR) programmatically.

The inspection and manipulation of a C# program according to a desired goal is done with the help of reflection. You can inspect all the information about a class and also use reflection techniques to dynamically invoke methods of the class at runtime. The generated code of the methods in the class can be executed directly in the application at runtime.

With the help of reflection, the information in the metadata segment of your assemblies at runtime can be viewed. In a nutshell, reflection enables you to see the data the way the compiler recognizes it when it is building your application into an Executable file (EXE file). You then have the flexibility to create applications that can be extended at runtime by taking advantage of other functionalities on a user’s system. Reflection can also be used, for example, to investigate whether certain classes exist in your home directory and, if so, to load and use them in your own application.

In a programming language without reflection, you are required to know which classes, functions, and types existed in the DLLs before you start using them. As the name suggests, DLLs can be dynamically loaded, but cannot be used dynamically. You cannot, for example, search through a set of DLLs for a function of a given name. Even if you are able to find the function and load it, you have no means to ask the system what parameters can be passed to it. C# reflection provides you this capability.

Next, you learn about the need of reflection.

# Need of Reflection

Reflection is an important feature of .NET Framework because it is used to extract every detail of class in .NET Framework. Reflection is of great significance while developing large applications due to its capability to collect and manipulate the data present in the assemblies and metadata of the applications. It is also necessary because