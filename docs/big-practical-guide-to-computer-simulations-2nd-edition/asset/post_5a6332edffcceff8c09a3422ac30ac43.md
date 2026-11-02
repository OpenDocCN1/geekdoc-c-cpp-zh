
## 1.5 Important C compiler options

Throughout this book, many C compiler options are explained which are useful or even necessary for some tasks. Here, they are summarized:

`-o` sets the name of the output file, e.g. like in `cc -o first first.c`

`-c` Just the compile process is performed, no final executable is linked. Each .c file will result in a corresponding .o file. This is useful in case the source code contains some functions which are used in several different programs. This process can be made automatic using *make* files, see Sec. 2.1.

`-l` states the name of a library where some precompiled functions can be found, e.g. for mathematical functions (m) in `cc -o mathtest mathtest.c -lm`

`-Wall` Switches on (almost) all compiler warnings, e.g. indicates if one uses `=' inside a condition instead of `=='.

`-Wextra` Switches on additional compiler warnings, e.g. indicates if one compares variables of different types.

`-Wshadow` When using this option, the compiler will warn if a local definition shadows a global definition, e.g. in case there are two variables of the same name (see page 44).

`-g` Switches on support for debuggers, see Sec. 4.1.

`-pg` Switches on support for profiling, i.e. for measuring where the program spends how much running time, see Sec. 4.4.

`-O` Switches on optimization of the code. This means it will run faster. For example, the compiler may "unroll" loops where the number of iterations is fixed. Also, it writes the code of a function inline instead of calling the function (can be forced via the `inline` directive at the beginning of a function definition). It can get rid of intermediate expressions/find common subexpression. Furthermore, it can decide to

- `#include <header.h>`

This will include a standard header file `header.h` (which is to be replaced by a real file name) as provided by the operating system. Hence, the search for such files will usually take place in directories provided by the operating system. Basically, every program has to have a `#include <stdio.h>` at least. Other important standard header files to be included are `stdlib.h` and `math.h`.
When using the `-I` compiling option, one can specify additional directories, where the compiler searches for header files.

- `#include "header.h"`

This is used for your private and local header files. This means, the compiler will first look in the current directory for the header files. Only if they are not found there, it will look in the standard directories. More information on what you have to take into account when writing your own header files is given below.

The second important type of compiler directive is the definition of a macro. Macros are shortcuts for code sequences in programming languages. Their primary purpose is to allow computer programs to be written more quickly. But the main benefit comes from the fact that a more flexible software development becomes possible. By using macros appropriately, programs become better structured, more generally applicable, and less error-prone. Here, it is explained how macros are defined and used in C; a detailed introduction can be found in C textbooks such as Ref. [Kernighan and Ritchie (1988)]. Other high-level programming languages exhibit similar features.

In C a macro is constructed via the `#define` directive. Macros are processed in the preprocessing stage of the compiler. This directive has the form

```c
#define <name> <definition>
```

Each definition must be on one line, without other definitions or directives. If the definition exceeds one line, each line except the last one has to be ended with the backslash `\` symbol. The simplest form of a macro is a constant, e.g.

```c
#define PI 3.1415926536
```

You can use the same sort of names for macros as for variables. It is convention to use only upper-case letters for macros. A macro can be deleted via the #undef directive.

When scanning the code, the preprocessor just replaces literally every occurrence of a macro by its definition. If you have, for example, the expression 2.0*PI*omega in your code, the preprocessor will convert it into 2.0*3.1415926536*omega. You can use macros also in the definition of other macros. But macros are not replaced in strings, i.e. printf("PI"); will print PI and not 3.1415926536 when the program is run.

It is possible to test for the (non)existence of macros using the #ifdef and #ifndef directives. This allows for conditional compiling or for platform-independent code, such as in

```
#ifdef UNIX
...
#endif
#ifdef MSDOS
...
#endif
```

Please note that it is possible to supply definitions of macros to the compiler via the -D option, e.g. cc -o program program.c -DUNIX=1. If a macro is used only for conditional #ifdef/#ifndef statements, an assignment like =1 can be omitted, i.e. -DUNIX is sufficient.

When programs are divided into several modules, or when library functions are used, the definitions of data types and functions are provided in header files (.h files), as mentioned above. It is important that each header file should be read by the compiler only once for each source code file, otherwise declarations will appear twice and the compiler will complain. When projects become more complex, many header files have to be managed, and it may become difficult to avoid multiple scanning of some header files. This can be prevented automatically by this simple construction using macros:

```
/** example .h file: myfile.h **/

#ifndef _MYFILE_H_
#define _MYFILE_H_

  .... (rest of .h file)
  (may contain other #include directives)

#endif /* _MYFILE_H_ */
```

After the body of the header file has been read the first time during a compilation process, the macro _MYFILE_H_ is defined, thus the body will never be read again.

So far, macros are just constants. You will benefit from their full power when using macros with arguments. They are given in braces after the name of the macro, such as in

```
#define   MIN(x,y)   ( (x)<(y) ?  (x):(y) )
```

You do not have to worry more than usual about the names you choose for the arguments, there cannot be a conflict with other variables of the same name, because they are replaced by the expression you provide when a macro is used, e.g. MIN(4*a, b-32) will be expanded to (4*a)<(b-32) ? (4*a):(b-32).

The arguments are used in (  ) braces in the macro, because the comparison < must have the lowest priority, regardless of which operators are included in the expressions that are supplied as actual arguments. Furthermore, you should take care of unexpected side effects. Macros do not behave like functions. For example, when calling MIN(a++,b++) the variable a or b may be increased twice when the program is executed. It is usually better to use inline functions (or sometimes templates in C++) in such cases. But there are many applications of macros, which cannot be replaced by inline functions, like in the following example, which closes this section.

The example illustrates how a program can be written in a clear way using macros, making the program less error-prone, and furthermore allowing for a broad applicability. A system of Ising spins is considered, i.e., a lattice where at each site i a particle σ_i is placed. Each particle can have only two states σ_i = ±1. It is assumed that all lattice sites are numbered from 1 to N. This is different from C arrays, which start at index 0. The benefit of starting with index 1 for the sites is that, for many simulations of Ising systems, one needs the site 0 for additional technical reasons, see below. For the simplest version of the model only neighbors of spins are interacting. With a two-dimensional square lattice of size N = L × L a spin i, which is not at the boundary, interacts with spins i + 1 (+x-direction), i − 1 (−x-direction), i + L (+y-direction), and i − L (−y-direction). A spin at the boundary may interact with fewer neighbors when free boundary conditions are assumed. With periodic boundary conditions (pbc), all spins have exactly 4 neighbors. In this case, a spin at the boundary interacts
