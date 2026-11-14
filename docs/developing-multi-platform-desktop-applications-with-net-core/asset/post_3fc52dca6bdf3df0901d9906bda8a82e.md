
application is very complex and requires a learning curve for being used properly. A user will be much more inclined to learn the use of a particular software if he knows that knowledge will be pertinent on several other platforms.

There is another reason for choosing multiplatform application: the positive psychological impact on your customers, if you can provide a software solution whatever the system they use. The multiplatform distribution of your software implies a good technical mastering at every step of the development process and indicates you are not dependent on one OS.

Multiplatform development offers you (and your company) the possibility to not be captive of a particular OS often subject to drastic changes, which can even challenge the validity of the application you are developing.

You have to keep in mind that achieving such a control over the software you develop comes with the price of a bigger effort during the development phase (especially if your project requires the use of native functions API (in the other cases .NET Core 3 provides you a solid and adaptative way for the implementation of the project)).

.NET Core 3.0

## Chapter 2. PRESENTATION OF .NET CORE 3

.NET Core is a product born in 2015 (actually in beta since 2014).

It has been defined from the classical .NET Framework. Many technical options chosen during the .NET Framework evolution have defined the need of new paradigms.

We will see how these evolutions of the .NET Framework took place and in which context the need of the new framework: .NET Core has appeared obvious.

## 2.1 LITTLE HISTORIC OF THE MICROSOFT .NET FRAMEWORK

The first .NET Framework was delivered in 2002 and was a proprietary system (a black-box) from Microsoft. It was a response from the Redmond editor to the Java framework gaining in popularity at this time. As the Java framework, the .NET Framework uses a virtual machine for the execution of the program.

With the .NET Framework the source language was no longer compiled to machine code but to an MSIL (Microsoft Intermediate Language), this language is compiled at runtime by the CLR (Common Language Runtime) to machine code, executed in the .NET Framework virtual machine.

This runtime translates in real time each portion of the code which has to be executed through native code for the platform.

![](img/3d310cc066dda6e2dfa67a650614076f_22_0.png)

Added to this compilation capability the CLR provides many services for the code generated, here is a non-exhaustive list of these basic features provided:

- Base Class Library (BCL).
- Threading Model.
- Type checker.
- Exception manager.
- Garbage Collector.
- MSIL to Native code compiler.
- Class Loader.

Shortly after Microsoft released many subsets of the .NET Framework adapted to each field of application the company encountered: .NET Compact Framework, Silverlight, Windows Phone ...

Each of these frameworks incorporates its own set of specific functionalities at the framework level and thus has become incompatible between them (for most of the code).

Due to their specific evolutions (vertical) of their APIs the development of applications targeting multiple types of platforms was more and more costly in terms of time and resources due to the vertical evolutions of each framework.

It can easily be explained by the fact that initially there was no will to share code between frameworks because these frameworks were dedicated to their specific field of applications and platform context.

But nowadays the cross-platform development becomes a very common requirement for many projects. Many applications blur the lines between vertical .NET frameworks: often a web application uses Windows dedicated functionality, desktop or phone applications use web backends (Web Services or Web APIs) and so forth...

That is in that context that .NET Core and .NET Standard have been planned and defined as a new subset of the .NET Frameworks.

Here is a little schema explaining the link between .NET Framework and .NET Core.

![](img/3d310cc066dda6e2dfa67a650614076f_24_0.png)

(source Microsoft)

The .NET Standard can be used with the .NET Framework and .NET Core, this library format provides an amazing portability whatever the framework you intend to use with it.

## 2.2 WHY .NET CORE?

The complexity implied by the use of multiple frameworks, each specializes in their own field, becomes the pitfall of most multifaceted platform development. As these kinds of development are turning into increasingly commonplace the need of a new framework appears.

That's in that context that appears the need of a minimal framework where all the specifics for each platform and features will be integrated through NuGet package instead of being integrated inside the core framework (like it was the case previously for the .NET Framework).

Furthermore, the .NET Framework is a part of the Windows system, that's not the case for .NET Core 3 which can be distributed with the application in a self-contained manner and is self-sufficient on its own.

The well thought architecture of the .NET Core provides many benefits for its exploitation in a production environment as you can see _(figure 1)_ compared to the classical .NET Framework (which is Windows dependent).

| | .NET framework | .NET Core 3 |
|---|---|---|
| Windows Update | Yes | No |
| Deploy Runtime | Depends | Yes |
| Side by Side install | No | Yes |

_(figure 1)_
_(Source Microsoft)_

A key point in the .NET Core is the use of a dedicated package manager format: NuGet.

The NuGet packaging system is integrated in Visual Studio 2019 and is like APT for Debian, NPM for Node.js or pip for Python. NuGet allows the availability of every and each library by encapsulating binaries and their dependencies inside a single file. This file (.nupkg extension) is a ZIP archive which contains a manifest with all the associated dependencies and the targeted frameworks information.

Thus, a NuGet package can implement a complete feature on its own for a multiplatform use.

## 2.3 NEW FEATURES

Like its predecessors the .NET Core 3 is open source and cross-platform. With this implementation, Microsoft has included the support of C# 8, a major release of the C# language. But this is not the only addition to the .NET Core Microsoft has done in this version.

The two following schemas illustrate the job done by Microsoft for the third release of their new iconic framework: .NET Core 3. We can see that it is a major release compared to the .NET Core 2 which was basically an update of the first version designed for running Web applications and services for cross-platform environments.

.NET Core 2:

![](img/3d310cc066dda6e2dfa67a650614076f_26_0.png)

.NET Core 3:

![](img/3d310cc066dda6e2dfa67a650614076f_27_0.png)

(source Microsoft)

As you can see .NET Core 3 not only targets web server platform but also gains many new functionalities; such as AI and IoT.

But unfortunately, the desktop development is a Windows-only functionality (it relies on WinFX, Windows dependent).

By proposing these new functionalities Microsoft fully validates the basic concept underneath .NET Core: the modularity is included only in specialized packages (and not integrated in the framework as it was the case in .NET Framework).

A major addition to .NET Core 3 is the support of C# 8 new functionalities:

- Default interface member.
- Nullable reference types.
- Switch expressions.
- Property patterns.
- Tuples patterns.
- Static local function.
- Nullable reference types.
- Asynchronous streams.
- Floating-point API improvements and compliance with IEEE standard.
- Parsing and format fixes.
- New math API (BitIncrement/BitDecrement which matches with nextUp nextDown IEEE operations).

### Other features included in .NET Core 3:

- APIs to access performance-oriented CPU instructions, such as the SIMD. These instructions can improve performance.
- A fast in-box JSON Writer and JSON document.
- GPIO (general purpose input/output) support for the Raspberry Pi computer.
- Improved local dotnet tools. Local tools are associated with a location on-disk, enabling per-project and per-repository tools.
- Assembly unloadability, which is part of the AssemblyLoaderContext. The capability enables a loader context to be unloaded, with memory released for instantiated types, static fields, and for the assembly itself. An application should be able to load and unload assemblies via this mechanism without a memory leak.
- For Visual Studio support, the C# beta features the addition of Windows Presentation Foundation (WPF) and Windows Forms templates to the New Project Dialog, to make it easier to start an application without using the command line.
- MSIX application package format deployment, for deploying .NET Core 3 desktop apps to Windows 10.
