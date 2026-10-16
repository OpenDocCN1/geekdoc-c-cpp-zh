
Several places. The many improvements have been made possible by a new compiler engine code named Roslyn.

> NOTE Roslyn is covered in Chapter 18, “.NET Compiler Platform.”

The full .NET Framework is not the only .NET Framework that was in use in recent years. Some scenarios required smaller frameworks. In 2007, the first version of Microsoft Silverlight was released (code named WPF/E, WPF Everywhere). Silverlight was a web browser plug-in that allowed dynamic content. The first version of Silverlight supported programming only via JavaScript. The second version included a subset of the .NET Framework. Of course, server-side libraries were not needed because Silverlight was always running on the client, but the Framework shipped with Silverlight also removed classes and methods from the core features to make it lightweight and portable to other platforms. The last version of Silverlight for the desktop (version 5) was released in December 2011. Silverlight had also been used for programming for the Windows Phone. Silverlight 8.1 made it into Windows Phone 8.1, but this version of Silverlight is also different from the version on the desktop.

On the Windows desktop, where there is such a huge framework with .NET and the need for faster and faster development cadences, big changes were also required. In a world of DevOps where developers and operations work together or are even the same people to bring applications and new features continuously to the user, there’s a need to have new features available in a fast way. Creating new features or making bug fixes is a not-so-easy task with a huge framework and many dependencies.

With several smaller .NET Frameworks available (e.g. Silverlight, Silverlight for the Windows Phone), it became important to share code between the desktop version of .NET and a smaller version. A technology to share code between different .NET versions is the portable library. Over time, with many different .NET Frameworks and versions, the management of the portable library has become a nightmare.

With all these issues, a new version of .NET is a necessity. (Yes, it’s really a requirement to solve these issues.) The new version of the Framework is invented with the name .NET Core. .NET Core is smaller with modular NuGet packages, has a runtime that’s distributed with every application, is open source, and is available not only for the desktop version of Windows but also for many different Windows devices, as well as for Linux and OS X.

For creating web applications, ASP.NET Core 1.0 is a complete rewrite of ASP.NET. This release is not completely backward compatible to older versions and requires some changes to existing ASP.NET MVC code (with ASP.NET MVC 6). However, it also has a lot of advantages when compared with the older versions, such as a lower overhead with every network request—which results in better performance—and it can also run on Linux. ASP.NET Web Forms is not part of this release because ASP.NET Web Forms was not designed for best performance; it was designed for developer friendliness based on patterns known by Windows Forms application developers.

Of course, not all applications can be changed easily to make use of .NET Core. That’s why the huge framework received improvements as well—even if those improvements are not completed in as fast a pace as .NET Core. The new version of the full .NET Framework is 4.6. Small updates for ASP.NET Web Forms are available on the full .NET stack.

> **NOTE** Roslyn is covered in Chapter 18. The changes to the C# language are covered in all the language chapters in Part I—for example, read-only properties are in Chapter 33, “Objects and Types”; the `nameof` operator and null propagation are in Chapter 8, “Operators and Casts”; string interpolation is in Chapter 10, “Strings and Regular Expressions”; and exception filters are in Chapter 14, “Errors and Exceptions.”
> 
> Where possible, .NET Core is used in this book. You can read more information about .NET Core and NuGet packages later in this chapter.

## Choosing Technologies and Going Forward

When you know the reason for competing technologies within the Framework, it’s easier to select a technology to use for programming applications. For example, if you’re creating new Windows applications it’s not a good idea to bet on Windows Forms. Instead, you should use an XAML-based technology, such as Windows apps or Windows desktop applications using WPF.

If you’re creating web applications, a safe bet is to use ASP.NET Core with ASP.NET MVC 6. Making this choice rules out using ASP.NET Web Forms. If you’re accessing a database, you should use Entity Framework rather than LINQ to SQL, and you should opt for the Managed Extensibility Framework instead of System.AddIn.

Legacy applications still use Windows Forms and ASP.NET Web Forms and some other older technologies. It doesn’t make sense to change existing applications just to use new technologies. There must be a huge advantage to making the change—for example, when maintenance of the code is already a nightmare and a lot of refactoring is needed to change to faster release cycles that are being demanded by customers, or when using a new technology allows for reducing the coding time for updates. Depending on the type of legacy application, it might not be worthwhile to switch to a new technology. You can allow the application to still be based on older technologies because Windows Forms and ASP.NET Web Forms will still be supported for many years to come.

The content of this book is based on the newer technologies to show what’s best for creating new applications. In case you still need to maintain legacy applications, you can refer to older editions of this book, which cover ASP.NET Web Forms, Windows Forms, `System.AddIn`, and other legacy technologies that are still part of and available with the .NET Framework.

## .NET 2015

.NET 2015 is an umbrella term for all the .NET technologies. [Figure 1.1](#figure-1-1) gives an overall picture of these technologies. The left side represents the .NET Framework 4.6 technologies such as WPF and ASP.NET 4. ASP.NET Core 1.0 can run on .NET Framework 4.6 as well, as you can see in this figure. The right side represents the new .NET Core technologies. Both ASP.NET Core 1.0 and the Universal Windows Platform (UWP) run on .NET Core. You can also create console applications that run on .NET Core.

![](img/3d365b72b289213a91ade7eb366b8f35_58_0.png)

**Figure 1.1**

A part of .NET Core is a new runtime: the CoreCLR. This runtime is used from ASP.NET Core 1.0. Instead of using the CoreCLR runtime, .NET can also be compiled to native code. The UWP automatically makes use of this feature; these .NET applications are compiled to native code before being offered from the Windows Store. You can also compile other .NET Core applications—and the applications running on Linux—to native code.

In the lower part of [Figure 1.1](#figure-1-1), you can see there’s also some sharing going on between .NET Framework 4.6 and .NET Core. *Runtime components*, such as the code for the garbage collector and the RyuJIT (this is a new JIT compiler to compile IL code to native code) are shared. The garbage collector is used by CLR, CoreCLR, and .NET Native. The RyuJIT just-in-time compiler is used by CLR and CoreCLR.

| Namespace | Description |
|---|---|
| System.Collections | This is the root namespace for collections. Collections are also found within sub-namespaces such as `System.Collections.Concurrent` and `System.Collections.Generic`. |
| System.Data | This is the namespace for accessing databases. `System.Data.SqlClient` contains classes to access the SQL Server. |
| System.Diagnostics | This is the root namespace for diagnostics information, such as event logging and tracing (in the namespace `System.Diagnostics.Tracing`). |
| System.Globalization | This is the namespace that contains classes for globalization and localization of applications. |
| System.IO | This is the namespace for file I/O, which are classes to access files and directories. Readers, writers, and streams are here. |
| System.Net | This is the namespace for core networking, such as accessing DNS servers and creating sockets with `System.Net.Sockets`. |
| System.Threading | This is the root namespace for threads and tasks. Tasks are defined within `System.Threading.Tasks`. |
| System.Web | This is the root namespace for ASP.NET. Below this namespace, many sub-namespaces are defined, such as `System.Web.UI`, `System.Web.UI.WebControls`, and `System.Web.Hosting`. |
| System.Windows | This is the root namespace for Windows desktop applications with WPF. Example subnamespaces are `System.Windows.Shapes`, `System.Windows.Data`, and `System.Windows.Documents`. |

> **NOTE** Some of the new .NET classes use namespaces that start with the name `Microsoft` instead of `System`, like `Microsoft.Data.Entity` for the Entity Framework and `Microsoft.Extensions.DependencyInjection` for the new dependency injection framework.

## .NET Core 1.0

.NET Core 1.0 is the new .NET that is used by all new technologies and
