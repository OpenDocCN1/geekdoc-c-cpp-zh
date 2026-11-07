
Figure F.8 uses the variable value of type union Number to display the value stored in the union as both an int and a double. The program output is implementation dependent. The program output shows that the internal representation of a double value can be quite different from the representation of an int.

```cpp
// Fig. F.8: FigF08.cpp
// An example of a union.
#include <iostream>
using namespace std;

// define union Number
union Number
{
   int integer1;
   double double1;
}; // end union Number

int main()
{
   Number value; // union variable

   value.integer1 = 100; // assign 100 to member integer1

   cout << "Put a value in the integer member\n"
        << "and print both members.\nint: "
        << value.integer1 << "\ndouble: " << value.double1
        << endl;

   value.double1 = 100.0; // assign 100.0 to member double1

   cout << "Put a value in the floating member\n"
        << "and print both members.\nint: "
        << value.integer1 << "\ndouble: " << value.double1
        << endl;
} // end main
```

```text
Put a value in the integer member
and print both members.
int: 100
double: -2.95596e+061
Put a value in the floating member
and print both members.
int: 0
double: 100
```

**Fig. F.8** | Printing the value of a union in both member data types.

An **anonymous union** is a union without a type name that does not attempt to define objects or pointers before its terminating semicolon. Such a union does not create a type but does create an unnamed object. An anonymous union’s members may be accessed directly in the scope in which the anonymous union is declared just as are any other local variables—there is no need to use the dot (.) or arrow (->) operators.

Anonymous unions have some restrictions. Anonymous unions can contain only data members. All members of an anonymous union must be public. And an anonymous union declared globally (i.e., at global namespace scope) must be explicitly declared static. Figure F.9 illustrates the use of an anonymous union.

```cpp
// Fig. F.9: FigF_09.cpp
// Using an anonymous union.
#include <iostream>
using namespace std;

int main()
{
   // declare an anonymous union
   // members integer1, double1 and charPtr share the same space
   union
   {
      int integer1;
      double double1;
      char *charPtr;
   };  // end anonymous union

   // declare local variables
   int integer2 = 1;
   double double2 = 3.3;
   char *char2Ptr = "Anonymous";

   // assign value to each union member
   // successively and print each
   cout << integer2 << ' ';
   integer1 = 2;
   cout << integer1 << endl;

   cout << double2 << ' ';
   double1 = 4.4;
   cout << double1 << endl;

   cout << char2Ptr << ' ';
   charPtr = "union";
   cout << charPtr << endl;
}  // end main
```

```text
1 2
3.3 4.4
Anonymous union
```

**Fig. F.9** | Using an anonymous union.

## F.13 Linkage Specifications

It is possible for a C++ program to call functions written and compiled with a C compiler. As stated in Section 6.17, C++ specially encodes function names for type-safe linkage. C, however, does not encode its function names. Thus, a function compiled in C will not be recognized when an attempt is made to link C code with C++ code, because the C++ code expects a specially encoded function name. C++ enables you to provide [linkage specifications](#) to inform the compiler that a function was compiled on a C compiler and to prevent the name of the function from being encoded by the C++ compiler. Linkage specifications are useful when large libraries of specialized functions have been developed, and the user either does not have access to the source code for recompilation into C++ or does not have time to convert the library functions from C to C++.

To inform the compiler that one or several functions have been compiled in C, write the function prototypes as follows:

```cpp
extern "C" function prototype    // single function

extern "C"                    // multiple functions
{
    function prototypes
}
```

These declarations inform the compiler that the specified functions are not compiled in C++, so name encoding should not be performed on the functions listed in the linkage specification. These functions can then be linked properly with the program. C++ environments normally include the standard C libraries and do not require you to use linkage specifications for those functions.

## F.14 Wrap-Up

This appendix introduced a number of C legacy-code topics. We discussed redirecting keyboard input to come from a file and redirecting screen output to a file. We also introduced variable-length argument lists, command-line arguments and processing of unexpected events. You also learned about allocating and resizing memory dynamically.

## Summary

### Section F.2 Redirecting Input/Output on UNIX/Linux/Mac OS X and Windows Systems

- On many systems—UNIX, LINUX, Mac OS X or Windows systems in particular—it is possible to redirect input to a program and output from a program. Input is redirected from the UNIX, LINUX, Mac OS X or Windows command lines using the redirect input symbol (<) or a pipe (|). Output is redirected from the UNIX, LINUX, Mac OS X or Windows command lines using the redirect output symbol (>) or the append output symbol (>>). The redirect output symbol simply stores the program output in a file, and the append output symbol appends the output to the end of a file.

### Section F.3 Variable-Length Argument Lists

- The macros and definitions of the variable arguments header `<cstdarg>` provide the capabilities necessary to build functions with variable-length argument lists.
- An ellipsis (…) in a function prototype indicates that the function receives a variable number of arguments.
- Type `va_list` is suitable for holding information needed by macros `va_start`, `va_arg` and `va_end`. To access the arguments in a variable-length argument list, an object of type `va_list` must be declared.
- Macro `va_start` is invoked before the arguments of a variable-length argument list can be accessed. The macro initializes the object declared with `va_list` for use by macros `va_arg` and `va_end`.
- Macro `va_arg` expands to an expression of the value and type of the next argument in the variable-length argument list. Each invocation of `va_arg` modifies the `va_list` object so that the object points to the next argument in the list.
- Macro `va_end` facilitates a normal return from a function whose variable argument list was referred to by the `va_start` macro.

### Section F.4 Using Command-Line Arguments

- On many systems—UNIX, LINUX, Mac OS X and Windows in particular—it is possible to pass command-line arguments to `main` by including in `main`’s parameter list the parameters `argc` and `argv[]`. Parameter `argc` is the number of command-line arguments. Parameter `argv` is an array of `char *`’s containing the command-line arguments.

### Section F.5 Notes on Compiling Multiple-Source-File Programs

- A function definition must be entirely contained in one file—it cannot span two or more files.
- Global variables must be declared in each file in which they are used.
- Function prototypes can be used to declare functions in other program files. (The `extern` specifier is not required in a function prototype.) This is accomplished by including the function prototype in each file in which the function is invoked, then linking the compiled files together.
- The storage-class specifier `static`, when applied to a global namespace scope variable or a function, prevents it from being used by any function that is not defined in the same file. This is referred to as internal linkage. Global variables and functions that are not preceded by `static` in their definitions have external linkage—they can be accessed in other files if those files contain proper declarations and/or function prototypes.
- The `static` specifier is commonly used with utility functions that are called only by functions in a particular file. If a function is not required outside a particular file, the principle of least privilege should be enforced by using `static`.
- When building large programs from multiple source files, compiling the program becomes tedious if making small changes to one file means that the entire program must be recompiled. Many systems provide special utilities that recompile only the modified program file. On UNIX systems, the utility is called `make`. Utility `make` reads a file called `Makefile` that contains instructions for compiling and linking the program.

### Section F.6 Program Termination with exit and atexit

- Function `exit` forces a program to terminate as if it had executed normally.
- Function `atexit` registers a function to be called upon normal termination of the program—i.e., either when the program terminates by reaching the end of `main`, or when `exit` is invoked.
- Function `atexit` takes a pointer to a function (e.g., a function name) as an argument. Functions called at program termination cannot have arguments and cannot return a value.
- Function `exit` takes one argument—normally the symbolic constant `EXIT_SUCCESS` or the symbolic constant `EXIT_FAILURE`. If `exit` is called with `EXIT_SUCCESS`, the implementation-defined value for successful termination is returned to the calling environment. If `exit` is called with `EXIT_FAILURE`, the implementation-defined value for unsuccessful termination is returned.
