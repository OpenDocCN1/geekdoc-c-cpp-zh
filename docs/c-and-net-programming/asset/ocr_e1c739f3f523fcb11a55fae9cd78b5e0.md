# ## Two Marks Questions with Answers

**Q.1** How many languages are supported by .NET at present time ?

**Ans. :** When .NET was introduced first time, it supports many languages like VB.NET,C#,COBOL and Perl etc. At present time it supports almost 44 languages.

**Q.2** What is CTS ?

**Ans. :** CTS stands for Common Type System. It has a set of rules which state how a data type should be declared, defined and used in the program. It describes the data types that are to be used in the application.

We can design our own classes and values by following the rules that are present in the CTS. The rules are made so that the data type declared using a programming language can be called by an application that is developed using a different language.

**Q.3** What is MSIL ?

**Ans. :** MSIL stands for Microsoft Intermediate Language.

MSIL provides instructions for calling methods, initializing and storing values, operations such as memory handling, exception handling and so on. All .Net codes are first compiled to IL.

**Q.4** How is a Managed code executed ?

**Ans. :** Follow these steps while executing a Managed code :

+   - Choosing a language compiler depending on the language in which the code is written.
+   - Converting the above code into Intermediate language by its own compiler.
+   - The IL is then targeted to CLR which converts the code into native code with the help of JIT.
+   - Execution of Native code.

**Q.5** What is the difference between managed and unmanaged code ?

**Ans. :**

| Managed code | Unmanaged code |
| --- | --- |
| Managed code is managed by CLR | Any code that is not managed by CLR |
| .NET framework is necessary to execute managed code | Independent of .NET framework |
| CLR manages memory management through garbage collection | Own runtime environment for compilation and execution |