
```cpp
18  if ( number1 == number2 )
19      cout << number1 << " == " << number2 << endl;

21  if ( number1 != number2 )
22      cout << number1 << " != " << number2 << endl;

24  if ( number1 < number2 )
25      cout << number1 << " < " << number2 << endl;

27  if ( number1 > number2 )
28      cout << number1 << " > " << number2 << endl;

30  if ( number1 <= number2 )
31      cout << number1 << " <= " << number2 << endl;

33  if ( number1 >= number2 )
34      cout << number1 << " >= " << number2 << endl;
35  } // end function main
```

```text
Enter two integers to compare: 3 7
3 != 7
3 < 7
3 <= 7
```

```text
Enter two integers to compare: 22 12
22 != 12
22 > 12
22 >= 12
```

```text
Enter two integers to compare: 7 7
7 == 7
7 <= 7
7 >= 7
```

**Fig. 2.13** | Comparing integers using if statements, relational operators and equality operators. (Part 2 of 2.)

## Lines 6–8

```cpp
using std::cout; // program uses cout
using std::cin;  // program uses cin
using std::endl; // program uses endl
```

are using declarations that eliminate the need to repeat the std:: prefix as we did in earlier programs. Once we insert these using declarations, we can write cout instead of std::cout, cin instead of std::cin and endl instead of std::endl, respectively, in the remainder of the program.

In place of lines 6–8, many programmers prefer to use the declaration

```cpp
using namespace std;
```

which enables a program to use all the names in any standard C++ header file (such as `<iostream>`) that a program might include. From this point forward in the book, we’ll use the preceding declaration in our programs.

## Lines 13–14

```cpp
int number1;  // first integer to compare
int number2;  // second integer to compare
```

declare the variables used in the program. Remember that variables may be declared in one declaration or in separate declarations.

The program uses cascaded stream extraction operations (line 17) to input two integers. Remember that we are allowed to write cin (instead of std::cin) because of line 7. First a value is read into variable number1, then a value is read into variable number2.

```cpp
if ( number1 == number2 )
    cout << number1 << " == " << number2 << endl;
```

compares the values of variables number1 and number2 to test for equality. If the values are equal, the statement in line 20 displays a line of text indicating that the numbers are equal. If the conditions are true in one or more of the if statements starting in lines 22, 25, 28, 31 and 34, the corresponding body statement displays an appropriate line of text.

Each if statement in Fig. 2.13 has a single statement in its body and each body statement is indented. In Chapter 4 we show how to specify if statements with multiple-statement bodies (by enclosing the body statements in a pair of braces, { }, creating what is called a compound statement or a block).

![](img/023f159fdd47d944d48e08843cea732d_93_0.png)

## Good Programming Practice 2.12

Indent the statement(s) in the body of an if statement to enhance readability.

![](img/023f159fdd47d944d48e08843cea732d_93_1.png)

## Good Programming Practice 2.13

For readability, there should be no more than one statement per line in a program.

![](img/023f159fdd47d944d48e08843cea732d_93_2.png)

## Common Programming Error 2.8

Placing a semicolon immediately after the right parenthesis after the condition in an if statement is often a logic error (although not a syntax error). The semicolon causes the body of the if statement to be empty, so the if statement performs no action, regardless of whether or not its condition is true. Worse yet, the original body statement of the if statement now becomes a statement in sequence with the if statement and always executes, often causing the program to produce incorrect results.

Note the use of white space in Fig. 2.13. Recall that white-space characters, such as tabs, newlines and spaces, are normally ignored by the compiler. So, statements may be split over several lines and may be spaced according to your preferences. It’s a syntax error to split identifiers, strings (such as "hello") and constants (such as the number 1000) over several lines.

- A message that directs the user to take a specific action is known as a prompt.

- C++ keyword return is one of several means to exit a function.

### Section 2.4 Another C++ Program: Adding Integers

- All variables in a C++ program must be declared before they can be used.

- A variable name in C++ is any valid identifier that is not a keyword. An identifier is a series of characters consisting of letters, digits and underscores ( _ ). Identifiers cannot start with a digit. C++ identifiers can be any length; however, some systems and/or C++ implementations may impose some restrictions on the length of identifiers.

- C++ is case sensitive.

- Most calculations are performed in assignment statements.

- A variable is a location in memory where a value can be stored for use by a program.

- Variables of type int hold integer values, i.e., whole numbers such as 7, -11, 0, 31914.

### Section 2.5 Memory Concepts

- Every variable stored in the computer's memory has a name, a value, a type and a size.

- Whenever a new value is placed in a memory location, the process is destructive; i.e., the new value replaces the previous value in that location. The previous value is lost.

- When a value is read from memory, the process is nondestructive; i.e., a copy of the value is read, leaving the original value undisturbed in the memory location.

- The std::endl stream manipulator outputs a newline, then "flushes the output buffer."

### Section 2.6 Arithmetic

- C++ evaluates arithmetic expressions in a precise sequence determined by the rules of operator precedence and associativity.

- Parentheses may be used to group expressions.

- Integer division (i.e., both the numerator and the denominator are integers) yields an integer quotient. Any fractional part in integer division is truncated—no rounding occurs.

- The modulus operator, %, yields the remainder after integer division. The modulus operator can be used only with integer operands.

### Section 2.7 Decision Making: Equality and Relational Operators

- The if statement allows a program to take alternative action based on whether a condition is met. The format for an if statement is

```cpp
if ( condition )
    statement;
```

If the condition is true, the statement in the body of the if is executed. If the condition is not met, i.e., the condition is false, the body statement is skipped.

- Conditions in if statements are commonly formed by using equality operators and relational operators. The result of using these operators is always the value true or false.

- The declaration

```cpp
using std::cout;
```

is a using declaration that informs the compiler where to find cout (namespace std) and eliminates the need to repeat the std:: prefix. The declaration

```cpp
using namespace std;
```

enables the program to use all the names in any included standard library header file.

- b) A ______ begins the body of every function and a ______ ends the body.
- c) Every C++ statement ends with a(n) ______.
- d) The escape sequence \n represents the ______ character, which causes the cursor to position to the beginning of the next line on the screen.
- e) The ______ statement is used to make decisions.

## 2.2

State whether each of the following is true or false. If false, explain why. Assume the statement using `std::cout;` is used:

- a) Comments cause the computer to print the text after the // on the screen when the program is executed.
- b) The escape sequence \n, when output with cout and the stream insertion operator, causes the cursor to position to the beginning of the next line on the screen.
- c) All variables must be declared before they’re used.
- d) All variables must be given a type when they’re declared.
- e) C++ considers the variables number and NumbeR to be identical.
- f) Declarations can appear almost anywhere in the body of a C++ function.
- g) The modulus operator (%) can be used only with integer operands.
- h) The arithmetic operators *, /, % and + - all have the same level of precedence.
- i) A C++ program that prints three lines of output must contain three statements using cout and the stream insertion operator.

## 2.3

Write a single C++ statement to accomplish each of the following (assume that using declarations have not been used):

- a) Declare the variables c, thisIsAVariable, q76534 and number to be of type int.
- b) Prompt the user to enter an integer. End your prompting message with a colon (:) followed by a space and leave the cursor positioned after the space.
- c) Read an integer from the user at the keyboard and store it in integer variable age.
- d) If the variable number is not equal to 7, print "The variable number is not equal to 7".
- e) Print the message "This is a C++ program" on one line.
- f) Print the message "This is a C++ program" on two lines. End the first line with C++.
- g) Print the message "This is a C++ program" with each word on a separate line.
- h) Print the message "This is a C++ program". Separate each word from the next by a tab.

## 2.4

Write a statement (or comment) to accomplish each of the following (assume that using declarations have been used for cin, cout and endl):

- a) State that a program calculates the product of three integers.
- b) Declare the variables x, y, z and result to be of type int (in separate statements).
- c) Prompt the user to enter three integers.
- d) Read three integers from the keyboard and store them in the variables x, y and z.
- e) Compute the product of the three integers contained in variables x, y and z, and assign the result to the variable result.
- f) Print "The product is " followed by the value of the variable result.
- g) Return a value from main indicating that the program terminated successfully.

## 2.5

Using the statements you wrote in Exercise 2.4, write a complete program that calculates and displays the product of three integers. Add comments to the code where appropriate. *[Note: You’ll need to write the necessary using declarations.]*

## 2.6

Identify and correct the errors in each of the following statements (assume that the statement using `std::cout;` is used):

```
a) if (c < 7);
       cout << c is less than \n;
```

```
b) if (c >= 7)
       cout << "c is equal to or greater than 7\n";
```
