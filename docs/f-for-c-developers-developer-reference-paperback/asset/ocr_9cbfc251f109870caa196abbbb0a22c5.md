# Compiler Directives

FSI is a feature to when you want to execute small programs. However, it is not a good choice for building executable binaries. To build binaries, you need to use Visual Studio. We'll use it to create one of the projects previously mentioned in this chapter. The builder and execution process is largely the same for F# and C# applications, although they have different compilers. I already presented the FSI directives, and I will now list the F# compiler directives. The following five directives are supported by F#:

+   * if is used for conditional compilation. The syntax is if <symbol>. If the symbol is defined by the compiler, the code after if is included in the compilation, as shown in Listing 1-18.
* else is used for conditional compilation. If the symbol is not defined, the code after else is included in the compilation, as shown in Listing 1-18.
* endif is used for conditional compilation, and it marks the end of the conditional compilation. This is also shown in Listing 1-18.
* line indicates the original source code line and file name.
* warning used to disable one or more warnings. F# tends to be more restrictive and gives more warnings than C# does. If your organization has a zero-warning policy, you can ignore specific warnings by using the warning directive. Only a number is needed as a suffix to a warning directive, and you can put multiple warning numbers in one line, as in the following example:
  warning "1" "2" "3"

LISTING 1-18 A conditional compilation

```
#if VERSION1
let f1 x y =
    printf "x: %d y: %d" x y
    x + y
#else
let f1 x y =
    printf "x: %d y: %d" x y
    x - y
#endif
```