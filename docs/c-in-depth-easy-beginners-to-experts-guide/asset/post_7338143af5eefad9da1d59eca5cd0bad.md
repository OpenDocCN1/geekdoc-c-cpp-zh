
The first step after typing in a program (or just a sub-unit of a program) is to compile the program. The compiling process converts the source code file you typed in into machine language and is stored in an object file. This is known as compiling.

With most systems, the object file is automatically linked with the system libraries. These libraries contain the code for the functions that are part of the language library. (For example, the C libraries contain the code for the `printf()` function.)

## 2.1 Compiler Errors

Every language has syntax rules. These rules determine which statements are legal in the language and which are not. Compiler programs are designed to enforce these rules. When a rule is broken, the compiler prints an error message and an object file is not created.

Most compilers will continue scanning the source file after an error and report other errors it finds. However, once an error has been found, the compiler may be confused by later perfectly legal statements and report them as errors. This brings us to the first rule of compiler errors:

### First Rule of Compiler Errors

*The first listed compiler error is always a true error; however, later errors may not be true errors.*

Succeeding errors may disappear when the first error is removed. So, if later error messages are puzzling, ignore them. Fix the errors that you are sure are errors and re-compile. The puzzling errors may magically disappear when the other true errors are removed.

If you have many errors, the first error may scroll off the screen. One solution to this problem is to save the errors into a file using redirection. One problem is that errors are written to stderr, not stdout, which the `>` redirection operator uses.

To redirect output to stderr, use the `2>` operator.

### Here's an example:

```text
$cc x.c 2>errors
$more errors
```

The compiler is just a program that other humans created. Often the error messages it displays are confusing (or just plain wrong!). Do not assume that the line that an error message refers to is always the line where the true error actually resides.

The compiler scans source files from the top sequentially to the bottom.

Sometimes an error is not detected by the compiler until many lines below where the actual error is. Often the compiler is too stupid to realize this and refers to the line in the source file where it realized something is wrong. The true error is earlier in the code. This brings us to the second rule of compiler errors:

### Second Rule of Compiler Errors

> A compiler error may be caused by any source code line above the line referred to by the compiler; however, it cannot be caused by a line below.

In C (and C++), do not forget that the `#include` preprocessor statement inserts the code of a header file into the source file. An error in the header file may cause a compiler error referencing a line in the main source file.

Most systems allow the preprocessed code (that the C compiler actually compiles!) to be stored in a file. This allows you to see exactly what is being compiled. This file will also show how each C macro was expanded. This can be very helpful to discover the cause of normally very hard to find errors.

A useful technique for finding the cause of puzzling compiler errors is to delete (or comment out) preceding sections of code until the error disappears. When the error disappears, the last section removed must have caused the error.

The compiler can also display warnings. A warning is not a syntax error; however, it may be a logical error in the program. It marks a statement in your program that is legal, but is suspicious.

You should treat warnings as errors unless you understand why the warning was generated. Often compilers can be set to different warning levels. It is to your advantage to set this level as high as possible, to have the compiler give as many warnings as possible. Look at these warnings very carefully!

### Brain Wash Drill

**Remember** that just because a program compiles with no errors or warnings does not mean that the program is correct! It only means that every line of the program is syntactically correct. That is, the compiler understands what each statement says to do. The program may still have many logical errors! An English paper may be grammatically correct (i.e., have nouns, verbs, etc. in the correct places), but be gibberish.

## 2.2 Linker Errors

The linker is a program that links object files (which contain the compiled machine code from a single source file) and libraries (which are files that are collections of object files) together to create an executable program. The linker matches up functions and global variables used in object files to their definitions in other object files. The linker uses the name (often the term symbol is used) of the function or global variable to perform the match.

The most common type of linker error is an unresolved symbol or name. This error occurs when a function or global variable is used, but the linker cannot find a match for the name. For example, on an IBM AIX system, the error message looks like this: 0706-317 ERROR: Unresolved or undefined symbols detected:

Symbols in error (followed by references) are dumped to the load map. The `-bloadmap:<filename>` option will create a load map..fun

This message means that a function (or global variable) named fun (ignore the period) was referenced in the program, but never defined. There are two common causes of these errors:

- **Misspelling the name of the function**

  In the example above, there was a function named func. This is not a compiler error. Code in one source file can use functions defined in another. The compiler assumes that any function referenced, but not defined in the file that references it, will be defined in another file and linked. It is only at the link stage that this assumption can be checked. (Note that C++ compilers will usually generate compiler errors for this, since C++ requires prototypes for all referenced functions!)

- **The correct libraries or object files were not linked**

  The linker must know what libraries and object files are needed to form the executable program. The standard C libraries are automatically linked. UNIX systems, like the AIX system, do not automatically link in the standard C math library! To link in the math library on the AIX system, use the `-lm` flag on the compile command. For example, to compile a C program that uses `sqrt`, type: `cc prog.c -lm`. Remember that the `#include` statement only inserts text into source files. It is a common myth that it also links in the appropriate library! The linker never sees this statement!

There are also bugs related to the linker. One difficult bug to uncover occurs when there are two definitions of a function or global variable. The linker will pick the first definition it finds and ignores the other. Some linkers will display a warning message when this occurs (The AIX linker does not!).

Another bug related to linking occurs when a function is called with the wrong arguments. The linker only looks at the name of the function when matching. It does no argument checking. Here's an example:

File: x.c

```c
int f( int x, int y)
{
    return x + y;
}
```

File: y.c

```c
int main()
{
    int s = f(3);
    return 0;
}
```

These types of bugs can be prevented by using prototypes. For example, if the prototype: `int f( int, int);` is added to y.c, the compiler will catch this error. Actually, the best idea is to put the prototype in a header file and include it in both x.c and y.c. Why use a header file?

So that there is only one instance of the prototype that all files use. If a separate instance is typed into each source file, there is no guarantee that each instance is the same.

If there is only one instance, it cannot be inconsistent with itself! Why include it in x.c (the file the function is defined in)? So that the compiler can check the prototype and ensure that it is consistent with the function's definition. (Additional note: C++ uses a technique called name mangling to catch these types of errors.)

## 3. Runtime Errors

A runtime error occurs when the program is running and usually results in the program aborting. On a UNIX/Linux system, an aborting program creates a coredump.

A coredump is a binary file named `core` that contains information about the state of the program when it aborted. Debuggers like gdb and dbx can read this file and tell you useful information about what the program was doing when it aborted. There are several types of runtime errors:

### Illegal memory access
