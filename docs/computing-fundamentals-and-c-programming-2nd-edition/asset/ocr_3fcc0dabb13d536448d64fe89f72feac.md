4. Suppose you are in the process of testing your program, which is rather a large one. You would like to have print calls inserted in certain places to display intermediate results and messages in order to trace the flow of execution and errors, if any. Such statements are called 'debugging' statements. You want these statements to be a part of the program and to become 'active' only when you decide so.

One solution to these problems is to develop different programs to suit the needs of different situations. Another method is to develop a single, comprehensive program that includes all optional codes and then directs the compiler to skip over certain parts of source code when they are not required. Fortunately, the C preprocessor offers a feature known as *conditional compilation*, which can be used to 'switch' on or off a particular line or group of lines in a program.

# **Situation 1**

This situation refers to the conditional definition of a macro. We want to ensure that the macro TEST is always defined, irrespective of whether it has been defined in the header file or not. This can be achieved as follows:

```
```c
#include "DEFINE.H"
#ifndef TEST
#define TEST 1
#endif
```
```

**DEFINE.H** is the header file that is supposed to contain the definition of **TEST** macro. The directive.

```
```c
#ifdef TEST
```
```

searches for the definition of **TEST** in the header file and *if not defined*, then all the lines between the **#ifdef** and the corresponding **#endif** directive are left 'active' in the program. That is, the preprocessor directive

`# define TEST` is processed.

In case, the TEST has been defined in the header file, the #ifdef condition becomes false, therefore the directive **#define TEST** is ignored. Remember, you cannot simply write

```
```c
# define TEST 1
```
```

because if **TEST** is already defined, an error will occur.

Similar is the case when we want the macro **TEST** never to be defined. Looking at the following code:

```
```c
#ifdef TEST
#undef TEST
#endif
```
```

This ensures that even if **TEST** is defined in the header file, its definition is removed. Here again we cannot simply say

```
```c
#undef TEST
```
```

because, if TEST is not defined, the directive is erroneous.

# **Situation 2**

The main concern here is to make the program portable. This can be achieved as follows:

```
```c
....
main()
```
```