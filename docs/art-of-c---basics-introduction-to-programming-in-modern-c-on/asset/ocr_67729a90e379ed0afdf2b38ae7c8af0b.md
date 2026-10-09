In this example, the single-line top-level statement is a “method call”, Console.WriteLine(“Hello World!!!”). (The pair of parentheses ( ( and ) ) is used for the “method invocation”. In this case, WriteLine is the method.)

The statement appears to include two components separated by a dot (.), namely Console and WriteLine(“Hello World!!!”). in fact, this statement is a shorthand for

```
System.Console.WriteLine("Hello World!!!");
```

This includes three components. The first part, System, is called a “namespace”. The System namespace is from the standard .NET library, and it includes many different types and what not. The Console class happens to be one of them. The namespaces are used to reduce the chances of name collisions across different C# programs (e.g., executables and libraries).

In order be able to use the Console class, its name should be qualified with the namespace, as in the example: System.Console. Alternatively, one can use the keyword using to “introduce” (all) the names from the given namespace into the program, or more precisely to the specific source code file. For example,

```
using System;
Console.WriteLine("Hello World!!!");
```

In this example, by using the using declaration, we can refer to the Console class without having to fully qualify its name. Note, however, that certain system namespaces are treated as special, as of C# 10.0, including the System namespace. They need not be explicitly imported using the using declaration. As in the original example code, we can just omit the using System declaration. This is known as the “implicit using”, “implicit global using”, or “implicit namespace import”, in C# 10.0. This is an “opt-in” feature, and we will discuss this further a bit later.