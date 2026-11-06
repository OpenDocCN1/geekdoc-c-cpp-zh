
## 17. Avoid magic numbers.

### Summary

Programming isn’t magic, so don’t incant it: Avoid spelling literal constants like **42** or **3.14159** in code. They are not self-explanatory and complicate maintenance by adding a hard-to-detect form of duplication. Use symbolic names and expressions instead, such as **width * aspectRatio**.

### Discussion

Names add information and introduce a single point of maintenance; raw numbers duplicated throughout a program are anonymous and a maintenance hassle. Constants should be enumerators or **const** values, scoped and named appropriately.

One **42** may not be the same as another **42**. Worse, “in-head” computations made by the programmer (e.g., “this **84** comes from doubling the **42** used five lines ago”) make it tedious and error-prone to later replace **42** with another constant.

Prefer replacing hardcoded strings with symbolic constants. Keeping strings separate from the code (e.g., in a dedicated **.cpp** or resource file) lets non-programmers review and update them, reduces duplication, and helps internationalization.

### Examples

*Example 1: Important domain-specific constants at namespace level.*

```cpp
const size_t PAGE_SIZE              = 8192;
           WORDS_PER_PAGE           = PAGE_SIZE / sizeof(int),
           INFO_BITS_PER_PAGE = 32 * CHAR_BIT;
```

*Example 2: Class-specific constants.* You can define static integral constants in the class definition; constants of other types need a separate definition or a short function.

```cpp
// File widget.h
class Widget {
  static const int defaultWidth = 400;          // value provided in declaration
  static const double defaultPercent;           // value provided in definition
  static const char* Name() { return "Widget"; }
};

// File widget.cpp
const double Widget::defaultPercent = 66.67; // value provided in definition
const int Widget::defaultWidth;              // definition required
```

### References

*[Dewhurst03] §2 • [Kernighan99] §1.5 • [Stroustrup00] §4.8, §5.4*

## 19. Always initialize variables.

### Summary

Start with a clean slate: Uninitialized variables are a common source of bugs in C and C++ programs. Avoid such bugs by being disciplined about cleaning memory before you use it; initialize variables upon definition.

### Discussion

In the low-level efficiency tradition of C and C++ alike, the compiler is often not required to initialize variables unless you do it explicitly (e.g., local variables, forgotten members omitted from constructor initializer lists). Do it explicitly.

There are few reasons to ever leave a variable uninitialized. None is serious enough to justify the hazard of undefined behavior.

If you’ve used a procedural language (e.g., Pascal, C, Fortran, or Cobol) you might be used to defining variables in separation from the code that uses them, and then assigning them values later when they’re about to be used. This approach is obsolete and not recommended (see Item 18).

A common misconception about uninitialized variables is that they will crash the program, so that those few uninitialized variables lying around here and there will be quickly revealed by simple testing. On the contrary, programs with uninitialized variables can run flawlessly for years if the bits in the memory happen to match the program’s needs. Later, a call from a different context, a recompilation, or some change in another part of the program will cause failures ranging from inexplicable behavior to intermittent crashes.

### Examples

*Example 1: Using a default initial value or ?: to reduce mixing data flow with control flow.*

```cpp
// Not recommended: Doesn't initialize variable
int speedupFactor;
if( condition )
  speedupFactor = 2;
else
  speedupFactor = -1;
```

```cpp
// Better: Initializes variable
int speedupFactor = -1;
if( condition )
  speedupFactor = 2;
```

## 20. Avoid long functions. Avoid deep nesting.

### Summary

Short is better than long, flat is better than deep: Excessively long functions and nested code blocks are often caused by failing to give one function one cohesive responsibility (see Item 5), and both are usually solved by better refactoring.

### Discussion

Every function should be a coherent unit of work bearing a suggestive name (see Item 5 and the Discussion in Item 70). When a function instead tries to merge such small conceptual elements inside a long function body, it ends up doing too much.

Excessive straight-line function length and excessive block nesting depth (e.g., if, for, while, and try blocks) are twin culprits that make functions more difficult to understand and maintain, and often needlessly so.

Each level of nesting adds intellectual overhead when reading code because you need to maintain a mental stack (e.g., enter conditional, enter loop, enter try, enter conditional, …). Have you ever found a closing brace in someone’s code and wondered which of the many fors, whiles, or ifs it matched? Prefer better functional decomposition to help avoid forcing readers to keep as much context in mind at a time.

Exercise common sense and reasonableness: Limit the length and depth of your functions. All of the following good advice also helps reduce length and nesting:

- *Prefer cohesion:* Give one function one responsibility (see Item 5).
- *Don’t repeat yourself:* Prefer a named function over repeated similar code snippets.
- *Prefer &&:* Avoid nested consecutive ifs where an && condition will do.
- *Don’t try too hard:* Prefer automatic cleanup via destructors over try blocks (see Item 13).
- *Prefer algorithms:* They’re flatter than loops, and often better (see Item 84).
- *Don’t switch on type tags:* Prefer polymorphic functions (see Item 90).

### Exceptions

A function might be legitimately long and/or deep when its functionality can’t be reasonably refactored into independent subtasks because every potential refactoring would require passing many local variables and context (rendering the result less readable rather than more readable). But if several such potential functions take similar arguments, they might be candidates for becoming members of a new class.

### References

[*Piwowarski82*] • [*Miller56*]

## 21. Avoid initialization dependencies across compilation units.

### Summary

Keep (initialization) order: Namespace-level objects in different compilation units should never depend on each other for initialization, because their initialization order is undefined. Doing otherwise causes headaches ranging from mysterious crashes when you make small changes in your project to severe non-portability even to new releases of the same compiler.

### Discussion

When you define two namespace-level objects in different compilation units, which object’s constructor is called first is not defined. Often (but not always) your tools might happen to initialize them in the order in which the compilation units’ object files are linked, but this assumption is usually not reliable; even when it does hold, you don’t want the correctness of your code to subtly depend on your makefile or project file. (For more on the evils of order dependencies, see also Item 59.)

Therefore, inside the initialization code of any namespace-level object, you can’t assume that any other object defined in a different compilation unit has already been initialized. These considerations apply to dynamically initialized variables of primitive types, such as a namespace-level **bool reg_success = LibRegister("mylib");**

Note that, even before they are ever constructed using a constructor, namespace-level objects are statically initialized with all zeroes (as opposed to, say, automatic objects that initially contain garbage). Paradoxically, this zero-initialization can make bugs harder to detect, because instead of crashing your program swiftly the static zero-initialization gives your yet-uninitialized object an appearance of legitimacy. You’d think that the string is empty, that pointer is null, and that integer is zero, when in fact no code of yours has bothered to initialize them yet.

To avoid this problem, avoid namespace-level variables wherever possible; they are dangerous (see Item 10). When you do need such a variable that might depend upon another, consider the Singleton design pattern; used carefully, it might avoid implicit dependencies by ensuring that an object is initialized upon first access. Still, Singleton is a global variable in sheep’s clothing (see again Item 10), and is broken by mutual or cyclic dependencies (again, zero-initialization only adds to the confusion).

### References

[Dewhurst03] §55 • [Gamma95] • [McConnell93] §5.1-4 • [Stroustrup00] §9.4.1, §10.4.9
