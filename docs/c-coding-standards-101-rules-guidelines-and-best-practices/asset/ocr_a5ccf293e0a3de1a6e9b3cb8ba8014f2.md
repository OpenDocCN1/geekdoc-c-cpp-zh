# # 63. Use sufficiently portable types in a module’s interface.

# ## Summary

Take extra care when living on the edge (of a module): Don’t allow a type to appear in a module’s external interface unless you can ensure that all clients understand the type correctly. Use the highest level of abstraction that clients can understand.

# ## Discussion

The more widely distributed your library, and the less control you have over the build environment of all of its clients, the fewer the types that the library can reliably use in its external interface. Interfacing across modules involves binary data exchange. Alas, C++ doesn’t specify standard binary interfaces; widely distributed libraries in particular might need to rely on built-in types like int and char to interface with the outer world. Even compiling the same type using different build options on the same compiler can cause binary-incompatible versions of the type.

Typically, either you control the compiler and options used to build the module and all its clients, and you can use any type—or you don’t, and you can use only platform-provided types and C++ built-in types (even then, document the size and representation you expect for the latter). In particular, never mention standard library types in the interface of a module unless all other modules that use it will be compiled at the same time and with the same standard library source image.

There is a tradeoff between the problems of using types that can’t be correctly understood by all clients, and the problems of using a low level of abstraction. Abstraction is important; if some clients understand only low-level types, and you must therefore use those, consider also supplying alternate operations that use higher-level types. Consider a SummarizeFile function that takes the file to be processed as a parameter. There are three common options for the parameter: It can be a char\* that points to a C-style string containing the file’s name; a string that contains the file’s name; or an istream or a custom File object. Each of these choices is a tradeoff:

+   - Option 1: char\*. Clearly the char\* type is accessible to the widest audience of clients. Unfortunately, it is also the lowest-level option; in particular, it is less robust (e.g., the caller and callee must explicitly decide who allocates the memory and who deallocates it), more open to errors (e.g., the file might not exist), and less secure (e.g., to classic buffer overrun attacks).

+   - Option 2: string. The string type is accessible to the more restricted audience of clients that are written in C++ and compiled using the same standard library implementation, the same compiler, and compatible compiler settings. In exchange, it is more robust (e.g., callers and callees can be less explicit about