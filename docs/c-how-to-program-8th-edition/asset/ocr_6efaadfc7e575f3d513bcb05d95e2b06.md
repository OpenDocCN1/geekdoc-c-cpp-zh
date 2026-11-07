+   - Type `va_list` is suitable for holding information needed by macros `va_start`, `va_arg` and `va_end`. To access the arguments in a variable-length argument list, an object of type `va_list` must be declared.
+   - Macro `va_start` is invoked before the arguments of a variable-length argument list can be accessed. The macro initializes the object declared with `va_list` for use by macros `va_arg` and `va_end`.
+   - Macro `va_arg` expands to an expression of the value and type of the next argument in the variable-length argument list. Each invocation of `va_arg` modifies the `va_list` object so that the object points to the next argument in the list.
+   - Macro `va_end` facilitates a normal return from a function whose variable argument list was referred to by the `va_start` macro.

# Section F.4 Using Command-Line Arguments

+   - On many systems—UNIX, LINUX, Mac OS X and Windows in particular—it is possible to pass command-line arguments to `main` by including in `main`’s parameter list the parameters `argc` and `argv[]`. Parameter `argc` is the number of command-line arguments. Parameter `argv` is an array of `char *`’s containing the command-line arguments.

# Section F.5 Notes on Compiling Multiple-Source-File Programs

+   - A function definition must be entirely contained in one file—it cannot span two or more files.
+   - Global variables must be declared in each file in which they are used.
+   - Function prototypes can be used to declare functions in other program files. (The `extern` specifier is not required in a function prototype.) This is accomplished by including the function prototype in each file in which the function is invoked, then linking the compiled files together.
+   - The storage-class specifier `static`, when applied to a global namespace scope variable or a function, prevents it from being used by any function that is not defined in the same file. This is referred to as internal linkage. Global variables and functions that are not preceded by `static` in their definitions have external linkage—they can be accessed in other files if those files contain proper declarations and/or function prototypes.
+   - The `static` specifier is commonly used with utility functions that are called only by functions in a particular file. If a function is not required outside a particular file, the principle of least privilege should be enforced by using `static`.
+   - When building large programs from multiple source files, compiling the program becomes tedious if making small changes to one file means that the entire program must be recompiled. Many systems provide special utilities that recompile only the modified program file. On UNIX systems, the utility is called `make`. Utility `make` reads a file called `Makefile` that contains instructions for compiling and linking the program.

# Section F.6 Program Termination with exit and atexit

+   - Function `exit` forces a program to terminate as if it had executed normally.
+   - Function `atexit` registers a function to be called upon normal termination of the program—i.e., either when the program terminates by reaching the end of `main`, or when `exit` is invoked.
+   - Function `atexit` takes a pointer to a function (e.g., a function name) as an argument. Functions called at program termination can have arguments and cannot return a value.
+   - Function `exit` takes one argument—normally the symbolic constant `EXIT_SUCCESS` or the symbolic constant `EXIT_FAILURE`. If `exit` is called with `EXIT_SUCCESS`, the implementation-defined value for successful termination is returned to the calling environment. If `exit` is called with `EXIT_FAILURE`, the implementation-defined value for unsuccessful termination is returned.