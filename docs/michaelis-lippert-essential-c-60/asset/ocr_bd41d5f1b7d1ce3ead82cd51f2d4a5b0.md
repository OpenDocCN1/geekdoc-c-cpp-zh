execution time and then invoke that member or determine whether a construct is decorated with a particular attribute. This provides **late binding**, in which the system determines which code to execute at execution time rather than at compile time. Reflection can even be used for generating documentation by iterating through metadata and copying it into a help document of some kind (see Chapter 17).

# SUMMARY

This chapter described many new terms and acronyms that are important for understanding the context under which C# programs run. The preponderance of three-letter acronyms can be confusing. Table 21.2 provides a summary list of the terms and acronyms that are part of the CLI.

# TABLE 21.2: Common C#-Related Acronyms

| Acronym | Definition | Description |
|---|---|---|
| .NET | None | Microsoft’s implementation of the entire CLI stack. Includes the CLR, CIL, and various languages, all of which are CLS-compliant. |
| BCL | Base Class Library | The portion of the CLI specification that defines the collection, threading, console, and other base classes necessary to build virtually all programs. |
| C# | None | A programming language. Separate from the CLI standard is a C# Language Specification, also ratified by the ECMA and ISO standards bodies. |
| CIL (IL) | Common Intermediate Language | The language of the CLI specification that defines the instructions for the code executable on implementations of the CLI. It is sometimes also referred to as IL or Microsoft IL (MSIL) to distinguish it from other intermediate languages. (To indicate that it is a standard broader than Microsoft, CIL is preferred over MSIL and even IL.) |
| CLI | Common Language Infrastructure | The specification that defines the intermediate language, base classes, and behavioral characteristics which enable implementers to create Virtual Execution Systems and compilers in which source languages are interoperable on top of a common execution environment. |