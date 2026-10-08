Chapter 16. Types IV: Qualifiers and Specifiers

# 16.2.5 _Thread_local

When you're using multiple threads and you have some variables in either global or block scope, this is a way to make sure that each thread gets its own copy of the variable. This'll help you avoid race conditions and threads stepping on each other's toes.

If you're in block scope, you have to use this along with either extern or static.

Also, if you include <threads.h>, you can use the rather more palatable thread_local as an alias for the uglier _Thread_local.

More information can be found in the Threads section.