
| Location in text | Recursion examples and exercises |
|---|---|
| *Chapter 19* |  |
| Section 19.6, Figs. 19.20–19.22 | Binary tree insert |
| Section 19.6, Figs. 19.20–19.22 | Preorder traversal of a binary tree |
| Section 19.6, Figs. 19.20–19.22 | Inorder traversal of a binary tree |
| Section 19.6, Figs. 19.20–19.22 | Postorder traversal of a binary tree |
| Exercise 19.20 | Print a linked list backward |
| Exercise 19.21 | Search a linked list |
| Exercise 19.22 | Binary tree delete |
| Exercise 19.23 | Binary tree search |
| Exercise 19.24 | Level order traversal of a binary tree |
| Exercise 19.25 | Printing tree |
| *Chapter 20* |  |
| Section 20.3.3, Fig. 20.6 | Mergesort |
| Exercise 20.8 | Linear search |
| Exercise 20.9 | Binary search |
| Exercise 20.10 | Quicksort |

**Fig. 6.32** | Summary of recursion examples and exercises in the text. (Part 2 of 2.)

## 6.23 Wrap-Up

In this chapter, you learned more about function declarations, including function prototypes, function signatures, function headers and function bodies. We overviewed the math library functions. You learned about argument coercion, or the forcing of arguments to the appropriate types specified by the parameter declarations of a function. We demonstrated how to use functions rand and srand to generate sets of random numbers that can be used for simulations. We showed how to define sets of constants with enums. You also learned about the scope of variables, storage-class specifiers and storage duration. Two different ways to pass arguments to functions were covered—pass-by-value and pass-by-reference. For pass-by-reference, references are used as an alias to a variable. We showed how to implement inline functions and functions that receive default arguments. You learned that multiple functions in one class can be overloaded by providing functions with the same name and different signatures. Such functions can be used to perform the same or similar tasks, using different types or different numbers of parameters. We demonstrated a simpler way of overloading functions using function templates, where a function is defined once but can be used for several different types. You then studied recursion, where a function calls itself to solve a problem.

In Chapter 7, you’ll learn how to maintain lists and tables of data in arrays and object-oriented vectors. You’ll see a more elegant array-based implementation of the dice-rolling application and two enhanced versions of the GradeBook case study we presented in Chapters 3–6 that will use arrays to store the actual grades entered.

- Compilers can inline code for which you have not explicitly used the `inline` keyword. Today’s optimizing compilers are so sophisticated that it’s best to leave inlining decisions to the compiler.

### Section 6.15 References and Reference Parameters

- When an argument is passed by value (p. 237), a copy of the argument’s value is made and passed to the called function. Changes to the copy do not affect the original variable’s value in the caller.
- With pass-by-reference (p. 237), the caller gives the called function the ability to access the caller’s data directly and to modify it if the called function chooses to do so.
- A reference parameter (p. 238) is an alias for its corresponding argument in a function call.
- To indicate that a function parameter is passed by reference, follow the parameter’s type in the function prototype and header by an ampersand (&).
- All operations performed on a reference are actually performed on the original variable.

### Section 6.16 Default Arguments

- When a function is called repeatedly with the same argument for a particular parameter, you can specify that such a parameter has a default argument (p. 240).
- When a program omits an argument for a parameter with a default argument, the compiler inserts the default value of that argument to be passed to the function call.
- Default arguments must be the rightmost (trailing) arguments in a function’s parameter list.
- Default arguments are specified in the function prototype.

### Section 6.17 Unary Scope Resolution Operator

- C++ provides the unary scope resolution operator (p. 242), `::`, to access a global variable when a local variable of the same name is in scope.

### Section 6.18 Function Overloading

- C++ enables several functions of the same name to be defined, as long as these functions have different sets of parameters. This capability is called function overloading (p. 243).
- When an overloaded function is called, the C++ compiler selects the proper function by examining the number, types and order of the arguments in the call.
- Overloaded functions are distinguished by their signatures.
- The compiler encodes each function identifier with the types of its parameters to enable type-safe linkage (p. 244). Type-safe linkage ensures that the proper overloaded function is called and that the types of the arguments conform to the types of the parameters.

### Section 6.19 Function Templates

- Overloaded functions typically perform similar operations that involve different program logic on different data types. If the program logic and operations are identical for each data type, overloading may be performed more compactly and conveniently using function templates (p. 246).
- Given the argument types provided in calls to a function template, C++ automatically generates separate function template specializations (p. 246) to handle each type of call appropriately.
- All function template definitions begin with the `template` keyword (p. 246) followed by a template parameter list (p. 246) to the function template enclosed in angle brackets (`<` and `>`).
- The formal type parameters (p. 246) are preceded by keyword `typename` (or `class`) and are placeholders for fundamental types or user-defined types. These placeholders are used to specify the types of the function’s parameters, to specify the function’s return type and to declare variables within the body of the function definition.
- C++11 introduces trailing return types for functions. To specify a trailing return type place `auto` before the function name, then follow the function’s parameter list with `->` and the return type.

### Section 6.20 Recursion

- A recursive function (p. 248) calls itself, either directly or indirectly.
- A recursive function knows how to solve only the simplest case(s), or so-called base case(s). If the function is called with a base case (p. 249), the function simply returns a result.
- If the function is called with a more complex problem, the function typically divides the problem into two conceptual pieces—a piece that the function knows how to do and a piece that it does not know how to do. To make recursion feasible, the latter piece must resemble the original problem, but be a slightly simpler or slightly smaller version of it.
- For recursion to terminate, the sequence of recursive calls (p. 249) must converge on the base case.
- C++11’s new unsigned long long int type (which can be abbreviated as unsigned long long) on some systems enables you to store values in 8 bytes (64 bits) which can hold numbers as large as 18,446,744,073,709,551,615.

### Section 6.21 Example Using Recursion: Fibonacci Series

- The ratio of successive Fibonacci numbers converges on a constant value of 1.618…. This number frequently occurs in nature and has been called the golden ratio or the golden mean (p. 252).

### Section 6.22 Recursion vs. Iteration

- Iteration (p. 249) and recursion are similar: both are based on a control statement, involve repetition, involve a termination test, gradually approach termination and can occur infinitely.
- Recursion repeatedly invokes the mechanism, and overhead, of function calls. This can be expensive in both processor time and memory space. Each recursive call (p. 249) causes another copy of the function’s variables to be created; this can consume considerable memory.

### Self-Review Exercises

- 6.1  Answer each of the following:
- a) Program components in C++ are called ________ and ________.
- b) A function is invoked with a(n) ________.
- c) A variable known only within the function in which it’s defined is called a(n) ________.
- d) The ________ statement in a called function passes the value of an expression back to the calling function.
- e) The keyword ________ is used in a function header to indicate that a function does not return a value or to indicate that a function contains no parameters.
- f) An identifier’s ________ is the portion of the program in which the identifier can be used.
- g) The three ways to return control from a called function to a caller are ________, ________ and ________.
- h) A(n) ________ allows the compiler to check the number, types and order of the arguments passed to a function.
- i) Function ________ is used to produce random numbers.
- j) Function ________ is used to set the random number seed to randomize the number sequence generated by function rand.
- k) Storage-class specifier ________ is a recommendation to the compiler to store a variable in one of the computer’s registers.
- l) A variable declared outside any block or function is a(n) ________ variable.
- m) For a local variable in a function to retain its value between calls to the function, it must be declared with the ________ storage-class specifier.
