the value for a variable displayed in hexadecimal notation, you can either enter a hexadecimal number, or enter a decimal value prefixed by 0n (zero followed by n), so you could enter a value as A9, or as 0n169. If you just enter 169 it is interpreted as a hexadecimal value. Naturally, you should be cautious about flinging new values into your program willy-nilly. Unless you are sure you know what effect your changes are going to have, you may end up with a certain amount of erratic program behavior, which is unlikely to get you closer to a working program.

You’ll probably find it useful to run a few more of the examples we have seen in previous chapters in debug mode. It enables you to get a good feel for how the debugger operates under various conditions. Monitoring variables and expressions is a considerable help in sorting out problems with your code, but there’s a great deal more assistance available for seeking out and destroying bugs. Take a look at how you can add code to a program that provides more information about when and why things go wrong.

# Adding Debugging Code

For a program involving a significant amount of code, you certainly need to add code that is aimed at highlighting bugs wherever possible and providing tracking output to help you pin down where the bugs are. You don’t want to be in the business of single stepping through code before you have any idea of what bugs there are, or which part of the code is involved. Code that does this sort of thing is only required while you are testing a program. You won’t need it after you believe the program is fully working, and you won’t want to carry the overhead of executing it or the inconvenience of seeing all the output in a finished product. For this reason, code that you add for debugging only operates in the debug version of a program, not in the release version (provided you implement it in the right way, of course).

The output produced by debug code should provide clues as to what is causing a problem, and if you have done a good job of building debug code into your program, it will give you a good idea of which part of your program is in error. You can then use the debugger to find the precise nature and location of the bug, and fix it.

The first way you can check the behavior of your program that you will look at is provided by a C++ library function.

# Using Assertions

The standard library header <cassert> declares the assert() function that you can use to check logical conditions within your program when a special preprocessor symbol, NDEBUG, is not defined. The function is declared as:

```
void assert(int expression);
```

The argument to the function specifies the condition to be checked, but the effect of the assert() function is suppressed if a special preprocessor symbol, NDEBUG, is defined. The symbol NDEBUG is automatically defined in the release version of a program, but not in the debug version. Thus an assertion checks its argument in the debug version of a program but does nothing in a release version. If you want to switch off assertions in the debug version of a program, you can define NDEBUG explicitly yourself using a #define directive. To be effective, you must place the #define directive for NDEBUG preceding the #include directive for the <cassert> header in the source file: