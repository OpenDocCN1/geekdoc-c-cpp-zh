Application startup occurs when the execution environment calls the application's entry point. If the entry point declares a parameter, then during application startup, the implementation shall ensure that the initial value of that parameter is a non-null reference to a string array. This array shall consist of non-null references to strings, called application parameters, which are given implementation-defined values by the host environment prior to application startup. The intent is to supply to the application information determined prior to application startup from elsewhere in the hosted environment.

> *Note:* On systems supporting a command line, application parameters correspond to what are generally known as command-line arguments. *end note*

If the entry point's return type is int rather than void, the return value from the method invocation by the execution environment is used in application termination (§7.2).

Other than the situations listed above, entry point methods behave like those that are not entry points in every respect. In particular, if the entry point is invoked at any other point during the application's lifetime, such as by regular method invocation, there is no special handling of the method: if there is a parameter, it may have an initial value of null, or a non-null value referring to an array that contains null references. Likewise, the return value of the entry point has no special significance other than in the invocation from the execution environment.

# 7.2 Application termination

*Application termination* returns control to the execution environment.

If the return type of the application's entry point method is int, the value returned serves as the application's *termination status code*. The purpose of this code is to allow communication of success or failure to the execution environment.

If the return type of the entry point method is void, reaching the right brace (}) that terminates that method, or executing a return statement that has no expression, results in a termination status code of 0. If the entry point method terminates due to an exception (§20.4), the exit code is implementation-specific. Additionally, the implementation may provide alternative APIs for specifying the exit code.

Whether or not finalizers (§14.13) are run as part of application termination is implementation-specific.

> *Note:* The .NET Framework implementation makes every reasonable effort to call finalizers (§14.13) for all of its objects that have not yet been garbage collected, unless such cleanup has been suppressed (by a call to the library method GC.SuppressFinalize, for example). *end note*

# 7.3 Declarations

Declarations in a C# program define the constituent elements of the program. C# programs are organized using namespaces. These are introduced using namespace declarations (§13), which can contain type declarations and nested namespace declarations. Type declarations (§13.7) are used to define classes (§14), structs (§15), interfaces (§17), enums (§18), and delegates (§19). The kinds of members permitted in a type declaration depend on the form of the type declaration. For instance, class declarations can contain declarations for constants (§14.4), fields (§14.5), methods (§14.6), properties (§14.7), events (§14.8), indexers (§14.9), operators (§14.10), instance constructors (§14.11), static constructors (§14.12), finalizers (§14.13), and nested types (§14.3.9).

A declaration defines a name in the *declaration space* to which the declaration belongs. It is a compile-time error to have two or more declarations that introduce members with the same name in a declaration space, except in the following cases: