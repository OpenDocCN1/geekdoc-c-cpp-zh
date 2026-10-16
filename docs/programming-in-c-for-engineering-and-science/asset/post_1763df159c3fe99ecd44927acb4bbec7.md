
- Insert appropriate documentation before each function defined in the main function's file, to separate it from other program components;
- Indent the declarations and statements within each function.
- *All guidelines for programming style apply to functions.*
- *Once a problem has been analyzed to identify the problem's objects and the operations needed to solve it, an algorithm should be constructed that specifies the order in which the operations are applied to the objects.*
- *Operations that are not predefined (or are nontrivial) in C++ should be encoded as functions, separate from the main function.*
- *A function that encodes an operation should be designed in the same manner as the main function.*
- *A function that returns no values should have its return type declared as void.*
- *A function that receives no values should have no parameters within the parentheses of the function heading.*
- *If a function is sufficiently general that it might someday prove useful in solving a different problem, a library should be constructed to store that function, rather than declaring and defining it in the program's source file.*
- *A library's files should be documented in much the same way as programs. For each library, provide a special documentation file that describes clearly, precisely, and completely the contents of the library and how to use items in it, any special algorithms it implements, and other useful information such as the author, a modification history, and so on. This documentation file should be kept in the same place as the other files of a library, so that users can refer to that file in order to understand and use the objects and functions stored in the library.*
- *When the header file of a less commonly used library is inserted in a program (using `#include`), a comment should be used to explain its purpose, for example, what is being used from it in the program.*
- *Libraries provide the following benefits:*
  - *A library extends the language, because its objects can be made available to any program or to another library.*
  - *The items in a library's interface can be used without being concerned about the details of their implementation.*
  - *Programs and libraries can be compiled separately. Changing the implementation file of a library requires recompilation of only that implementation file.*
- *Libraries provide another level of modularity in software design: related functions and other objects can be grouped together in independent libraries.*

## Warnings

1. When a function is called, the list of arguments is matched against the list of parameters from left to right, with the leftmost argument associated with the leftmost parameter, the next argument associated with the next parameter, and so on. The number of arguments must be the same as the number of parameters (for exceptions see the description of default arguments on the text’s website) and the type of each argument must be compatible with the type of the corresponding parameter.
2. Identifiers defined within a function (e.g., parameters, local variables, and local constants) are defined only during the execution of that function; they are undefined both before and after its execution. Any attempt to use such identifiers outside the function (without redeclaring them) is an error.
3. If a function changes the value of a parameter, the value of the corresponding argument is not altered. A parameter is a completely separate variable into which the argument value is copied. Any change to the parameter changes the copy, not the corresponding argument.¹⁰
4. A function must be declared before it is called.
5. If a function needs things from a library, the header file of that library must be inserted (using `#include`) before the definition of that function.
6. The implementation file of a library should always insert the header file of that library (using `#include`) so that the compiler can verify that each function’s prototype is consistent with its definition. Failure to follow this rule is a common source of linking errors.
7. A function that is defined in the implementation file of a library but not declared in that library’s header file cannot be called outside the library (but it can be called inside the library).

## TEST YOURSELF

### Section 6.3

1. In addition to input and output objects, what two other kinds of objects are usually included in the description of a function’s behavior?
2. In the function heading double sum(int a, char b), a and b are called ______.
3. For a function whose heading is double sum(int a, char b), the type of the value returned by the function is ______.
4. The keyword ______ is used to indicate the return type of a function that returns no value.
5. A function stub is a function definition in which the function’s body contains ________.

Questions 6–10 deal with the following function definition:

```cpp
int what(int n)
{
    return (n * (n + 1)) / 2;
}
```

6. If the statement `number1 = what(number2);` appears in the main function, number2 is called a(n) ________ in this function call.
7. If the statement `int number = what(3);` appears in the main function, the value assigned to number will be ________.
8. (True or false) The value assigned to number by the statement `int number = what(2+3);` in the main function will be 15.
9. (True or false) The value assigned to number by the statement `int number = what(1, 5);` in the main function will be 3.
10. Write a prototype for function `what()`.
11. Write a function definition that calculates values of x² + √x.
12. Write a function definition that calculates the integer average of two integers.
13. Write a function definition that displays three integers on three lines separated by two blank lines.

### Section 6.4

1. (True or false) Libraries were first provided in the language C++.
2. What are the three types of files included in a library?
3. What are the main benefits of using libraries?
4. A library’s ________ file contains the declarations and prototypes of the items in the library.
5. A library’s ________ file contains the definitions of the functions in the library.
6. A library’s ________ file is sometimes called its interface file.
7. The items in a library’s header file contain ________ information, whereas the items in its implementation file contain ________ information (public or private).
8. If a program contains `#include` ________, the compiler will search for the file lib in a special system include directory.
9. If a program contains `#include` ________, the compiler will search for the file lib in the directory that contains the program being compiled.
10. What two steps are required to translate a program that uses libraries?
11. (True or false) A library's header file is usually compiled separately from a program that uses the library.
12. (True or false) If a library's header file is modified then all programs that use the library must be recompiled.
13. ______ makes it possible to use a library without knowing all the details of how it is implemented.

## EXERCISES

### Section 6.3

For Exercises 1–13, you are to write functions to compute and return various quantities. To test these functions, you should write driver programs as instructed in the Programming Problems.

1. Find the circumference of a circle with a given radius. (C = 2πr).
2. Find the area of a circle with a given radius. (A = πr²).
3. Find the perimeter of a rectangle, given the lengths of the sides. (P = 2l + 2w).
4. Find the area of a square, given the lengths of the sides. (A = s²).
5. Find the perimeter of a triangle, given the lengths of the three sides. (P = s₁ + s₂ + s₃).
6. Find the area of a triangle, given the lengths of the three sides. (The area of a triangle can be found by using Hero's formula, area = √[s(s−a)(s−b)(s−c)] where a, b, and c are the lengths of the sides and s is one half of the perimeter.)
