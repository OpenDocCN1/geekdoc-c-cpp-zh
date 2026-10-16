# 10.6 Exception Handling and Environments

In the previous chapter, we described exception handling in some detail in terms of its syntax, semantics, and use. This section introduces some implementation issues, particularly as they affect the structure and behavior of the runtime environment. Further detail can be found in the sources listed in the Notes and References.

In principle, the operations of raising and handling exceptions are similar to procedure calls, and they can be implemented in similar ways. However, there are major differences as well. Primary among these are:

+   1. An activation cannot be created on the runtime stack to represent the raising of an exception, since this stack itself may be unwound as previously described when searching for a handler.
+   
+   2. A handler must be found and called dynamically, rather than statically as with ordinary function calls.
+   
+   3. The actions of a handler are based on the type of the exception, rather than the exception value itself; thus, exception type information must be retained during execution, contrary to standard practice for statically typed languages.

The first difference can be easily overcome. When an exception is raised, no activation record is created. Instead, the exception object and its type information are placed in a known location, such as a register or static memory. A jump is then performed to generic code that looks for a handler. Exit code is called if a handler is not found. The return address for the successful handling of an exception must also be stored in a known location. Under the termination model, this address is the location following the block in which the exception occurred. Otherwise, it is the return address of the most recent call, if the block is a procedure.

The second difference is more problematic. Pointers to handlers must, at least in theory, be kept on some kind of stack. Each time code is entered that has an associated handler, a new handler pointer is pushed, and when that same code is exited, the pointer is popped again to reveal any previous handlers. If this stack is to be implemented directly, it must be maintained either on the heap or elsewhere in its own memory area (i.e., not on the runtime stack), and a pointer to the current stack top must be maintained, either in static memory or in a register.

The third difference is somewhat less problematic but may involve some complexity that we will not go into here. The main issue is how to record the needed type information (essentially the type names) without added overhead in the exception structures themselves. One possibility is to have some sort of lookup table.

Once these issues have been addressed, the implementation of handlers is relatively straightforward. The basic idea is to collect all handler code attached to a particular block into a single handler implemented as a switch statement, based on the type of the exception parameter received, with a

> 13 Of course, languages with dynamic types, such as LISP and Smalltalk, already have type information available at runtime. C++ and Java also have mechanisms available for preserving and extracting type information when necessary at runtime; in C++ the mechanism is called RTTI (for Run Time Type Information); in Java it is called Reflection.