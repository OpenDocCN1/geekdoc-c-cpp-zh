
## The .NET Framework and .NET Core

To describe how .NET works, figure 1-3 presents the main components of the .NET Framework and .NET Core. This shows that .NET Core works similarly to the .NET Framework. In fact, most of the code and techniques that are presented in this book work the same regardless of whether you use the .NET Framework or .NET Core.

The main difference between these platforms is that the .NET Framework is older and only supports Windows. On the other hand, .NET Core is newer and cross-platform. As a result, .NET Core can run on Windows, macOS, and Linux. Currently, Microsoft plans to end development of .NET Framework at version 4.8. As a result, .NET Core is the future of .NET development.

In fact, the next version of .NET Core will be called .NET 5 (no Core in the name). It combines the best features of .NET Framework and .NET Core 3.1. As a result, it provides an easy migration path for .NET Framework applications, and it provides a foundation for future development of the .NET platform.

Both the .NET Framework and .NET Core provide a set of class libraries. These class libraries consist of segments of pre-written code called classes that provide many of the functions that you need for developing .NET applications. For instance, the Windows Forms classes are used for developing Windows Forms applications. The ASP.NET and ASP.NET Core classes are used for developing Web Forms applications. The EF and EF Core classes are used for developing applications that access databases. And other classes let you manage security, access files, and perform many other functions.

The .NET Framework and .NET Core also provide a common infrastructure that application programs written in a .NET language such as C# can use to run on various operating systems and hardware platforms. This infrastructure includes the Common Language Runtime, the .NET languages, and the compilers for those languages.

The Common Language Runtime (CLR) provides the services that are needed for executing any application that’s developed with one of the .NET languages. This is possible because all of the .NET languages compile to a common intermediate language, which you’ll learn more about in figure 1-5. The CLR also provides the Common Type System that defines the data types that are used by all .NET languages. Because all of the .NET applications are managed by the CLR, they are sometimes referred to as managed applications.

If you’re new to programming, you might not understand this diagram completely, but that’s all right. For now, all you need to understand is the general structure of the .NET Framework and .NET Core and the terms that have been presented so far. As you progress through this book, this diagram will make more sense, and you will become more familiar with each of the terms.

![](img/844f608d10a44654833ea5efc8a2e7a7_32_0.png)

### Description

- Windows Forms applications do not access the operating system or computer hardware directly. Instead, they use services of the .NET Framework or .NET Core, which in turn access the operating system and hardware.
- The .NET Framework and .NET Core provide *class libraries* that contain pre-written code known as *classes* that are available to all of the .NET programming languages. These class libraries consist of thousands of classes, but you can create simple .NET applications once you learn how to use just a few of them.
- The .NET Framework and .NET Core use a common infrastructure that includes the *Common Language Runtime (CLR)*, the languages, and the compilers.
- The CLR manages the execution of .NET programs by coordinating essential functions such as memory management, code execution, security, and other services. Because .NET applications are managed by the CLR, they are called *managed applications*.
- The *Common Type System* is a component of the CLR that ensures that all .NET applications use the same basic data types no matter what programming languages are used to develop the applications.

## The Visual Studio IDE

Figure 1-4 shows the Visual Studio IDE. By now, you know that Visual Studio supports the languages presented in figure 1-2. In addition, you can use Visual Studio to work with the .NET Framework and .NET Core.

Visual Studio includes a drag-and-drop designer that developers can use to design the user interface for Windows Forms applications. This designer generates the C# code that displays the user interface, which makes the tough task of developing the user interface much easier.

Visual Studio also includes an editor that can be used to work with any of the four languages presented in figure 1-2. This editor contains many features that make it easy to enter and edit the code for an application.

In a moment, this chapter takes a quick tour of Visual Studio, including a glimpse of the Windows Form Designer and the Code Editor. But first, it’s important that you understand what happens when you use Visual Studio to compile and run an application.

![](img/844f608d10a44654833ea5efc8a2e7a7_34_0.png)

### Description

- Visual Studio includes drag-and-drop designers that can be used to develop Windows Forms applications and Web Forms applications.
- Visual Studio includes a code editor that can be used to work with many languages, including the .NET languages presented in figure 1-2.

## How a C# application is compiled and run

Figure 1-5 shows how a C# application is compiled and run. To start, you use Visual Studio to create a project, which is made up of source files that contain C# statements. A project may also contain other types of files such as sound, image, or text files.

After you enter the C# code for a project, you use the C# compiler, which is installed when you install Visual Studio, to build (or compile) your C# source code into Microsoft Intermediate Language (MSIL). For short, this can be referred to as Intermediate Language (IL).

At this point, the Intermediate Language is stored on disk in a file that's called an assembly. In addition to the IL, the assembly includes references to the classes that the application requires. The assembly can then be run on any computer that has the Common Language Runtime installed on it. When the assembly is run, the CLR converts the Intermediate Language to native code that can be run by the operating system.

If you have developed applications with other languages, this process should be familiar to you. If this is your first language, though, you won't really understand this process until you develop your first applications. Until then, just try to focus on the terms and concepts.

Incidentally, a solution is a container that can hold one or more projects. Although a solution can contain more than one project, the solution for a simple application usually contains just one project. In that case, the solution and the project are essentially the same thing.

![](img/844f608d10a44654833ea5efc8a2e7a7_36_0.png)

### Operation

- The programmer uses Visual Studio to create a *project*, which includes C# *source files*. In some cases, a project will also contain other types of files such as images, sound, or text files.
- The C# *compiler* compiles (translates) the C# source code for a project into *Microsoft Intermediate Language (MSIL)*, or just *Intermediate Language (IL)*. This language is stored on disk in an *assembly* that also contains references to the required classes. An assembly is an executable file that has an .exe or .dll extension.
- The assembly is run by .NET’s Common Language Runtime. The CLR manages all aspects of how the assembly is run, including converting the Intermediate Language to native code that can be run by the operating system, managing memory for the assembly, and enforcing security.

### About projects and solutions

- A *solution* is a container that can hold one or more projects.
