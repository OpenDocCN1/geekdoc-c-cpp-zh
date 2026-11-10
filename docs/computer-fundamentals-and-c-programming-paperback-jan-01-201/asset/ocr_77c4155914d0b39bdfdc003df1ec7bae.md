This task can't be performed by the `if` statement because OS would be expanded before it can be tested. `#if` can also be used with the logical operators (`||` and `&&`) to test complex conditions. Furthermore, using the `defined` operator, `#if` can also check whether a symbolic constant or macro is defined or not:

```
```c
#if (OS == 1 || OS == 2)
#if defined UNIX
#if !defined UNIX            Negates previous test
```
```

The two preceding examples replicate the behavior of the `#ifdef` and `#ifndef` directives. Even though `#if` and `if` have a lot in common, some features of `if` are not available in `#if`. For instance, `sizeof` and casts can't be used with `#if`.

# 17.3 USING #ifdef FOR DEBUGGING PROGRAMS

If a separate debugger program is not used, the standard technique of debugging programs is to display variables at key program locations. These print statements help determine whether a code section is working properly. After the debugging exercise is over, these lines are either deactivated by commenting them or removed altogether. A better solution would be to use the conditional compilation feature that makes debugging convenient.

We can use the `#ifdef` feature to print a diagnostic statement depending on whether a named constant is defined or not:

```
```c
#ifdef DEBUG
    fprintf(stderr, "Value of x = %d\n", x);
#endif
```
```

In the testing phase, we can insert either of the following statements at the beginning of the preprocessor section to enable execution of DEBUG-dependent statements:

```
```c
#define DEBUG 1
#define DEBUG                  DEBUG is considered defined
```
```

Once the code has been finalized, you need not remove this directive; simply add the following directive after the previous one:

```
```c
#undef DEBUG
```
```

Can't this task be achieved using a variable and checking its value with the `if` statement? Sure it can, but the solution provided by the preprocessor is more efficient because DEBUG-related code will be ignored by the compiler if DEBUG is not defined. The size of the executable is thus trimmed, which won't happen when a variable is used instead.

Most C compilers also provide a separate option to set a named constant at the time of compilation. When using the GCC compiler, simply define DEBUG in the command line using the -D option:

```
```bash
gcc -D DEBUG foo.c
```
```

With Visual Studio, use the /D switch:

```
```bash
cl /DDEBUG foo.c
```
```