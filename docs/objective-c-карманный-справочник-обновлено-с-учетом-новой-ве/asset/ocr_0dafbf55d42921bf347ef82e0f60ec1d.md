# 5

# Numbers

One of the big differences between Objective-C and Smalltalk is that Objective-C inherits the full range of primitive (non-object) C types. These are, in ascending order of size, **char, short, int, long and long long** integers, with both signed and unsigned variants, as well as two floating-point types: **float** and double. These all behave exactly as they do in C, complete with type promotion rules. You'll also find that Objective-C compilers support a **long double** type, which is architecture-dependent.

Note that this is very similar to Java, where you have a small selection of non-object types, but with some very important differences. In Java, the *intrinsic types* are defined to have a fixed size. In C, they are defined to have a minimum precision. For example, the specification says that an **int** has “the natural size suggested by the architecture of the execution environment,\”