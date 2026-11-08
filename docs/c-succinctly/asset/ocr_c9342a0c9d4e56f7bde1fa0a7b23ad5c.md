# Chapter 4 Storage Duration

# Overview

To quote the C++ Language Standard, “Storage duration is the property of an object that defines the minimum potential lifetime of the storage containing the object.” Basically, it tells you how long you should expect a variable to be usable. The variable might be a fundamental type, such as an int, or a complex type, such as a class. Regardless of its type, a variable is only guaranteed to last for as long as the programming language says it should.

C++ manages memory very differently from C#. For one thing, there is no requirement to have a garbage collector, and few implementations provide one. To the extent that C++ implementations do have automatic memory management, they mostly do so through smart pointers and reference counting. C++ classes do not automatically live on a heap (GC-managed or otherwise). Instead, they [work much more like structures in C#](#).

You can push a C++ class instance onto a heap when you need to, but if you declare it locally and don’t do anything funny, then it will have an automatic duration, typically implemented using a stack, and will be automatically destroyed when the program leaves the scope in which the class exists.

C++ gives you more control over memory management than C#. A consequence of this is that the C++ language and runtime environment cannot do as much to prevent erroneous code as the C# language and the CLR can. One of the keys to being a good C++ programmer is to understand how memory management works and to use the best practices in order to write efficient, correct code.

# Static Duration

Global variables, including those inside namespaces, and variables marked with the duration keyword `static` have static storage duration.

Global variables are initialized during program initialization (i.e. the period before the program actually starts execution of your main or wmain function). They are initialized in the order in which they are defined in the source code. It’s generally not a good idea to rely on initialization order since refactoring and other seemingly innocent changes could easily introduce a potential bug into your program.

Local statics are zero-initialized the first time program execution reaches the block containing the local static. Typically, they will be initialized to their specified values or initialized by calling the specified constructor at that point. The value assignment or construction phase is not required until the program reaches and executes the statement, except in very rare circumstances. Once a local static is initialized, the initialization specified with its declaration will never run again. This, of course, is just what we would expect of a local static. If kept initialized itself every time the program reached its definition line, then it would be the same as a non-static local.

You can assign other values to global and local statics, unless you also make them const, of course.

# Automatic Duration

Within a block, an object has automatic duration if it is defined without the new operator to instantiate it, and without a storage duration keyword, although it can optionally have the register keyword. This means the object is created at the point when it is defined and is destroyed when the program exits the block its variable was declared in, or when a new value is assigned to the variable.