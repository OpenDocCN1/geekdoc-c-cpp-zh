Win32 API (and other selected native Windows APIs) that provides consistent functionality across different types of hardware, from servers to phones. When you build a Universal Windows Platform (UWP) app, you use the APIs exposed by WinRT rather than Win32. Similarly, the CLR on Windows 10 also uses WinRT; all managed code written by using C# or any other managed language is still executed by the CLR, but at run time the CLR converts your code into WinRT API calls rather than Win32. Between them, the CLR and WinRT are responsible for managing and running your code safely.

A primary purpose of WinRT is to simplify the interoperability between languages so that you can more easily integrate components developed by using different programming languages into a single seamless application. However, this simplicity comes at a cost, and you have to be prepared to make a few compromises based on the different feature sets of the various languages available. In particular, for historical reasons, although C++ supports structures, it does not recognize member functions. In C# terms, a member function is an instance method. So, if you are building C# structures (or structs) that you want to package up in a library to make available to developers programming in C++ (or any other unmanaged language), these structs should not contain any instance methods. The same restriction applies to static methods in structs. If you want to include instance or static methods, you should convert your struct into a class. Additionally, structs cannot contain private fields, and all public fields must be C# primitive types, conforming value types, or strings.

WinRT also imposes some other restrictions on C# classes and structs if you want to make them available to native applications. Chapter 12 provides more information.

# Summary

In this chapter, you saw how to create and use enumerations and structures. You learned some of the similarities and differences between a structure and a class, and you saw how to define constructors to initialize the fields in a structure. You also saw how to represent a structure as a string by overriding the ToString method.

+   If you want to continue to the next chapter, keep Visual Studio 2015 running and turn to Chapter 10, “Using arrays.”

+   If you want to exit Visual Studio 2015 now, on the File menu, click Exit. If you see a Save dialog box, click Yes and save the project.

# Quick reference