![](bbox=[0.83, 0.12, 0.94, 0.17])

# What Is a Dynamic Language?

In a language such as C#, which is statically typed, the compiler attempts to prove type safety, and, if it cannot, generates an error. In a dynamic language, this attempt at proving type safety is not made. In addition, most dynamic languages perform more complex type operations, such as determining the correct method overload, at runtime whereas C# performs this type of resolution at compile time.

In effect, what would normally be done at compile time in a statically typed language is done at runtime. This includes the idea that you can generate code at runtime (using what is commonly called an eval or repl loop) that can modify the state of running objects. As a result, dynamic languages enable a great deal of freedom and are most frequently used as scripting languages.

Some common dynamic languages are Jscript, JavaScript, Python, IronPython, Ruby, and IronRuby.

Just as code written for the .NET Framework is called managed code, the resulting application is called a managed application. When a managed application runs, it automatically hosts the common language runtime it was built against. Not only does the .NET Framework provide a number of different runtime hosts, it also provides the tools necessary to write your own. Because of this capability, unmanaged applications such as Internet Information Services (IIS) and Microsoft SQL Server can host their own copy of the common language runtime, enabling them to take advantage of both managed and unmanaged features.

Figure 1.1 shows how the different components of the .NET Framework relate to your application, the overall operating system, and unmanaged applications.

# The Common Language Runtime

The common language runtime (CLR) is the core of the .NET Framework and provides a unified type system and a managed runtime environment. Together they form a foundation for developing and executing applications that are language- and platform-independent and help eliminate, or at least reduce, many common programming errors.

# Common Type System

The unified type system, called the common type system (CTS), enables all .NET languages to share the same type definitions, enabling those types to be manipulated in a consistent manner. This helps ensure correctly written applications by

GO TO ▶
We discuss types a bit later in this hour.
Hour 2, "Understanding C# types," provides more detailed information.