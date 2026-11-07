```
```cpp
#ifndef NULL
    #define NULL 0
#endif
```
```

which determines whether the symbolic constant NULL is already defined. The expression `#ifndef NULL` includes the code up to `#endif` if NULL is not defined, and skips the code if NULL is defined. Every `#if` expression ends with `#endif`. Directives `#ifdef` and `#ifndef` are shorthand for `#if defined(name)` and `#if !defined(name)`. A multiple-part conditional preprocessor construct may be tested using the `#elif` (the equivalent of `else if` in an `if` structure) and the `#else` (the equivalent of `else` in an `if` structure) directives.

During program development, programmers often find it helpful to “comment out” large portions of code to prevent it from being compiled. If the code contains C-style comments, `/*` and `*/` cannot be used to accomplish this task, because the first `*/` encountered would terminate the comment. Instead, you can use the following preprocessor construct:

```
```cpp
#if 0
    code prevented from compiling
#endif
```
```

To enable the code to be compiled, simply replace the value 0 in the preceding construct with the value 1.

Conditional compilation is commonly used as a debugging aid. Output statements are often used to print variable values and to confirm the flow of control. These output statements can be enclosed in conditional preprocessor directives so that the statements are compiled only until the debugging process is completed. For example,

```
```cpp
#ifdef DEBUG
    cerr << "Variable x = " << x << endl;
#endif
```
```

causes the `cerr` statement to be compiled in the program if the symbolic constant DEBUG has been defined before directive `#ifdef DEBUG`. This symbolic constant is normally set by a command-line directive or by settings in the IDE (e.g., Visual Studio) and not by an explicit `#define` definition. When debugging is completed, the `#define` directive is removed from the source file, and the output statements inserted for debugging purposes are ignored during compilation. In larger programs, it might be desirable to define several different symbolic constants that control the conditional compilation in separate sections of the source file.

> > **Common Programming Error E.5**
> >
> > Inserting conditionally compiled output statements for debugging purposes in locations where C++ currently expects a single statement can lead to syntax errors and logic errors. In this case, the conditionally compiled statement should be enclosed in a compound statement. Thus, when the program is compiled with debugging statements, the flow of control of the program is not altered.

![](bbox=[0.159, 0.74, 0.22, 0.796])

# E.6 #error and #pragma Preprocessor Directives

The `#error` directive

```
```cpp
#error tokens
```
```