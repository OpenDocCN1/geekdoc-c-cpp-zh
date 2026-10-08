When you can split your algorithm into tasks that can run parallel, TPL undertakes the challenge to execute them concurrently, while entirely hiding low-level constructs (such as threads, semaphores, locks, and so on) from you.

+   - Code contracts allows you to execute preconst, preconditions, and object invariants for run-time checking, static analysis, and documentation.
- Managed Extensibility Framework (MEF) — .NET 4 contains a new technology that allows you to shift your statically fixpled applications into dynamically composed ones. With MEF, you have a flexible plug-in system where the composition is based on declarative syntax, practically free from any coupling code.

# CHANGES IN COMMON LANGUAGE RUN-TIME

Admitted the soul of the .NET Framework is the CLR. At the beginning of the .NET 1.0, .NET 1.1, and .NET 2.0 had their own CLRs. The .NET 3.0, .NET 3.5, and .NET 3.5 SPI Framework used CLR 2.0, because these versions were about extending the BCL and architecture services (like WF, WCF, WPF, and Cardspace) to the framework.

After some five years, .NET 4 ships with a new CLR, consistently having the version number 4.0. In this section, you will learn the important core features of CLR 4.0:

+   - Now a native process is able to help more CLR versions side-by-side.
- DLR is an organic part of the .NET Framework.

A type equivalence feature implemented in the CLR helps deploying applications accessing COM objects without deploying Primary Interop Assemblies (PIAs).

> This section contains sample code using the C# 4.0 syntax, which may feature the dynamic binding, but also named and optional parameters. You may not be familiar with these syntax elements. Chapter 25 gives you a detailed overview of them many useful snippets.

You can go on reading this chapter without being aware of these constructs, because they are intuitive enough. If you find something in the source code where you suspect a syntax error or a typo, note that it's probably not an error but rather the use of C# 4.0.

# In-Process Side-By-Side Execution

The CLR development team at Microsoft invested a lot of resources to provide compatibility among CLRs, so that each new version would be highly compatible with the old versions. Theoretically, each version of the .NET Framework could have been developed so that it was completely