
The circled numbers under the statement indicate the order in which C++ applies the operators. The multiplication, modulus and division are evaluated first in left-to-right order (i.e., they associate from left to right) because they have higher precedence than addition and subtraction. The addition and subtraction are applied next. These are also applied left to right. The assignment operator is applied last because its precedence is lower than that of any of the arithmetic operators.

## Evaluation of a Second-Degree Polynomial

To develop a better understanding of the rules of operator precedence, consider the evaluation of a second-degree polynomial $y = ax^2 + bx + c$.

```
y = a * x * x + b * x + c;

Operator order: 6, 1, 2, 4, 3, 5
```

The circled numbers under the statement indicate the order in which C++ applies the operators. *There is no arithmetic operator for exponentiation in C++*, so we've represented $x^2$ as $x * x$. In Chapter 5, we'll discuss the standard library function `pow` ("power") that performs exponentiation.

Suppose variables a, b, c and x in the preceding second-degree polynomial are initialized as follows: a = 2, b = 3, c = 7 and x = 5. Figure 2.11 illustrates the order in which the operators are applied and the final value of the expression.

![](img/b42ba5cd262b1358d16610173f975e4d_87_0.png)

**Fig. 2.11**  |  Order in which a second-degree polynomial is evaluated.

## Redundant Parentheses

As in algebra, it's acceptable to place unnecessary parentheses in an expression to make the expression clearer. These are called redundant parentheses. For example, the preceding assignment statement could be parenthesized as follows:

```
y = (a * x * x) + (b * x) + c;
```

## 2.7 Decision Making: Equality and Relational Operators

We now introduce a simple version of C++'s if statement that allows a program to take alternative action based on whether a condition is true or false. If the condition is true, the statement in the body of the if statement is executed. If the condition is false, the body statement is not executed. We'll see an example shortly.

Conditions in if statements can be formed by using the relational operators and equality operators summarized in Fig. 2.12. The relational operators all have the same level of precedence and associate left to right. The equality operators both have the same level of precedence, which is lower than that of the relational operators, and associate left to right.

| Algebraic relational or equality operator | C++ relational or equality operator | Sample C++ condition | Meaning of C++ condition |
|---|---|---|---|
| **Relational operators** |  |  |  |
| > | > | x > y | x is greater than y |
| < | < | x < y | x is less than y |
| ≥ | >= | x >= y | x is greater than or equal to y |
| ≤ | <= | x <= y | x is less than or equal to y |
| **Equality operators** |  |  |  |
| = | == | x == y | x is equal to y |
| ≠ | != | x != y | x is not equal to y |

**Fig. 2.12**  Relational and equality operators.

![](img/b42ba5cd262b1358d16610173f975e4d_88_0.png)

> **Common Programming Error 2.3**
>
> Reversing the order of the pair of symbols in the operators !=, >= and <= (by writing them as =!, => and =<, respectively) is normally a syntax error. In some cases, writing != as =! will not be a syntax error, but almost certainly will be a logic error that has an effect at execution time. You'll understand why when you learn about logical operators in Chapter 5. A fatal logic error causes a program to fail and terminate prematurely. A nonfatal logic error allows a program to continue executing, but usually produces incorrect results.

![](img/b42ba5cd262b1358d16610173f975e4d_88_1.png)

> **Common Programming Error 2.4**
>
> Confusing the equality operator == with the assignment operator = results in logic errors. We like to read the equality operator as "is equal to" or "double equals," and the assignment operator as "gets" or "gets the value of" or "is assigned the value of." As you'll see in Section 5.9, confusing these operators may not necessarily cause an easy-to-recognize syntax error, but may cause subtle logic errors.

## Using the if Statement

The following example (Fig. 2.13) uses six if statements to compare two numbers input by the user. If the condition in any of these if statements is satisfied, the output statement associated with that if statement is executed.

```cpp
// Fig. 2.13: fig02_13.cpp
// Comparing integers using if statements, relational operators
// and equality operators.
#include <iostream> // allows program to perform input and output

using std::cout; // program uses cout
using std::cin; // program uses cin
using std::endl; // program uses endl

// function main begins program execution
int main()
{
    int number1 = 0; // first integer to compare (initialized to 0)
    int number2 = 0; // second integer to compare (initialized to 0)

    cout << "Enter two integers to compare: "; // prompt user for data
    cin >> number1 >> number2; // read two integers from user

    if ( number1 == number2 )
        cout << number1 << " == " << number2 << endl;

    if ( number1 != number2 )
        cout << number1 << " != " << number2 << endl;

    if ( number1 < number2 )
        cout << number1 << " < " << number2 << endl;

    if ( number1 > number2 )
        cout << number1 << " > " << number2 << endl;

    if ( number1 <= number2 )
        cout << number1 << " <= " << number2 << endl;

    if ( number1 >= number2 )
        cout << number1 << " >= " << number2 << endl;
} // end function main
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

**Fig. 2.13**  |  Comparing integers using if statements, relational operators and equality operators. (Part 1 of 2.)

```text
Enter two integers to compare: 7 7
7 == 7
7 <= 7
7 >= 7
```

**Fig. 2.13**  |  Comparing integers using if statements, relational operators and equality operators.  
(Part 2 of 2.)

### using Declarations

Lines 6–8

```
using std::cout;  // program uses cout
using std::cin;   // program uses cin
using std::endl;  // program uses endl
```

are **using declarations** that eliminate the need to repeat the std:: prefix as we did in earlier programs. We can now write cout instead of std::cout, cin instead of std::cin and endl instead of std::endl, respectively, in the remainder of the program.

In place of lines 6–8, many programmers prefer to produce the **using directive**

```
using namespace std;
```

which enables a program to use all the names in any standard C++ header (such as <iostream>) that a program might include. From this point forward in the book, we'll use the preceding directive in our programs.¹

### Variable Declarations and Reading the Inputs from the User

Lines 13–14

```
int number1 = 0;  // first integer to compare (initialized to 0)
int number2 = 0;  // second integer to compare (initialized to 0)
```

declare the variables used in the program and initialize them to 0.

The program uses cascaded stream extraction operations (line 17) to input two integers. Remember that we're allowed to write cin instead of std::cin because of line 7. First a value is read into variable number1, then a value is read into variable number2.

### Comparing Numbers

The if statement in lines 19–20

```
if ( number1 == number2 )
    cout << number1 << " == " << number2 << endl;
```

compares the values of variables number1 and number2 to test for equality. If the values are equal, the statement in line 20 displays a line of text indicating that the numbers are equal. If the conditions are true in one or more of the if statements starting in lines 22, 25, 28, 31 and 34, the corresponding body statement displays an appropriate line of text.

Each if statement in Fig. 2.13 has a single statement in its body and each body statement is indented. In Chapter 4 we show how to specify if statements with multiple-statement bodies (by enclosing the body statements in a pair of braces, { }, creating what's called a **compound statement** or a **block**).

1. In Chapter 23, Other Topics, we'll discuss some issues with using directives in large-scale systems.
