
# 10
Enhancements to the .NET Core Framework

Changes in a release of a new .NET Framework version may affect the core run-time engine (including Common Language Run-time and the Common Type System), the Base Class Library (BCL), Framework services (such as ASP.NET, WPF, WCF and so on), and connected tools and utilities.

While in .NET 3.0, 3.5, and 3.5 SP1 targeted Framework services and part the BCL, the .NET 4 release touched the Common Language Run-time (CLR) significantly and added brand new services (and related BCL types) to shift toward new programming paradigms. This chapter and the following ones (closing with Chapter 21) detail all the new technologies, paradigms, and services that are in .NET 4.

This chapter covers fundamental enhancements and improvements to the core .NET Framework. You can use them in your managed applications independently of whether you are using Windows Forms, ASP.NET, Windows Presentation Foundation (WPF), Windows Workflow Foundation (WF), Windows Communication Foundation (WCF), Silverlight, Azure, SQL Server, SharePoint, or whatever technology you use with .NET.

Here's what you'll discover in this chapter:

- Changes in the CLR — This .NET framework version got a new CLR that has many enhancements. Now a native component is able to host more CLR versions side-by-side. As an important import to Object Model (COM) interoperability and version resilience, the CLR can handle type equivalence. Programming language changes in this version are primarily about dynamic capabilities, based on a new component called Dynamic Language Run-time (DLR).

- Parallel computing — Using the Task Parallel Library (TPL) and Parallel Language Integrated Query (LINQ), you can turn your sequential algorithms into concurrent without having to write tremendous plumbing code for threading infrastructure.

When you can split your algorithm into tasks that can run parallel, TPL undertakes the challenge to execute them concurrently, while entirely hiding low-level constructs (such as threads, semaphores, locks, and so on) from you.

- Code contracts allows you to execute pre, preconditions, and object invariants for run-time checking, static analysis, and documentation.
- Managed Extensibility Framework (MEF) — .NET 4 contains a new technology that allows you to shift your statically coupled applications into dynamically composed ones. With MEF, you have a flexible plug-in system where the composition is based on declarative syntax, practically free from any coupling code.

# CHANGES IN COMMON LANGUAGE RUN-TIME

Consider the soul of the .NET Framework is the CLR. At the beginning of the .NET 1.0, .NET 1.1, and .NET 2.0 had their own CLRs. The .NET 3.0, .NET 3.5, and .NET 3.5 SP1 used CLR 2.0, because these versions were about extending the BCL and architecture services (like WF, WCF, WPF, and Cardspace) to the framework.

After some five years, .NET 4 ships with a new CLR, consistently having the version number 4.0. In this section, you will learn the important core features of CLR 4.0:

- Now a native process is able to help more CLR versions side-by-side.
- DLR is an organic part of the .NET Framework.

A type equivalence feature implemented in the CLR helps deploying applications accessing COM objects without deploying Primary Interop Assemblies (PIAs).

> This section contains sample code using the C# 4.0 syntax, which may feature the dynamic binding, but also named and optional parameters. You may not be familiar with these syntax elements. Chapter 25 gives you a detailed overview of them and many useful snippets.

You can go on reading this chapter without being aware of these constructs, because they are intuitive enough. If you find something in the source code where you suspect a syntax error or a typo, note that it's probably not an error but rather the use of C# 4.0.

# In-Process Side-By-Side Execution

The CLR development team at Microsoft invested a lot of resources to provide compatibility among CLRs, so that each new version would be highly compatible with the old versions. Theoretically, each version of the .NET Framework could have been developed so that it was completely compatible with older versions, and a concrete CLR could run applications developed with any of the preceding versions. In this way, .NET Framework versions could be seamlessly updated to a newer one so that only one (the latest) version is installed on a computer, while being able to run the applications originally targeting an old framework version.

# Understanding Side-By-Side Execution

This approach has serious limitations. Aiming at full compatibility would mean that any design issues, mistakes, or paradigm decisions should show in the framework forever. This simply does not work, it is a very strict limit for innovations! Full compatibility means not only that all source code will compile with all new framework versions, but also documented and undocumented behaviors remain the same. It would mean, even if you have multiple CPU cores in them, any existing framework implementation would be allowed to leverage on this capability implicitly, because of backward compatibility issues, as .NET Framework 1.0 BCL was designed with single CPU core in mind.

The CLR avoided the "one-CLR rules" and designed the .NET Framework from the very first version with the capability to run separate versions side-by-side on the same computer. This is a good approach from the point of view that it prevents the "innovation bottleneck.". However, the side-by-side scenario avoids an important question of which CLR version an application or a component should use among the ones installed on the machine.

# Issues Before Side-By-Side Execution

The CLR avoided the "one-CLR rules" and designed the .NET Framework from the very first version with the capability to run separate versions side-by-side on the same computer. This is a good approach from the point of view that it prevents the "innovation bottleneck.". However, the side-by-side scenario avoids an important question of which CLR version an application or a component should use among the ones installed on the machine.

# Issues Before CLR

The CLR avoided the "one-CLR rules" and designed the .NET Framework from the very first version with the capability to run separate versions side-by-side on the same computer. This is a good approach from the point of view that it prevents the "innovation bottleneck.". However, the side-by-side scenario avoids an important question of which CLR version an application or a component should use among the ones installed on the machine.

# Changes in CLR Hosting

The CLR avoided the "one-CLR rules" and designed the .NET Framework from the very first version with the capability to run separate versions side-by-side on the same computer. This is a good approach from the point of view that it prevents the "innovation bottleneck.". However, the side-by-side scenario avoids an important question of which CLR version an application or a component should use among the ones installed on the machine.

# DLR Integration

Most developers are familiar with the fact that types and operations are strictly checked during the compilation. The compiler generates Microsoft Intermediate Language (MSIL) code that explicitly carries out those operations by invoking methods.

There are programming languages that behave adversely — for example, the dynamic languages. The compiler makes only a few checks upon types. The majority of them are postponed to the execution of the corresponding operation. In addition to the dynamic languages, there are script languages and object models (for example, COM objects over Microsoft Office functionality, the DTE object model in Visual Studio, the HTML DOM in Internet Explorer, and so on) that also check operations at run-time.

For a long time, NET was unable to handle the interoperability between static and dynamic languages in a straightforward and easy-to-use way. It simply did not fit into the compilation approach, and the CLR itself designed entirely with a static type system in mind.
