**Answer: False.** Actually, the CERT guideline MSC30-C indicates that implementation-specific random-number generation functions must be used to ensure that the random numbers produced are not predictable.

# Summary

# Section 5.1 Introduction

+   - The best way to develop and maintain a large program is to divide (p. 180) it into several smaller pieces, each more manageable than the original program.

# Section 5.2 Modularizing Programs in C

+   - A function (p. 180) is invoked by a **function call** (p. 181), which specifies the function name and provides information (as arguments) that the function needs to perform its task.

# Section 5.3 Math Library Functions

+   - A function is invoked by writing its name followed by a left parenthesis, the argument (or a comma-separated list of arguments) and a right parenthesis.
+   - Each argument may be a constant, a variable or an expression.

# Section 5.4 Functions

+   - There are several motivations for “functionalizing” a program. The divide-and-conquer approach makes program development more manageable. Another is building new programs by using existing functions. Such software reusability is a key concept in object-oriented programming languages derived from C, such as C++, Java, C# (pronounced “C sharp”), Objective-C and Swift.
+   - With good function naming and definition, you can create programs from standardized functions that accomplish specific tasks, rather than custom code. This is known as abstraction. We use abstraction each time we use standard library functions like `printf`, `scanf` and `pow`. A third motivation is to avoid repeating code in a program. Packaging code as a function allows it to be executed from other program locations by calling that function.

# Section 5.5 Function Definitions

+   - The arguments passed to a function should match in number, type and order with the parameters (p. 185) in the function definition.
+   - When a program encounters a function call, control transfers from the point of invocation to the called function, the statements of that function execute, then control returns to the caller.
+   - A called function can return control to the caller in one of three ways. If the function does not return a value, control is returned when the function-ending right brace is reached, or by executing the statement
+   
+     ```c
+     return;
+     ```
+   
+     If the function does return a value, the statement
+   
+     ```c
+     return expression;
+     ```
+   
+     returns the value of `expression`.
+   - A local variable (p. 185) is known only in a function definition. Other functions are not allowed to know the names of a function’s local variables, nor is any function allowed to know the implementation details of any other function.