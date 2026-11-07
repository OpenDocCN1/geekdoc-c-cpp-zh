
user input

```cpp
float num, area;

cout << "Enter dimension in feet: ";
cin >> num;
```

- 8. Call the first function and output its returned value

  ```cpp
  area = computeArea(num);
  cout << "Circle: Area = " << area << " sq.ft." << endl;
  ```

- 9. Call the overloaded functions and output their returns

  ```cpp
  area = computeArea(num, num);
  cout << "Square: Area = " << area << " sq.ft." << endl;
  area = computeArea('T', num, num);
  cout << "Triangle: Area = " << area << " sq.ft." << endl;
  ```

- 10. Save, compile, and run the program, then enter a numeric value when requested, to see the output

![](img/bf8dbdfb89042fadbaa73b4160c74bac_56_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_56_1.png)

The value passed to the char argument is never used – that argument is included merely to differentiate that overloaded function.

## Optimizing functions

Functions can call themselves recursively, to repeatedly execute the statements contained in their function body – much like a loop. As with loops, a recursive function must contain an incrementer and a conditional test to call itself again, or stop repeating when a condition is met. The syntax of a recursive function looks like this:

```text
return-data-type function-name(argument-list)
{
    statements-to-be-executed;
    incrementer;
    conditional-test-to-recall-or-exit;
}
```

The incrementer will change the value of a passed argument – so subsequent calls will pass the adjusted value back to the function.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_57_0.png)

optimize.cpp

- 1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use.

  ```cpp
  #include <iostream>
  using namespace std;
  ```

- 2. Below the preprocessor instructions, declare two function prototypes that will both be recursive functions.

  ```cpp
  int computeFactorials(int, int);
  int factorial(int);
  ```

- 3. Below the prototype declarations, add a main function containing a final **return** statement.

  ```cpp
  int main()
  {
      // Program code goes here.
      return 0;
  }
  ```

- 4. After the main function, add the definition for the first function prototype – a recursive function.

  ```cpp
  int computeFactorials(int num, int max)
  {
      cout << "Factorial of " << num << ": ";
      cout << factorial(num) << endl;     // Statements.
      num++;                              // Incrementer.
      if (num > max) return 0;            // Exit...
      else computeFactorials(num, max);   // Or call again.
  }
  ```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_57_1.png)

A recursive function generally uses more system resources than a loop – but it can make for more readable code.

- 5. Define a recursive function for the second prototype.

  ```cpp
  int factorial(int n)
  {
      int result;
      if (n == 1) result = 1;             // Exit or...
  }
  ```

```cpp
else result = (factorial(n - 1) * n); // Decrement.
return result;                        // and call again.
}
```

- 6. At the start of the main function, insert a call to the recursive function `computeFactorials(1, 8);`

- 7. Save, compile, and run the program to see the output

![](img/bf8dbdfb89042fadbaa73b4160c74bac_58_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_58_1.png)

If you accidentally run an infinite recursive function, press the Ctrl + C keys to terminate the process.

The output lists factorial values (factorial 3 is 3 × 2 × 1 = 6, etc.), but the program can be improved by optimizing the `factorial()` function. This function does not need a variable if written with the ternary operator. It then contains just one statement, so its definition can replace the prototype declaration as an "inline" declaration. This means that the program need not keep checking between the declaration and definition, and so improves efficiency.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_58_2.png)

Inline declarations may only contain one or two statements, as the compiler recreates them at each calling point – longer inline declarations would, therefore, produce a more unwieldy program.

- 8. Delete the `factorial()` function definition, then replace its prototype declaration with this inline declaration

  ```cpp
  inline int factorial(int n)
  { return (n == 1) ? 1 : (factorial(n - 1) * n); }
  ```

- 9. Save, compile, and run the program again to see the same output, produced more efficiently

## Summary

- An **if** statement evaluates a given test expression for a Boolean value of **true** or **false**.
- Statements contained in braces after an **if** statement will only be executed when the evaluation is found to be **true**.
- The **if** and **else** keywords are used to perform conditional branching according to the result of a tested expression.
- A **switch** statement is an alternative form of conditional branching that matches a **case** statement to a given value.
- The **for** loop structure has parameters declaring an initializer, a test expression, and an incrementer or decrementer.
- A **while** loop and **do-while** loop must always have an incrementer or decrementer within their loop body.
- Any type of loop can be immediately terminated by including a **break** statement within the loop body.
- A single iteration of any type of loop can be skipped by including a **continue** statement within the loop body.
- Functions are usually declared as prototypes at the start of the program, and defined after the main function.
- Variables declared in a function are only accessible from within that function, as they only have local scope.
- Values can be passed into functions if arguments are declared in the function prototype and definition.
- Overloaded functions have the same name but a different number or type of declared arguments.
- Recursive functions repeatedly call themselves until a test condition is met.
- Short function definitions of just one or two statements can be declared in place of a prototype using the **inline** keyword.

## 4 Handling strings

This chapter demonstrates how to manipulate C++ text strings as a simpler, more powerful alternative to character arrays.

- Creating string variables
- Getting string input
- Solving the string problem
- Discovering string features
- Joining & comparing strings
- Copying & swapping strings
- Finding substrings
- Replacing substrings
- Summary

## Creating string variables

Unlike the **char**, **int**, **float**, **double**, and **bool** data types, there is no native “string” data type in C++ – but its **<string>** library class provides a **string** object that emulates a string data type. To make this available to a program, the library must be added with an **#include <string>** directive at the start of the program.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_61_0.png)

Like the **<iostream>** class library, the **<string>** library is part of the **std** namespace that is used by the C++ standard library classes. This means that a string object can be referred to as **std::string**, or more simply as **string** when a **using namespace std;** directive is included at the start of the program.

Once the **<string>** library is made available, a **string** “variable” can be declared in the same way as other variables. The declaration may optionally initialize the variable using the **=** assignment operator, or it may be initialized later in the program.

Additionally, a **string** variable may be initialized by including a text string between parentheses after the variable name.

Text strings in C++ must always be enclosed within “ ” double quote characters – ‘ ’ single quotes are only used to surround character values of the **char** data type.

A C++ **string** variable is much easier to work with than the **char** arrays which C programmers must use, as it automatically resizes to accommodate the length of any text string. At a lower level, the text is still stored as a character array, but the **string** variable lets you ignore those details. Consequently, a character array can be assigned to a **string** variable using the **=** assignment operator.

It is important to remember that when numeric values are assigned to a **string** variable, they are no longer a numeric data type, so arithmetic cannot be performed on them. For example, attempting to add **string** values of “7” and “6” with the **+** addition operator produces the concatenated **string “76”**, not the numerical value of 13. In this case, the **+** operator recognizes that the context is not arithmetical, so adopts the guise of “concatenation operator” to unite the two strings. Similarly, the **+=** operator appends a **string** to another **string** and is useful to build long strings of text.

Several **string** values are built into a single long string in the example program described below.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_61_1.png)

- 1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use

  ```cpp
  #include <string>       // Include string support.
  #include <iostream>
  using namespace std;
  ```

- 2. Add a main function containing four **string** variable declarations and a final **return** statement

  ```cpp
  int main()
  ```
