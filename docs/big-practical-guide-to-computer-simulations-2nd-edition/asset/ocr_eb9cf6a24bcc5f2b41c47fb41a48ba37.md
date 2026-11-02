+   - `#include <header.h>`
+   
+     This will include a standard header file `header.h` (which is to be re-placed by a real file name) as provided by the operating system. Hence, the search for such files will usually take place in directories provided by the operating system. Basically, every program has to have a `#include <stdio.h>` at least. Other important standard header files to be included are `stdlib.h` and `math.h`.
+     When using the `-I` compiling option, one can specify additional directories, where the compiler searches for header files.
+   
+   - `#include "header.h"`
+   
+     This is used for your private and local header files. This means, the compiler will first look in the current directory for the header files. Only if they are not found there, it will look in the standard directories. More information on what you have to take into account when writing your own header files is given below.

The second important type of compiler directive is the definition of a macro. Macros are shortcuts for code sequences in programming languages. Their primary purpose is to allow computer programs to be written more quickly. But the main benefit comes from the fact that a more flexible software development becomes possible. By using macros appropriately, programs become better structured, more generally applicable, and less error-prone. Here, it is explained how macros are defined and used in C; a detailed introduction can be found in C textbooks such as Ref. [Kernighan and Ritchie (1988)]. Other high-level programming languages exhibit similar features.

In C a macro is constructed via the `#define` directive. Macros are processed in the preprocessing stage of the compiler. This directive has the form

```
```c
#define <name> <definition>
```
```

Each definition must be on one line, without other definitions or directives. If the definition exceeds one line, each line except the last one has to be ended with the backslash `\` symbol. The simplest form of a macro is a constant, e.g.

```
```c
#define PI 3.1415926536
```
```

You can use the same sort of names for macros as for variables. It is convention to use only upper-case letters for macros. A macro can be