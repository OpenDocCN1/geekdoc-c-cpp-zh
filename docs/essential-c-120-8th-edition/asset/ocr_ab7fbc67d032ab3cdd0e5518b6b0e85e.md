# Managed Execution and the Common Language Infrastructure 39

significant portions of the program’s behavior by managing aspects such as memory allocation, security, and just-in-time compilation. That code does not require the runtime to execute is called native code (or unmanaged code).

The specification for a runtime is included in a broader specification known as the Common Language Infrastructure (CLI) specification.15 An international standard, the CLI includes specifications for the following:

> NOTE

The term runtime can refer to either execution time or the VES. To help clarify the intended meaning, this book uses the term execution time to indicate when the program is executing, and it uses the term runtime when discussing the agent responsible for managing the execution of a C# program while it executes.

Running within the context of a runtime execution engine enables support for several services and features that programmers do not need to code for directly, including the following:

15. Miller, J., and S. Ragsdale. 2004. The Common Language Infrastructure Annotated Standard. Boston: Addison-Wesley.