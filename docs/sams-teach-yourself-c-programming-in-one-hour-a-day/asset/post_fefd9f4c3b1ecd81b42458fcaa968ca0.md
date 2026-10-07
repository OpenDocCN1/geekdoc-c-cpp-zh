
screen.c for your screen display functions, and so on. To compile and link more than two modules, include all source files in your project.

The main module should contain main(), of course, and any other functions that are program-specific (meaning that they have no general utility).

There is usually one header file for each secondary module. Each file has the same name as the associated module, with an .h extension. In the header file, put

- Prototypes for functions in the secondary module
- #define directives for any symbolic constants and macros used in the module
- Definitions of any structures or external variables in the module

Because this header file might be included in more than one source file, you want to prevent portions of it from compiling more than once. You can do this by using the preprocessor directives for conditional compilation (discussed later in this lesson).

## External Variables and Modular Programming

In many cases, the only data communication between the main module and the secondary module is through arguments passed and returned from the functions. In this case, you don't need to take special steps regarding data visibility; but what about an external variable to be visible in multiple modules?

Recall from Lesson 12, "Understanding Variable Scope," that an external variable is one declared outside of any function. An external variable is visible throughout the entire source-code file in which it is declared. However, it is not automatically visible in all modules. To make it visible, you must declare the variable in each module, using the extern keyword. For example, if you have an external variable declared in the main module

```c
float interest_rate;
```

you make interest_rate visible in a secondary module by including the following declaration in that module (outside of any function):

```
extern float interest_rate;
```

The extern keyword tells the compiler that the original declaration of interest_rate (the one set aside storage space for it) is located elsewhere, but that the variable should be made visible in this module. All extern variables have static duration and are visible to all functions in the module. Figure 22.5 illustrates the use of the extern keyword in a multiple-module program.

## LESSON 22 Advanced Compiler Use

> CAUTION If you use extern declarations and then don't actually declare the variable elsewhere, you get an error. This error can occur either when you link the final program or at runtime.

FIGURE 22.5
Using the extern keyword to make an external variable visible across modules.

```c
/* main module */
int x, y;
main() {
...
}
```

```
/* secondary mod1.c */
extern int x, y;
funcl() {
...
}
```

```
/* secondary mod2.c */
extern int x;
func4() {
...
}
```

In Figure 22.5, the variable x is visible throughout all three modules. In contrast, y is visible only in the main module and secondary module 1.

| DO | DON'T |
|---|---|
| DO create generic functions in their own source files. This way, they can be linked into any other programs that need them. | DON'T try to compile multiple source files together if more than one module contains a main() function. You can have only one main(). (You can have only one function of any name.) |
| DON'T always use the C source files when compiling multiple files together. If you compile a source file into an object file, recompile only when the file changes. This saves a great deal of time. | |

## The C Preprocessor

The preprocessor is a part of all C compiler packages. When you compile a C program, the preprocessor is the first compiler component that processes your program. In most compilers, the preprocessor is part of the compiler program. When you run the compiler, it automatically runs the preprocessor.

The preprocessor changes your source code based on instructions, or *preprocessor directives*, in the source code. The output of the preprocessor is a modified source-code file that is then used as the input for the next compilation. Normally, you never see this file because the compiler deletes it after it's used. However, later in this lesson, you need to learn about the preprocessor directives, which all begin with the # symbol.

## The #define Preprocessor Directive

The #define preprocessor directive has two uses: creating symbolic constants and creating macros.

## Simple Substitution Macros Using #define

You learned about substitution macros in Lesson 3, "Storing Information: Variables and Constants," although the term used to describe them in that lesson was *symbolic constants*. You create a substitution macro by using `#define` to replace text with other text. For example, to replace `text1` with `text2`, you write

```c
#define text1 text2
```

This directive causes the preprocessor to go through the entire source-code file, replacing every occurrence of `text1` with `text2`. The only exception occurs if `text1` is found within double quotation marks, in which case no change is made.

The most frequent use for substitution macros is to create symbolic constants, as explained in Lesson 3. For example, if your program contains the following lines:

```c
#define MAX 1000
x = y * MAX;
z = MAX - 12;
```

during preprocessing, the source code is changed to read as follows:

```c
x = y * 1000;
z = 1000 - 12;
```

The effect is the same as using your editor's search-and-replace feature to change every occurrence of MAX to 1000. Your original source-code file isn't changed, of course. Instead, a temporary copy is created with the changes. Note that #define isn't limited to creating symbolic numeric constants. For example, you can write

```c
#define ZINGBOFFLE printf(ZINGBOFFLE("Hello, world.");
```

although there is little reason to do so. You should also be aware that some authors refer to symbolic constants defined with #define as being macros themselves. (Symbolic constants are also called manifest(constants).) However, in this book, the word macro is reserved for the type of construction description next.

## Creating Function Macros with #define

You can use the #define directive to create function macros. A function macro is a type of shorthand, using something to represent something more complicated. The reason for the "function" name is that this macro can accept arguments, just like a real C function does. One advantage of function macros is that their arguments aren't type-sensitive. Therefore, you can pass any numeric variable type to a function macro that expects its argument.

Now look at an example. The preprocessor directive

```c
#define HALFOF(value) ((value)/2)
```

defines a macro named HALFOF that takes a parameter named value. Whenever the preprocessor encounters HALFOF(value) in the source code, it replaces it with the argument. Thus, the program

```c
result = HALFOF(10);
```

is replaced by the following:

```c
result = (10)/2;
```

A macro can have more than one parameter, and each parameter can be used multiple times. For example, the following macro, which calculates the average of five values, has five parameters:

```c
#define AVGS(v, w, x, y, z) ((v)+(w)+(x)+(y)+(z)/5
```
