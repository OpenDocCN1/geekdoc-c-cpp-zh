# 18. Unsafe code

The core C# language, as defined in the preceding chapters, differs notably from C and C++ in its omission of pointers as a data type. Instead, C# provides references and the ability to create objects that are managed by a garbage collector. This design, coupled with other features, makes C# a much safer language than C or C++. In the core C# language it is simply not possible to have an uninitialized variable, a “dangling” pointer, or an expression that indexes an array beyond its bounds. Whole categories of bugs that routinely plague C and C++ programs are thus eliminated.

While practically every pointer type construct in C or C++ has a reference type counterpart in C#, nonetheless, there are situations where access to pointer types becomes a necessity. For example, interfacing with the underlying operating system, accessing a memory-mapped device, or implementing a time-critical algorithm may not be possible or practical without access to pointers. To address this need, C# provides the ability to write unsafe code.

In unsafe code it is possible to declare and operate on pointers, to perform conversions between pointers and integral types, to take the address of variables, and so forth. In a sense, writing unsafe code is much like writing C code within a C# program.

Unsafe code is in fact a “safe” feature from the perspective of both developers and users. Unsafe code must be clearly marked with the modifier unsafe, so developers can’t possibly use unsafe features accidentally, and the execution engine works to ensure that unsafe code cannot be executed in an untrusted environment.

# 18.1 Unsafe contexts

The unsafe features of C# are available only in unsafe contexts. An unsafe context is introduced by including an unsafe modifier in the declaration of a type or member, or by employing an unsafe-statement:

+   - A declaration of a class, struct, interface, or delegate may include an unsafe modifier, in which case the entire textual extent of that type declaration (including the body of the class, struct, or interface) is considered an unsafe context.
+   - A declaration of a field, method, property, event, indexer, operator, instance constructor, destructor, or static constructor may include an unsafe modifier, in which case the entire textual extent of that member declaration is considered an unsafe context.
+   - An unsafe-statement enables the use of an unsafe context within a block. The entire textual extent of the associated block is considered an unsafe context.

The associated grammar extensions are shown below. For brevity, ellipses (...) are used to represent productions that appear in preceding chapters.

```
class-modifier:
    ...
    unsafe

struct-modifier:
    ...
    unsafe

interface-modifier:
    ...
    unsafe
```