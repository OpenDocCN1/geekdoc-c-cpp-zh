```
```c
#define SIZE 20
#endif
```
```

… but its value has to be changed

This situation can arise when including a `.h` file (say, `foo.h`) without knowing whether SIZE has been defined there. The **#ifndef** section ensures SIZE is set to 20, but do we really need the **#else** segment? Yes, we do if we need to reset SIZE to a different value (*17.2*). We may not remember the existing value of SIZE (if defined at all), so the **#undef-#define** sequence ensures that SIZE is properly set.

The **#else** option is needed when designing code for two operating systems. The following form lets you select the code to be executed depending on whether UNIX is defined or not:

```
```c
#ifdef UNIX
  ... code ...
#else
  ... code ...
#endif
```
```

How do you extend this logic to work with more than two operating systems? You simply can’t except by using multiple **#ifdef-#else-#endif** constructs. A better method would be to use the **#if-#elif-#else-#endif** feature introduced by C89.

> Note: **#ifdef** and **#ifndef** work only with named constants and macros. They can’t be used to check whether a variable is defined or not. The `if` statement in C can’t perform this check either.

# 17.7.2  The #if and #elif Directives

The **#if-#elif** duo behaves much like the `if-elif` statement of C in two ways. First, the construct permits multi-way branching, unlike **#ifdef** which restricts the number of options to two. Second, **#if** evaluates a constant control expression using the following syntax:

```
```c
#if expression1 is true
    directives1 or statements1
#elif expression2 is true
    directives2 or statements2
...
#else
    directives3 or statements3
#endif
```
```

Use of parentheses to enclose the expression is optional. Like the `if` statement, **#if** also uses the relational and logical operators. This is how you use the preprocessor to test a symbolic constant for different values:

```
```c
#if OS == 1
    #define UNIX
#elif (OS == 2)
    #define WINDOWS
#else
    #define MAC_OS_X
#endif
```
```

Parentheses OK