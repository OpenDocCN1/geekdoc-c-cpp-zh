AST enables the DLR to dynamically generate code (expression trees) in place of Intermediate Language (IL), which the CLR executes at runtime.

+   - **Call Site Caching:** Enables DLR to store all the information of the variables, such as their data types, as well as of the operations performed on these variables. The call site caching also enables the DLR to check whether such operations have been performed previously and if so, the DLR retrieves all the information about the variables and then reuses that information whenever required. The place where DLR stores these values is called call site.
+   - **Dynamic Object Interoperability:** Enables the DLR to provide a set of classes and interfaces that represent dynamic objects and operations. The authors of dynamic libraries use these classes and interfaces to create dynamic libraries, which can be used with the static and dynamic type languages.

![](bbox=[0.213, 0.291, 0.275, 0.318])

You learn more about LINQ in Chapter 6, LINQ in C# 2010.

Fig.C#-3.1 shows the architecture of DLR, which shows how the DLR integrates the dynamic languages with the CLR:

![](bbox=[0.354, 0.362, 0.671, 0.515])

Fig.C#-3.1

In Fig.C#-3.1, there are several languages at the topmost level in the architecture, such as IronRuby, IronPython, C#, VB.NET, and others in which you can write the source code. There are also various technologies, such as Microsoft .NET, Microsoft Silverlight, and Microsoft Office. DLR allows data to be accessed amongst various technologies and languages with the help of appropriate binders.

**Binders** allow DLR to communicate with .NET Framework and other services, such as Silverlight and MS Office. They specify how a particular operation can be performed at the call site. Call sites refer to the area in the code where logical and mathematical operations, such as **a + b** or **a/b()**, are performed on dynamic objects.

![](bbox=[0.213, 0.653, 0.275, 0.684])

You learn more about Silverlight in Chapter 11, Silverlight 4.0, of the ASP.NET 4.0 section.

Let’s now learn about the dynamic types.

# Working With the Dynamic Type

With the release of .NET 4.0, a new reference data type is introduced, called **dynamic**. When you use the dynamic keyword with any member variable or member function, the compiler checks the type of that variable or function at runtime instead of compile time.

The syntax for declaring a variable as **dynamic** is as follows:

```
dynamic x;
```

There is one more data type, var, in C# that is similar to the dynamic data type. The only difference between **dynamic** and var is that the types of the variables declared as **dynamic** can be changed dynamically as compiler checks them only at runtime. On the other hand, if you once declare a variable as var, you cannot change its type throughout the execution of program.