
# Chapter 24: The Common Language Infrastructure

whether the source languages using the library are CTS-compliant. It is called the Common Language Specification because it is intended to also encourage CLI languages to provide a means of creating interoperable libraries, or libraries that are accessible from other languages.

For example, it is perfectly reasonable for a language to provide support for an unsigned integer, such a type is not included as part of the CLS. Therefore, developers implementing a class library should not externally expose unsigned integers because doing so would cause the library to be less accessible from CLS-compliant source languages that do not support unsigned integers. Ideally, any libraries that are accessible from multiple languages should conform to the CLS. Note that the CLS is not concerned with types that are not externally exposed to the assembly.

Also note that it is possible to have the compiler issue a warning when you create an API that is not CLS-compliant. To accomplish this, you use the assembly attribute System.CLSCompliant and specify a value of true for the parameter.

# Metadata

In execution instructions, CIL code includes metadata about the types and files included in a program. The metadata includes the following items:

- A description of each type within a program or class library
- The manifest information containing data about the program itself, along with the libraries it depends on
- Custom attributes embedded in the code, providing additional information about the constructs that the attributes decorate

The metadata is not a cursory, nonessential add-on to the CIL, but rather represents a core component of the CLI implementation. It provides the representation and the behavior about a type and includes location information about which assembly contains a particular type definition. It plays a key role in saving data from the compiler and making it accessible at execution time to debuggers and the runtime. This data not only is available in the CIL code but also is accessible during machine code execution so that the runtime can continue to make any necessary type checks.

Metadata provides a mechanism for the runtime to handle a mixture of native and managed code execution. Also, it increases code and execution robustness because it smooths the migration from one library version to the next, replacing compile-time-defined binding with a load-time implementation.

All header information about a library and its dependencies is found in a portion of the metadata known as the manifest. As a result, the manifest portion of the metadata enables developers to determine a module's dependencies, including information about particular versions of the dependencies and signatures indicating who created the module. At execution time, the runtime uses the manifest to determine which libraries to load, whether the libraries or the main program has been tampered with, and whether assemblies are missing.

The metadata also contains custom attributes that may decorate the code. Attributes provide additional metadata about CLI instructions that are accessible via the program at execution time.

Metadata is available at execution time by a mechanism known as reflection. With reflection, it is possible to look up a type or its member at execution time and invoke that member or determine whether a construct is decorated with a particular attribute. This provides for late binding, in which the system determines which code to execute at execution time rather than at compile time. Reflection can even be used for generating documentation by iterating through metadata and copying it into a help document of some kind (see Chapter 18).

# .NET Native and Ahead of Time Compilation

The .NET Native feature creates a platform-specific executable. This is referred to as ahead of time (AOT) compilation.

.NET Native allows programmers to continue to code in C# while achieving native code performance and faster startup times by eliminating the JIT compile code. When .NET Native compiles an application, the .NET FCL is statically linked to the application; .NET Framework runtime components optimized for static pre-compilation are included as well. These specially built components are optimized for .NET Native and provide improved performance over the standard .NET runtime. The compilation step does not change your application in any way. You are free to use all the constructs and APIs of .NET, as well as depend on managed memory and memory cleanup, since .NET Native will include all components of the .NET Framework in your executable.

# Summary

This chapter described many new terms and acronyms that are important for understanding the context under which C# programs run. The preponderance of three-letter acronyms can be confusing, so Table 24.2 summarizes the terms and acronyms that are part of the CLI.

TABLE 24.2: Common C#-Acronyms

| Acronym | Definition | Description |
| --- | --- | --- |
| .NET | None | Microsoft's implementation of the entire CLI stack. Includes the CLR, CIL, and various languages, all of which are CLS-compliant. |
| BCL | Base Class Library | The portion of the CLI specification defines the collection, threading, console, and other base classes necessary to build virtually all programs. |
| C# | None | A programming language. Separate from the CLI standard is a C# Language Specification, also ratified by the ECMA and ISO standards bodies. |
| CIL (IL) | Common Intermediate Language | The language of the CLI specification defines the instructions for the code executable on implementations of the CLI. It is sometimes referred to as IL or Microsoft IL (MSIL) to distinguish from other intermediate languages. (To indicate that it is a standard broader than Microsoft, CIL is preferred over MSIL and even IL) |
| CLI | Common Language Infrastructure | The specification that defines the intermediate language, base classes, and behavioral characteristics that enable implementers to create Virtual Execution Systems and compilers in which source languages are interoperable on top of a common execution environment. |

# TABLE 24.2: Common C#-Related Acronyms (continued)

| Acronym | Definition | Description |
| --- | --- | --- |
| CLR | Common Language Runtime | Microsoft's implementation of the runtime. |
| CLS | Common Language Specification | The portion of the CLI that defines a subset of features that source languages must support. |
| CTS | Common Type System | The part of the CLI that defines the representation of types. |
| FCL | .NET Framework Library | The large library that makes up the .NET Framework. |
| VES | Virtual Execution System | An agent that executes CIL. |
