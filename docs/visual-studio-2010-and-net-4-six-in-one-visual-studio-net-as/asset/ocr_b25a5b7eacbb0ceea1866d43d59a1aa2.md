# SUMMARY

.NET Framework 4.0 contains fundamental enhancements to the core functionality related to the preceding version. In this chapter, you learned about those features that you can use independently of whether you are using Windows Forms, ASP.NET, WPF, WF, WCF, Silverlight, or any other .NET technology.

After five years, .NET 4 ships with a new CLR that has important core improvements. In CLR 4.0, a native process is able to host more CLR versions side-by-side. .NET 4 supports deploying applications accessing COM objects without deploying APIs, and it is possible through a new CLR feature called type equivalence.

.NET 4 has a set of services that add dynamic programming capabilities to the CLR, and allow interoperation between .NET objects and dynamic languages. DLR dynamically allows languages like Python and Ruby to run on top of the CLR. DLR is also the base of the new features in C# and Visual Basic.

The many-core shift (using CPUs with multiple cores) has already happened. However, today, software is the weakest link, because most applications are designed to run sequentially. Microsoft provides a great technology in .NET 4 that efficiently targets issues coming from the use of multiple CPU cores. Instead of the sophistication in threading models, or automating parallelism, and having it from developers, use a declarative approach to TPL. It allows developers to explicitly declare that certain parts of their program can be executed in parallel. The platform takes care of the implementation.

Now, LINQ is also multi-core. PLINQ queries use all CPUs in your computer concurrently to execute in-memory queries that were previously carried out sequentially.

Modern software architecture uses the concept of contracts to describe responsibilities of components and communication through boundaries. The most frequently used .NET programming languages (such as C# and Visual Basic) do not give you type and interface definitions. Code contracts in .NET 4 provide a contract library to define preconditions, postconditions, and object invariants. Reflected tools allow you static code analysis, contract document generation, and instrumenting your code with run-time contract checks.

The MEF ships with .NET 4. This new technology helps you shift easily compiled applications into dynamically composed components. You can unify your components that export services offered to other parts, and sign the intention to use imported services provided by other parts or a host application. MEF uses the concept of a composition container that holds the matching among your parts in run-time. With MEF, you can easily implement scenarios where parts of your applications or services can be easily changed without following the "remove/reinstall" deployment pattern.

In Chapter 11, you will learn about the enhancements of the .NET Workflow Framework (WF 4.0), which is not just an updated version of WF 3.5, but has been totally redesigned and rewritten.