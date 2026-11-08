
- 23. The modulus operator, `%`, takes only integer operands.
- 24. Arithmetic expressions are evaluated using the precedence rules and the associativity of the arithmetic operators.
- 25. All operands in an integral expression, or integer expression, are integers, and all operands in a floating-point expression are decimal numbers.
- 26. A mixed expression is an expression that consists of both integers and decimal numbers.
- 27. When evaluating an operator in an expression, an integer is converted to a floating-point number, with a decimal part of 0, only if the operator has mixed operands.
- 28. You can use the cast operator to explicitly convert values from one data type to another.
- 29. A string is a sequence of zero or more characters.
- 30. Strings in C++ are enclosed in double quotation marks.
- 31. A string containing no characters is called a null or empty string.
- 32. Every character in a string has a relative position in the string. The position of the first character is 0, the position of the second character is 1, and so on.
- 33. The length of a string is the number of characters in it.
- 34. During program execution, the contents of a named constant cannot be changed.
- 35. A named constant is declared by using the reserved word `const`.
- 36. A named constant is initialized when it is declared.
- 37. All variables must be declared before they can be used.
- 38. C++ does not automatically initialize variables.
- 39. Every variable has a name, a value, a data type, and a size.
- 40. When a new value is assigned to a variable, the old value is lost.
- 41. Only an assignment statement or an input (read) statement can change the value of a variable.
- 42. In C++, `>>` is called the stream extraction operator.
- 43. Input from the standard input device is accomplished by using `cin` and the stream extraction operator `>>`.
- 44. When data is input in a program, the data items, such as numbers, are usually separated by blanks, lines, or tabs.
- 45. In C++, `<<` is called the stream insertion operator.
- 46. Output of the program to the standard output device is accomplished by using `cout` and the stream insertion operator `<<`.
- 47. The manipulator `endl` positions the insertion point at the beginning of the next line on an output device.
- 48. Outputting or accessing the value of a variable in an expression does not destroy or modify the contents of the variable.
- 49. The character `\` is called the escape character.
- 50. The sequence `\n` is called the newline escape sequence.
- 51. All preprocessor commands start with the symbol `#`.
- 52. The preprocessor commands are processed by the preprocessor before the program goes through the compiler.
- 53. The preprocessor command `#include <iostream>` instructs the preprocessor to include the header file `iostream` in the program.
- 54. To use `cin` and `cout`, the program must include the header file `iostream` and either include the statement `using namespace std;` or refer to these identifiers as `std::cin` and `std::cout`.
- 55. All C++ statements end with a semicolon. The semicolon in C++ is called the statement terminator.
- 56. A C++ system has three components: environment, language, and the standard libraries.
- 57. Standard libraries are not part of the C++ language. They contain functions to perform operations, such as mathematical operations.
- 58. A file containing a C++ program usually ends with the extension `.cpp`.
- 59. Prompt lines are executable statements that tell the user what to do.
- 60. Corresponding to the five arithmetic operators `+`, `-`, `*`, `/`, and `%`, C++ provides five compound operators: `+=`, `-=`, `*=`, `/=`, and `%=`, respectively.

## EXERCISES

- 1. Mark the following statements as true or false.
  - a. An identifier can be any sequence of digits and letters.
  - b. In C++, there is no difference between a reserved word and a pre-defined identifier.
  - c. A C++ identifier can start with a digit.
  - d. The operands of the modulus operator must be integers.
  - e. If `a = 4;` and `b = 3;`, then after the statement `a = b;`, the value of `b` is still 3.
  - f. In the statement `cin >> y;`, `y` can only be an `int` or a `double` variable.
  - g. In an output statement, the newline character may be a part of the string.
  - h. The following is a legal C++ program:

    ```cpp
    int main()
    {
        return 0;
    }
    ```

  - i. In a mixed expression, all the operands are converted to floating-point numbers.
  - j. Suppose `x = 5`. After the statement `y = x++;` executes, `y` is 5 and `x` is 6.
  - k. Suppose `a = 5`. After the statement `++a;` executes, the value of `a` is still 5 because the value of the expression is not saved in another variable.

- 2. Which of the following are valid C++ identifiers?
  - a. `firstCPPProject`
  - b. `POP_QUIZ`
  - c. `++Program2`
  - d. `quiz7`
  - e. `ProgrammingLecture2`
  - f. `3feet1Yard`
  - g. `Mike'sFirstAttempt`
  - h. `Update Grade`
  - i. `4th`
  - j. `New_Student`

- 3. Which of the following is a reserved word in C++?
  - a. `Const`
  - b. `include`
  - c. `Char`
  - d. `void`
  - e. `int`
  - f. `Return`

- 4. What is the difference between a keyword and a user-defined identifier?

- 5. Are the identifiers `firstName` and `FirstName` the same?

- 6. Evaluate the following expressions:
  - a. `36 / 5`
  - b. `18 - 32 / 6 * 3`
  - c. `80 * 11`
  - d. `6 - 8 * 11`
  - e. `22.0 / 5`
  - f. `27 - 12 / 8.0`
  - g. `25 - 7 * 3 + 8 / 3`
  - h. `18.0 + 5.0 * 3.0 / 4.0`

- 7. If `x = 5`, `y = 6`, `z = 4`, and `w = 3.5`, evaluate each of the following statements, if possible. If it is not possible, state the reason.
  - a. `(x + z) % y`
  - b. `(x + y) % w`
  - c. `(y + w) % x`
  - d. `(x + y) * w`
  - e. `(x % y) % z`
  - f. `(y % z) % x`
  - g. `(x % z) % y`
  - h. `((x * y) * w) * z`

- 8. Given:

  ```cpp
  int num1, num2, newNum;
  double x, y;
  ```

  Which of the following assignments are valid? If an assignment is not valid, state the reason.

  When not given, assume that each variable is declared.

  - a. `num1 = 35;`
  - b. `newNum = num1 - num2;`
  - c. `num1 = 5; num2 = 2 + num1; num1 = num2 / 3;`
  - d. `num1 * num2 = newNum;`
  - e. `x = 12 * num1 - 15.3;`
  - f. `num1 * 2 = newNum + num2;`
  - g. `x / y == x * y;`
  - h. `num2 = num1 % 2.0;`
  - i. `newNum = static_cast<int> (x) % 5;`
  - j. `x = x + y - 5;`
  - k. `newNum = num1 + static_cast<int> (4.6 / 2);`

- 9. Do a walk-through to find the value assigned to `e`. Assume that all variables are properly declared.

  ```cpp
  a = 3;
  b = 4;
  c = (a % b) * 6;
  d = c / b;
  e = (a + b + c + d) / 4;
  ```

- 10. Which of the following variable declarations are correct? If a variable declaration is not correct, give the reason(s) and provide the correct variable declaration.

  ```cpp
  55 = age;                                      //Line 1
  char letter = '';                              //Line 2
  string message = "First test is on Monday"       //Line 3
  int one = 5;                                    //Line 4
  int prime;                                      //Line 5
  double x, y, z;                                 //Line 6
  ```

- 11. Which of the following are valid C++ assignment statements? Assume that `i`, `x`, and `percent` are double variables.
  - a. `i = i + 5;`
  - b. `x + 2 = x;`
  - c. `x = 2.5 * x;`
  - d. `percent = 10%;`

- 12. Write C++ statement(s) that accomplish the following:
  - a. Declare `int` variables `x` and `y`. Initialize `x` to 25 and `y` to 18.
  - b. Declare and initialize an `int` variable `temp` to 10 and a `char` variable `ch` to `'A'`.
  - c. Update the value of an `int` variable `x` by adding 5 to it.
  - d. Declare and initialize a `double` variable `payRate` to 12.50.
  - e. Copy the value of an `int` variable `firstNum` into an `int` variable `tempNum`.
  - f. Swap the contents of the `int` variables `x` and `y`. (Declare additional variables, if necessary.)
  - g. Suppose `x` and `y` are `double` variables. Output the contents of `x`, `y`, and the expression `x + 12 / y - 18`.
  - h. Declare a `char` variable `grade` and set the value of `grade` to `'A'`.
  - i. Declare `int` variables to store four integers.
  - j. Copy the value of a `double` variable `z` to the nearest integer into an `int` variable `x`.
