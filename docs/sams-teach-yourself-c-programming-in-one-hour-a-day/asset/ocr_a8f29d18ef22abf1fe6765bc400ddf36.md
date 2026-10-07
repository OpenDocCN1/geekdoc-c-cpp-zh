# Error-Handling

The C standard library contains a variety of functions and macros that help you deal with program errors.

# The assert() Macro

The macro assert() can diagnose program bugs. It is defined in assert.h, and its prototype is

```
void assert(int expression);
```

The argument expression can be anything you want to test—a variable or any C expression. If expression evaluates to TRUE, assert() does nothing. If expression evaluates to FALSE, assert() displays an error message on stderr and aborts program execution.

How do you use assert()? It is most frequently used to track program bugs (which are distinct from compilation errors). A bug doesn't prevent a program from compiling, but it causes the program to get incorrect results or run improperly (locking up, for example). For instance, a financial-analysis program you're writing might occasionally give incorrect answers. You suspect that the problem is caused by the variable interest_rate taking a negative value, which should never happen. To check this, place the statement

```
assert(interest_rate >= 0);
```

at locations in the program where interest_rate is used. If the variable ever becomes negative, assert() alerts you. You can then examine the relevant code to find the cause of the problem.

To see how assert() works, run Listing 20.3. If you enter a nonzero value, the program displays the value and terminates normally. If you enter zero, the assert() macro forces abnormal program termination. The exact error message you see depends on your compiler, but here's a typical example:

```
Assertion failed: x, file list1903.c, line 13
```

Note that, for assert() to work, your program must be compiled in debug mode. Refer to your compiler documentation for information on enabling debug mode (as explained in a moment). When you later compile the final version in release mode, the assert() macros are disabled.