+   - An assignment statement is a replacement statement: `a = b;` replaces the value of a with the value of b.
+   - Assignment is a value-producing operator that returns the value being assigned. This together with right-associativity makes it possible to chain assignments; for example, `a = b = c = d;`.
+   - An assignment statement of the form `alpha = alpha Δ beta;` can be written more compactly as `alpha Δ= beta;`.
+   - The increment (`++`) and decrement (`--`) operations are useful for incrementing/decrementing an integer variable by 1.
+   - I/O is carried out in C++ by operators acting on streams (`istream`s for input and `ostream`s for output), which connect an executing program with an input/output device.
+   - Input statements of the form
+   
+     ```cpp
+     an_istream >> variable_1 >> variable_2 >> ... >> variable_n;
+     ```
+   
+     are used to input values for variables; `cin` is the istream associated with the keyboard. White space (spaces, tabs, or newlines) is used to separate input values. Leading white space will be ignored when reading a value for a variable.
+   - It is good practice to prompt the user with an informative message when data values are to be entered.
+   - Output statements of the form
+   
+     ```cpp
+     an_ostream << expr_1 << expr_2 << ... << expr_n;
+     ```
+   
+     are used to output values of expressions; `cout` and `cerr` are ostreams associated with the screen.
+   - The format of output is controlled by inserting format manipulators into output lists.

# Style and Design Tips

In the examples in this text, we adopt certain stylistic guidelines for C++ programs, and you should write your program in a similar style. Those at the end of Chapter 3 are important ones and you should review them.

# Warnings

+   1. The type of value stored in a variable should be the same as or promotable to the type of that variable.
+   2. If an integer value is to be stored in a real variable, the integer will be promoted to a real type. By contrast, if a real value is to be stored in an integer variable, then the real value is truncated, possibly resulting in the loss of information.