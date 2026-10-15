
This makes the program less readable and prevents us from providing comments that describe each variable’s purpose.

We’ll soon discuss the data type double for specifying real numbers, and the data type char for specifying character data. Real numbers are numbers with decimal points, such as 3.4, 0.0 and −11.19. A char variable may hold only a single lowercase letter, a single uppercase letter, a single digit or a single special character (e.g., $ or *). Types such as int, double and char are often called fundamental types or built-in types. Fundamental-type names are keywords and therefore must appear in all lowercase letters. Appendix C contains the complete list of fundamental types.

A variable name (such as number1) is any valid identifier that is not a keyword. An identifier is a series of characters consisting of letters, digits and underscores (_) that does not begin with a digit. C++ is case sensitive—uppercase and lowercase letters are different, so a1 and A1 are different identifiers.

## Portability Tip 2.1

> C++ allows identifiers of any length, but your C++ implementation may impose some restrictions on the length of identifiers. Use identifiers of 31 characters or fewer to ensure portability.

## Good Programming Practice 2.4

> Avoid identifiers that begin with underscores and double underscores, because C++ compilers may use names like that for their own purposes internally. This will prevent names you choose from being confused with names the compilers choose.

## Error-Prevention Tip 2.1

> Languages like C++ are “moving targets.” As they evolve, more keywords could be added to the language. Avoid using “loaded” words like “object” as identifiers. Even though “object” is not currently a keyword in C++, it could become one; therefore, future compiling with new compilers could break existing code.

Declarations of variables can be placed almost anywhere in a program, but they must appear before their corresponding variables are used in the program. For example, in the program of Fig. 2.5, the declaration in line 9

```
int number1; // first integer to add
```

could have been placed immediately before line 14

```
std::cin >> number1; // read first integer from user into number1
```

Line 13

```
std::cout << "Enter first integer: "; // prompt user for data
```

prints the string Enter first integer: on the screen. We like to pronounce the preceding statement as “std::cout gets the character string "Enter first integer: ". ” Line 14

```
std::cin >> number1; // read first integer from user into number1
```

uses the input stream object cin (of namespace std) and the stream extraction operator, >>, to obtain a value from the keyboard. Using the stream extraction operator with

std::cin takes character input from the standard input stream, which is usually the keyboard. We like to pronounce the preceding statement as, “std::cin gives a value to number1” or simply “std::cin gives number1.”

## Error-Prevention Tip 2.2

Programs should validate the correctness of all input values to prevent erroneous information from affecting a program’s calculations.

When the computer executes the preceding statement, it waits for the user to enter a value for variable number1. The user responds by typing an integer (as characters), then pressing the Enter key (sometimes called the Return key) to send the characters to the computer. The computer converts the character representation of the number to an integer and assigns (i.e., copies) this number (or value) to the variable number1. Any subsequent references to number1 in this program will use this same value.

Line 16

```
std::cout << "Enter second integer: "; // prompt user for data
```

prints Enter second integer: on the screen, prompting the user to take action. Line 17

```
std::cin >> number2; // read second integer from user into number2
```

obtains a value for variable number2 from the user.

The assignment statement in line 19

```
sum = number1 + number2; // add the numbers; store result in sum
```

calculates the sum of the variables number1 and number2 and assigns the result to variable sum using the assignment operator =. The = operator and the + operator are called binary operators because each has two operands. In the case of the + operator, the operands are number1 and number2. In the case of the preceding = operator, the operands are sum and the value of the expression number1 + number2.

Line 21

```
std::cout << "Sum is " << sum << std::endl; // display sum; end line
```

displays the character string Sum is followed by the numerical value of variable sum followed by std::endl—a so-called stream manipulator. The name endl is an abbreviation for “end line” and belongs to namespace std. The std::endl stream manipulator outputs a newline, then “flushes the output buffer.” This simply means that, on some systems where outputs accumulate in the machine until there are enough to “make it worthwhile” to display them on the screen, std::endl forces any accumulated outputs to be displayed at that moment. This can be important when the outputs are prompting the user for an action, such as entering data.

Note that the preceding statement outputs multiple values of different types. The stream insertion operator “knows” how to output each type of data. Using multiple stream insertion operators (<<) in a single statement is referred to as concatenating, chaining or cascading stream insertion operations. It is unnecessary to have multiple statements to output multiple pieces of data.

Calculations can also be performed in output statements. We could have combined the statements in lines 19 and 21 into the statement

```
std::cout << "Sum is " << number1 + number2 << std::endl;
```

thus eliminating the need for the variable sum.

A powerful feature of C++ is that you can create your own data types called classes (we introduce this capability in Chapter 3 and explore it in depth in Chapters 9 and 10). You can then “teach” C++ how to input and output values of these new data types using the >> and << operators (this is called *operator overloading*—a topic we explore in Chapter 11).

## 2.5 Arithmetic

Figure 2.6 summarizes the C++ *arithmetic operators*. The *asterisk* (*) indicates multiplication and the *percent sign* (%) is the modulus operator that will be discussed shortly. The arithmetic operators in Fig. 2.6 are all binary operators.

*Integer division* (i.e., where both the numerator and the denominator are integers) yields an integer quotient; for example, the expression 7 / 4 evaluates to 1 and the expression 17 / 5 evaluates to 3. Note that any fractional part in integer division is discarded (i.e., truncated)—no rounding occurs.

C++ provides the *modulus operator*, %, that yields the remainder after integer division. The modulus operator can be used only with integer operands. The expression x % y yields the remainder after x is divided by y. Thus, 7 % 4 yields 3 and 17 % 5 yields 2. In later chapters, we discuss many interesting applications of the modulus operator, such as determining whether one number is a multiple of another (a special case of this is determining whether a number is odd or even).

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_75_0.png)

> **Common Programming Error 2.3**
> 
> Attempting to use the modulus operator (%) with noninteger operands is a compilation error.

| C++ operation | C++ arithmetic operator | Algebraic expression | C++ expression |
|---|---|---|---|
| Addition | + | f + 7 | f + 7 |
| Subtraction | - | p − c | p - c |
| Multiplication | * | bm or b · m | b * m |
| Division | / | x / y or x ÷ y | x / y |
| Modulus | % | r mod s | r % s |

**Fig. 2.6**  |  Arithmetic operators.

## Parentheses for Grouping Subexpressions

Parentheses are used in C++ expressions in the same manner as in algebraic expressions. For example, to multiply a times the quantity b + c we write a * ( b + c ).

## Rules of Operator Precedence

C++ applies the operators in arithmetic expressions in a precise sequence determined by the following *rules of operator precedence*, which are generally the same as those followed in algebra:
