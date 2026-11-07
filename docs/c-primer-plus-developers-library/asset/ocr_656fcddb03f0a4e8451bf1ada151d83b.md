# # Converting to ISO Standard C++

You might have programs (or programming habits) that you developed in C or in older versions of C++ and you want to convert to standard C++. This appendix provides some guidelines. Some pertain to moving from C to C++, and others pertain to moving from older C++ to standard C++.

# ## Use Alternatives for Some Preprocessor Directives

The C/C++ preprocessor provides an array of directives. In general, C++ practice is to use those directives that are designed to manage the compilation process and to avoid using directives as a substitute for code. For example, the #include directive is an essential component for managing program files. Other directives, such as #ifndef and #endif, let you control whether particular blocks of code get compiled. The #pragma directive lets you control compiler-specific compilation options. These are all useful, sometimes necessary, tools. You should exercise caution, however, when it comes to the #define directive.

# ## Use const Instead of #define to Define Constants

Symbolic constants make code more readable and maintainable. The constant's name indicates its meaning, and if you need to change the value, you just have to change the value once, in the definition, and then recompile. C uses the preprocessor to create symbolic names for a constant:

```
```c
#define MAX_LENGTH 100
```
```

The preprocessor then does a text substitution in your source code, replacing occurrences of MAX_LENGTH with 100 prior to compilation.

The C++ approach is to apply the const modifier to a variable declaration:

```
```c
const int MAX_LENGTH = 100;
```
```