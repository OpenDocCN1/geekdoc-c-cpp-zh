v) .NET Framework is a managed environment. The common language runtime monitors the execution of .NET applications and provides essential services. It manages memory, handles exceptions, ensures that applications work properly.

vi) Language interoperability is one goal of .NET. .NET languages share a common runtime (the common language runtime, a common class library), the Framework Class Library (FCL), a common component model and common types.

# vii) Common Language Runtime (CLR)

+   - .Net Framework provides runtime environment called Common Language Runtime (CLR).It provides an environment to run all the .Net Programs. The code which runs under the CLR is called as Managed Code. Programmers need not to worry on managing the memory if the programs are running under the CLR as it provides memory management and thread management.
+   - Programmatically, when the program needs memory, CLR allocates the memory for scope and de-allocates the memory if the scope is completed.
+   - Language Compilers (e.g. C#, VB.Net, J#) will convert the Code/Program to Microsoft Intermediate Language (MSIL) intern this will be converted to Native Code by CLR as shown in below Fig. 1.1.2.

![](bbox=[0.22, 0.58, 0.92, 0.87])

+   - Types of JIT compilers :
+     JIT Compiler (Just In Time) compiler is a part of CLR (Common Language Runtime). It is responsible for converting MSIL (binary format) to native code. It does this just before execution. If any earlier compiled code already which already exists, if needed, is used here.