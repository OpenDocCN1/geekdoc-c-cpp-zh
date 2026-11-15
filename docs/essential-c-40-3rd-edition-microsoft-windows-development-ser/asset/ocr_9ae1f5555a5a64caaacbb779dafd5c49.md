NGEN at installation (or at any time prior to execution) is that you can reduce the need for the jitter to run at startup, thereby decreasing startup time.

# Runtime

Even after the runtime converts the CIL code to machine code and starts to execute, it continues to maintain control of its execution. The code that executes under the context of an agent such as the runtime is managed code, and the process of executing under control of the runtime is managed execution. The control over execution transfers to the data; this makes it managed data because memory for the data is automatically allocated and de-allocated by the runtime.

Somewhat inconsistently, the term Common Language Runtime (CLR) is not technically a generic term that is part of the CLI. Rather, CLR is the Microsoft-specific implementation of the runtime for the .NET platform. Regardless, CLR is casually used as a generic term for runtime, and the technically accurate term, Virtual Execution System, is seldom used outside the context of the CLI specification.

Because an agent controls program execution, it is possible to inject additional services into a program, even though programmers did not explicitly code for them. Managed code, therefore, provides information to allow these services to be attached. Among other items, managed code enables the location of metadata about a type member, exception handling, access to security information, and the capability to walk the stack. The remainder of this section includes a description of some additional services made available via the runtime and managed execution. The CLI does not explicitly require all of them, but the established CLI platforms have an implementation of each.

# Garbage Collection

Garbage collection is the process of automatically de-allocating memory based on the program’s needs. This is a significant programming problem for languages that don’t have an automated system for doing this. Without the garbage collector, programmers must remember to always free any memory allocations they make. Forgetting to do so, or doing so repeatedly