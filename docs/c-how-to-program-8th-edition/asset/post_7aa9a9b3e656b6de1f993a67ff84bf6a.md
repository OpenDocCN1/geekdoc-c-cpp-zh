
- When function exit is invoked, any functions registered with `atexit` are invoked in the reverse order of their registration, all streams associated with the program are flushed and closed, and control returns to the host environment.

## Section F.7 Type Qualifier volatile

- The volatile qualifier is used to prevent optimizations of a variable, because it can be modified from outside the program’s scope.

## Section F.8 Suffixes for Integer and Floating-Point Constants

- C++ provides integer and floating-point suffixes for specifying the types of integer and floating-point constants. The integer suffixes are u or U for an unsigned integer, l or L for a long integer and ul or UL for an unsigned long integer. If an integer constant is not suffixed, its type is determined by the first type capable of storing a value of that size (first int, then long int). The floating-point suffixes are f or F for a float and l or L for a long double. A floating-point constant that is not suffixed is of type double.

## Section F.9 Signal Handling

- The signal-handling library provides the capability to register a function to trap unexpected events with function signal. Function signal receives two arguments—an integer signal number and a pointer to the signal-handling function.
- Signals can also be generated with function raise and an integer argument.

## Section F.10 Dynamic Memory Allocation with calloc and realloc

- The general-utilities library (cstdlib) provides functions calloc and realloc for dynamic memory allocation. These functions can be used to create dynamic arrays.
- Function calloc receives two arguments—the number of elements (nmem) and the size of each element (size)—and initializes the elements of the array to zero. The function returns a pointer to the allocated memory or, if the memory is not allocated, the function returns a null pointer.
- Function realloc changes the size of an object allocated by a previous call to malloc, calloc or realloc. The original object’s contents are not modified, provided that the amount of memory allocated is larger than the amount allocated previously.
- Function realloc takes two arguments—a pointer to the original object (ptr) and the new size of the object (size). If ptr is null, realloc works identically to malloc. If size is 0 and the pointer received is not null, the memory for the object is freed. Otherwise, if ptr is not null and size is greater than zero, realloc tries to allocate a new block of memory for the object. If the new space cannot be allocated, the object pointed to by ptr is unchanged. Function realloc returns either a pointer to the reallocated memory or a null pointer.

## Section F.11 Unconditional Branch: goto

- The result of the goto statement is a change in the program’s flow of control. Program execution continues at the first statement after the label in the goto statement.
- A label is an identifier followed by a colon. A label must appear in the same function as the goto statement that refers to it.

## Section F.12 Unions

- A union is a data type whose members share the same storage space. The members can be almost any type. The storage reserved for a union is large enough to store its largest member. In most cases, unions contain two or more data types. Only one member, and thus one data type, can be referenced at a time.
- A union is declared in the same format as a structure.
- A union can be initialized only with a value of the type of its first member or another object of the same union type.

## Section F.13 Linkage Specifications

- C++ enables you to provide linkage specifications to inform the compiler that a function was compiled with a C compiler and to prevent the name of the function from being encoded by the C++ compiler.
- To inform the compiler that one or several functions have been compiled in C, write the function prototypes as follows:

  ```cpp
  extern "C" function prototype   // single function

  extern "C"                    // multiple functions
  {
      function prototypes
  }
  ```

  These declarations inform the compiler that the specified functions are not compiled in C++, so name encoding should not be performed on the functions listed in the linkage specification. These functions can then be linked properly with the program.
- C++ environments normally include the standard C libraries and do not require you to use linkage specifications for those functions.

## Self-Review Exercises

**F.1** Fill in the blanks in each of the following:

- a) Symbol ________ redirects input data from the keyboard to come from a file.
- b) The ________ symbol is used to redirect the screen output to be placed in a file.
- c) The ________ symbol is used to append the output of a program to the end of a file.
- d) A(n) ________ is used to direct the output of a program as the input of another program.
- e) A(n) ________ in the parameter list of a function indicates that the function can receive a variable number of arguments.
- f) Macro ________ must be invoked before the arguments in a variable-length argument list can be accessed.
- g) Macro ________ is used to access the individual arguments of a variable-length argument list.
- h) Macro ________ performs termination housekeeping in a function whose variable argument list was referred to by macro va_start.
- i) Argument ________ of main receives the number of arguments in a command line.
- j) Argument ________ of main stores command-line arguments as character strings.
- k) The UNIX utility ________ reads a file called ________ that contains instructions for compiling and linking a program consisting of multiple source files. The utility recompiles a file only if the file (or a header it uses) has been modified since it was last compiled.
- l) Function ________ forces a program to terminate execution.
- m) Function ________ registers a function to be called upon normal termination of the program.
- n) An integer or floating-point ________ can be appended to an integer or floating-point constant to specify the exact type of the constant.
- o) Function ________ can be used to register a function to trap unexpected events.
- p) Function ________ generates a signal from within a program.

**F.12** Given the union

```c
union A
{
    double y;
    char *zPtr;
};
```

Which of the following are correct statements for initializing the union?

- a) `A p = b;` // b is of type A
- b) `A q = x;` // x is a double
- c) `A r = 3.14159;`
- d) `A s = { 75.63 };`
- e) `A t = { "Hi There!" };`
- f) `A u = { 3.14159, "Hi" };`
- g) `A v = { y = -7.843, zPtr = &x };`

# UML 2: Additional Diagram Types

## G.1 Introduction

If you’ve read the optional Software Engineering Case Study in Chapters 25–26, you should now have a comfortable grasp of the UML diagram types that we use to model our ATM system. The case study is intended for use in first- or second-semester courses, so we limit our discussion to a concise subset of the UML. The UML 2 provides a total of 13 diagram types. The end of Section 25.3 summarizes the six diagram types that we use in the case study. This appendix lists and briefly defines the seven remaining diagram types.

## G.2 Additional Diagram Types

The following are the seven diagram types that we’ve chosen not to use in our Software Engineering Case Study.

- **Object diagrams** model a “snapshot” of the system by modeling a system’s objects and their relationships at a specific point in time. Each object represents an instance of a class from a class diagram, and several objects may be created from one class. For our ATM system, an object diagram could show several distinct Account objects side by side, illustrating that they are all part of the bank’s account database.
- **Component diagrams** model the artifacts and components—resources (which include source files)—that make up the system.
- **Deployment diagrams** model the system’s runtime requirements (such as the computer or computers on which the system will reside), memory requirements, or other devices the system requires during execution.
- **Package diagrams** model the hierarchical structure of packages (which are groups of classes) in the system at compile time and the relationships that exist between the packages.
- **Composite structure diagrams** model the internal structure of a complex object at runtime. New in UML 2, they allow system designers to hierarchically decompose a complex object into smaller parts. Composite structure diagrams are beyond the scope of our case study. They are more appropriate for larger industrial applications, which exhibit complex groupings of objects at execution time.
