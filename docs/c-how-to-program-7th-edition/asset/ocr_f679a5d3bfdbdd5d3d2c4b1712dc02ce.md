**Good Programming Practice 9.1**
For clarity and readability, use each access specifier only once in a class definition. Place `public` members first, where they're easy to locate.

**Software Engineering Observation 9.1**
Each element of a class should have private visibility unless it can be proven that the element needs `public` visibility. This is another example of the principle of least privilege.

In Fig. 9.1, the class definition is enclosed in the following preprocessor wrapper (lines 6, 7 and 23):

```
```cpp
// prevent multiple inclusions of header file
#ifndef TIME_H
#define TIME_H
   ...
#endif
```
```

When we build larger programs, other definitions and declarations will also be placed in header files. The preceding preprocessor wrapper prevents the code between `#ifndef` (which means "if not defined") and `#endif` from being included if the name `TIME_H` has been defined. If the header has not been included previously in a file, the name `TIME_H` is defined by the `#define` directive and the header file statements are included. If the header has been included previously, `TIME_H` is defined already and the header file is not included again. Attempts to include a header file multiple times (inadvertently) typically occur in large programs with many header files that may themselves include other header files. [*Note*: The commonly used convention for the symbolic constant name in the preprocessor directives is simply the header file name in upper case with the underscore character replacing the period.]

**Error-Prevention Tip 9.1**
Use `#ifndef`, `#define` and `#endif` preprocessor directives to form a preprocessor wrapper that prevents header files from being included more than once in a program.

**Good Programming Practice 9.2**
Use the name of the header file in upper case with the period replaced by an underscore in the `#ifndef` and `#define` preprocessor directives of a header file.

# *Time* Class Member Functions

In Fig. 9.2, the `Time` constructor (lines 10–13) initializes the data members to 0—the universal-time equivalent of 12 AM. This ensures that the object begins in a consistent state. Invalid values cannot be stored in the data members of a `Time` object, because the constructor is called when the `Time` object is created, and all subsequent attempts by a client to modify the data members are scrutinized by function `setTime` (discussed shortly). Finally, it's important to note that you can define several overloaded constructors for a class.

The data members of a class cannot be initialized when they're declared in the class body. It's strongly recommended that these data members be initialized by the class's constructor (as there is no default initialization for fundamental-type data members). Data members can also be assigned values by `Time`'s `set` functions. [*Note*: Chapter 10 demon-