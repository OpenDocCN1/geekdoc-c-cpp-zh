
displays Enter first integer: followed by a space. This message is called a prompt because it directs the user to take a specific action. Line 13

```cpp
std::cin >> number1; // read first integer from user into number1
```

uses the standard input stream object cin (of namespace std) and the stream extraction operator, >>, to obtain a value from the keyboard.

When the preceding statement executes, the program waits for you to enter a value for variable number1. You respond by typing an integer (as characters), then pressing the Enter key (sometimes called the Return key) to send the characters to the program. The cin object converts the character representation of the number to an integer value and assigns this value to the variable number1. Pressing Enter also causes the cursor to move to the beginning of the next line on the screen.

When your program expects the user to enter an integer, the user could enter alphabetic characters, special symbols (like # or @) or a number with a decimal point (like 73.5). In these early programs, we assume that the user enters valid data. We’ll present various techniques for dealing with data-entry problems later.

### Obtaining the Second Value from the User

Line 15

```cpp
std::cout << "Enter second integer: "; // prompt user for data
```

displays Enter second integer: on the screen, prompting the user to take action. Line 16

```cpp
std::cin >> number2; // read second integer from user into number2
```

obtains a value for variable number2 from the user.

### Calculating the Sum of the Values Input by the User

The assignment statement in line 18

```cpp
sum = number1 + number2; // add the numbers; store result in sum
```

adds the values of number1 and number2 and assigns the result to sum using the assignment operator =. Most calculations are performed in assignment statements. The = operator and the + operator are binary operators—each has two operands. For the + operator, the two operands are number1 and number2. For the preceding = operator, the two operands are sum and the value of the expression number1 + number2. Placing a space on each side of a binary operator makes the operator stand out and makes the program more readable.

### Displaying the Result

Line 20

```cpp
std::cout << "Sum is " << sum << '\n'; // display sum
```

displays the string "Sum is" followed by the numerical value of variable sum and a newline. This statement outputs values of multiple types. The stream insertion operator “knows” how to output each type of data. Using multiple stream insertion operators (<<) in a single statement is called concatenating, chaining or cascading stream insertion operations.

Calculations can also be performed in output statements. We could have eliminated the variable sum by combining the statements in lines 18 and 20 into the statement

```cpp
std::cout << "Sum is " << number1 + number2 << '\n';
```

A signature feature of C++ is that you can create your own data types called classes, which we discuss in depth in Chapter 9 and subsequent chapters. You can then “teach” C++ how to input and output values of these new data types using the `>>` and `<<` operators, respectively. This is called **operator overloading**, which we explore in Chapter 11.

### Checkpoint

- 1. *(Code)* Write a statement that initializes the int variable `total` to 0 using braced initialization.
  
  **Answer:** `int total{0};`
- 2. *(Code)* Assume the int variables `billAmount` and `tip` exist and have been initialized. Write an initialization statement that adds the values of `billAmount` and `tip` and stores the result in the new int variable `totalBill`.
  
  **Answer:** `int totalBill{billAmount + tip};`
- 3. *(True/False)* Variables must be defined with a type and a name before using them.
  
  **Answer:** True.

## 2.5 Memory Concepts

Variable names such as number1, number2 and sum correspond to locations in the computer’s memory. Every variable has a name, a type, a size (determined by the type) and a value.

In the addition program of Fig. 2.4, when the following statement (line 13) executes

```cpp
std::cin >> number1;  // read first integer from user into number1
```

the program places the integer typed by the user into a memory location to which the compiler assigned the name number1. If the user enters 45 for number1, the program places 45 into the location number1, as in:

![](img/7b5e2088e71c7f78681d4ddbcf104c06_133_0.png)

When a value is placed in a memory location, the new value overwrites the previous one in that location—that previous value is lost.

Returning to our addition program, suppose the user enters 72 when the following statement (line 16) executes:

```cpp
std::cin >> number2;  // read second integer from user into number2
```

The program places 72 into the location number2, and memory appears as in:

![](img/7b5e2088e71c7f78681d4ddbcf104c06_133_1.png)

The variables’ locations are not necessarily adjacent in memory.

After the program obtains values for number1 and number2, it adds these values and places the total into the variable sum. The statement (line 18)

```cpp
sum = number1 + number2;
```

places the calculated sum of `number1` and `number2` into variable `sum`, after which memory appears as follows:

![](img/7b5e2088e71c7f78681d4ddbcf104c06_134_0.png)

Performing the calculation uses, but does not modify, the values of `number1` and `number2`.

### ✓ Checkpoint

- 1. *(Fill-in)* Every variable has a name, a ______, a ______ and a ______.
  
  **Answer:** type, size, value.
- 2. *(True/False)* Storing a value in a variable replaces the previous value in the corresponding memory location.
  
  **Answer:** True.
- 3. *(True/False)* An expression like `number1 + number2` uses the values of the variables `number1` and `number2`, but does not modify them.
  
  **Answer:** True.

## 2.6 Arithmetic

The following table summarizes the arithmetic operators:

| Operation | Arithmetic operator | Algebraic expression | C++ expression |
|---|---|---|---|
| Addition | `+` | *f + 7* | `f + 7` |
| Subtraction | `-` | *p − c* | `p - c` |
| Multiplication | `*` | *bm* or *b · m* | `b * m` |
| Division | `/` | *x / y* or *x ÷ y* | `x / y` |
| Remainder | `%` | *r mod s* | `r % s` |

The asterisk (*) indicates multiplication, and the percent sign (%) is the remainder operator, which we’ll discuss shortly. These arithmetic operators are all binary operators.

### Integer Division

Integer division in which the numerator and the denominator are integers yields an integer quotient. So, the expression `7 / 4` evaluates to 1, and the expression `17 / 5` evaluates to 3. Any fractional part resulting from integer division is truncated—no rounding occurs.

### Remainder Operator

The remainder operator, % (also called the modulus operator), yields the remainder after integer division and can be used only with integer operands. The expression `x % y` yields the remainder after dividing x by y. Thus, `7 % 4` yields 3 and `17 % 5` yields 2.

### Parentheses for Grouping Subexpressions

Parentheses are used in C++ expressions in the same manner as in algebraic expressions. For example, to multiply x times the quantity y + z, we write x × (y + z).

### Rules of Operator Precedence

C++ applies the operators in arithmetic expressions in a precise order determined by the following rules of operator precedence, which are generally the same as those in algebra:

- 1. Expressions in parentheses evaluate first. Parentheses are said to be at the “highest level of precedence.” In cases of nested or embedded parentheses, as in the following statement, expressions in the innermost pair of parentheses evaluate first:
  
  `(a * (b + c))`
- 2. Multiplication, division and remainder operations evaluate next. In an expression containing several of these operations, they’re applied from left to right. These three operators have the same level of precedence.
- 3. Addition and subtraction operations evaluate last and are applied from left to right. Addition and subtraction have the same level of precedence.

You can view the complete operator precedence chart at https://en.cppreference.com/w/cpp/language/operator_precedence. **Caution:** In an expression with two sets of parentheses “on the same level,” such as `(a + b) * (c − d)`, the C++ Standard does not specify the order in which these parenthesized subexpressions will evaluate.

### Operator Grouping

When we say that C++ applies certain operators from left to right, we are referring to the operators’ grouping (sometimes called associativity). For example, in the expression

```
a + b + c
```

the addition operators (+) group from left-to-right as if we parenthesized the expression as `(a + b) + c`. Most C++ operators of the same precedence group from left to right. We’ll see that some operators group from right to left.

### Sample Algebraic and C++ Expressions

Now consider several expressions in light of the rules of operator precedence. Each example lists an algebraic expression and its C++ equivalent. The following is an example of an arithmetic mean (average) of five terms:

Algebra: m = (a + b + c + d + e) / 5

C++: m = (a + b + c + d + e) / 5;

The parentheses are required because division has higher precedence than addition. The entire quantity (a + b + c + d + e) is to be divided by 5. If the parentheses are erroneously omitted, we obtain a + b + c + d + e / 5, which evaluates incorrectly as

a + b + c + d + e / 5

The following is an example of the equation of a straight line:

Algebra: y = mx + b

C++: y = m * x + b;
