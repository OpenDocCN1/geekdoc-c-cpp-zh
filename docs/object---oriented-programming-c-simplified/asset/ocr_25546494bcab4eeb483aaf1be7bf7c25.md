of date because implementers are working hard to ensure that their implementations correctly accept every C++ feature.

# SUGGESTIONS FOR C PROGRAMMERS

The better one knows C, the harder it seems to be to avoid writing C++ in C style, thereby losing some of the potential benefits of C++. Please take a look at Appendix B, which describes the differences between C and C++. Here are a few pointers to the areas in which C++ has better ways of doing something than C has:

+   1. Macros are almost never necessary in C++. Use `const` or `enum` to define manifest constants, `inline` to avoid function-calling overhead, `templates` to specify families of functions and types, and `namespaces` to avoid name clashes.
+   2. Don't declare a variable before you need it so that you can initialize it immediately. A declaration can occur anywhere a statement can, in `for-statement` initializers, and in conditions.
+   3. Don't use `malloc()`. The `new` operator does the same job better, and instead of `realloc()`, try a `vector`.
+   4. Try to avoid `void *`, pointer arithmetic, unions, and casts, except deep within the implementation of some function or class. In most cases, a cast is an indication of a design error. If you must use an explicit type conversion, try using one of the “new casts” for a more precise statement of what you are trying to do.
+   5. Minimize the use of arrays and C-style strings. The C++ standard library `string` and `vector` classes can often be used to simplify programming compared to traditional C style. In general, try not to build yourself what has already been provided by the standard library.

To obey C linkage conventions, a C++ function must be declared to have C linkage. Most important, try thinking of a program as a set of interacting concepts represented as classes and objects, instead of as a bunch of data structures with functions twiddling their bits.

# SUGGESTIONS FOR C++ PROGRAMMERS

By now, many people have been using C++ for a decade. Many more are using C++ in a single environment and have learned to live with the restrictions imposed by early compilers and first generation libraries. Often, what an experienced C++ programmer has failed to notice over the years is not the introduction of new features as such, but rather the changes in relationships between features that make fundamentally new programming techniques feasible. In other words, what you didn’t think of when first learning C++ or found impractical just might be a superior approach today. You find out only by re-examining the basics.

Read through the chapters in order. If you already know the contents of a chapter, you can be through in minutes. If you don’t already know the contents, you’ll have learned something unexpected. I learned a fair bit writing this book and I suspect that hardly any C++ programmer knows every feature and technique presented. Furthermore, to use the language well, you need a perspective that brings order to the set of features and techniques. Through its organization and examples, this book offers such a perspective.