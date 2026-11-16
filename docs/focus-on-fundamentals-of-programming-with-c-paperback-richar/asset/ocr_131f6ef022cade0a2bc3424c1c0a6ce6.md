# Separate Compilation

C does not require that all of the statements for a particular program be contained within a single file. C programs can be constructed from functions written in separate files and linked into a single program. Up until this point, all of our C source code for each project has been placed within a single .c file. But now, as our programs become longer and longer, we will need to find a more efficient way to organize our code.

We can compile a source file to create "object code" and can link its functions with other functions in other source files. If a function from one file needs to call a function contained inside another file, then the function call can be made in the normal fashion and arguments can be passed and returned in the usual way. As we are revising and debugging a program, it's easier if each compilation processes only part of the large program. Once we have written and debugged a function, we do not need to keep recompiling it as we work on other functions in the program.

Consider the following two C source files:

| File 1 | File 2 |
|---|---|
| `int main(void) {` | `void faa(void) {` |
| ` foo();` | ` puts("Green");` |
| ` faa();` | ` }` |
| `}` | |
| `void foo(void) {` | |
| ` puts("Red");` | |
| `}` | |

The C compiler finds the two function calls in File 1. The reference to `foo()` is resolved when the definition of `foo()` is found in the same file. The reference to `faa()` is resolved when the definition of `faa()` is found in File 2. All object files specified to the C compiler will be "pulled into" the C compiler and are automatically included in the final executable file.

In the case of our linked list declarations and functions, we create two files, `list.h` and `list.c`. The `.h` file is called a header file and typically contains declarations as well as function prototypes. Here is what the header file would look like for our linear linked list: