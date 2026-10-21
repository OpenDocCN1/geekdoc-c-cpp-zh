```
Argument 1: trying
Argument 2: multiple
Argument 3: argument values
Argument 4: 4.5
Argument 5: 0.0
```

# How It Works

From the output, you can see that one difference between this and the native C++ version is that you don’t get the program name passed to main() — not really a great disadvantage, really a positive feature in most circumstances. Accessing the command line arguments is now a trivial exercise involving just iterating through the elements in the args array.

# Summary

In this chapter, you learned about the basics of program structure. You should have a good grasp of how functions are defined, how data can be passed to a function, and how results are returned to a calling program. Functions are fundamental to programming in C++, so everything you do from here on will involve using multiple functions in a program. The key points that you should keep in mind about writing your own functions are these:

+   - Functions should be compact units of code with a well-defined purpose. A typical program will consist of a large number of small functions, rather than a small number of large functions.
+   - Always provide a function prototype for each function defined in your program, positioned before you call that function.
+   - Passing values to a function using a reference can avoid the copying implicit in the call-by-value transfer of arguments. Parameters that are not modified in a function should be specified as const.
+   - When returning a reference or a pointer from a native C++ function, ensure that the object being returned has the correct scope. Never return a pointer or a reference to an object that is local to a native C++ function.
+   - In a C++/CLI program there is no problem with returning a handle to memory that has been allocated dynamically because the garbage collector takes care of deleting it when it is no longer required.
+   - When you pass a C++/CLI array to a function, there is no need for another parameter for the length of the array, as the number of elements is available in the function body as the Length property for the array.

The use of references as arguments is a very important concept, so make sure you are confident about using them. You’ll see a lot more about references as arguments to functions when we look into object-oriented programming.