
# FIGURE A-3 Some special character constants

| Constant | Name |
| --- | --- |
| \n | New line |
| \t | Tab |
| \' | Single quote |
| " | Double quote |
| \0 | Zero |

You write decimal integer constants without commas, decimal points, or leading zeros. The default type of such a constant is int, if small enough, or long.

You write floating-point constants, which have a default type of double, with a decimal point. You can specify an power-of-10 multiplier by writing or E followed by the power of 10. For example, 1.2e-3 means 1.2 × 10⁻³.

Characters are enclosed in single quotes—for example, 'A' and '2'—and have a default type of char. You write a literal string as a sequence of characters enclosed in double quotes.

Several characters have a backslash, as shown in Figure A-3. This is useful when you want to embed one of these characters within a literal string. Once the program in Figure A-1 uses the new-line character \n in the string "cubic inches\n" to the end of the output with a carriage return. You will learn about using \n in the output in this appendix. You also use the backslash to specify a single quote as a character (\'') or a double quote within a character string.

Do not begin a decimal integer constant with zero.

> **Programming Tip:** Do not begin a decimal integer with zero. A constant that begins with zero is either an other constant or a hexadecimal constant.

## A.1.6 Named Constants

Unlike variables, whose values change during program execution, **named constants** have values that do not change. The declaration of a named constant is like that of an initialized variable, but the keyword precedes the data type. For example, the statement

The value of a named constant does not change

```cpp
const double PI = 3.14159;
```

declares PI as a named constant, as is the case in the sample program in Figure A-1. Once a named constant as PI is declared, you cannot assign another value. By using named constants, you may program both easier to read and easier to modify.

The standard header file clim contains constants as INT\_MIN and LONG\_MAX that specify installation-dependent maximum and minimum values for the integral data types. Likewise, the standard header file cfloat contains named constants that specify installation-dependent maximum and minimum values for the floating data types. You use the include directive to gain access to these headers.

Named constants make a program easier to read and modify

- 1 Octal and hexadecimal constants are also available, but they are not used in this book. An octal constant begins with 0, a hex constant with 0x or 0X.

## A.1.7 Enumerations

Enumeration provides another way to name integer constants. For example, the statement

```cpp
enum {SUN, MON, TUE, WED, THU, FRI, SAT};
```

is equivalent to the statements

```cpp
const int SUN = 0;
const int MON = 1;
const int SAT = 6;
```

By default, the values assigned to the constants—enumerators—begin with zero and are constant. You can, however, assign explicit values to any or all of the enumerators, as in

```cpp
enum {PLUS = '+', MINUS = '-'};
```

By naming an enumeration, you create a distinct integral type. For example,

```cpp
enum Season {WINTER, SPRING, SUMMER, FALL};
```

creates a type Season. The variable whichSeason, declared as Season whichSeason; can have WINTER, SPRING, SUMMER, or FALL. This use of named enumerations instead of int can make your program easier to understand.

## A.1.8 The typedef Statement

You use the typedef to give another name to an existing data type. In this way, you can make your program easier to modify and read. For example, the statement

```cpp
typedef double Real;
```

declares Real a synonym for double and allows you to use Real and double interchangeably. Suppose that you revise the program in Figure A-1 by using Real as follows:

```cpp
int main() {
    typedef double Real;
    const Real PI = 3.14159;
    Real radius;
    cout << "Enter the radius of the sphere: ";
    cin >> radius;
    volume = 4 * PI * radius * radius / 3;
}
```

At first glance, this does not seem to be advantageous as the original version, suppose that you decide to increase the precision of your computation by declaring PI, radius, and volume as long instead of double. In the original version (Figure A-1), you would have to change each occurrence of double to long.

```cpp
typedef long Real;
```

Realize that typedef does not create a new type, but simply creates a name for a type. C++, however, provides a way to create your own types.

## A.1.9 Assignments and Expressions

An expression is formed by combining variables, constants, operators, and parentheses. The assignment statement

```cpp
volume = 4 * PI * radius / 3;
```

assigns to the previously declared volume the value of the arithmetic expression on the right. The various kinds of expressions that you can use in assignment statement are discussed next.

Arithmetic expressions. You can combine variables and constants with arithmetic operators and parentheses to form arithmetic expressions. The arithmetic operators are

- Binary add or unary plus
- Binary subtract or unary minus
- Multiply
- Divide
- Remainder after division

The operators *, and % have the same precedence, which is higher than + and -. unary operators have higher precedence than binary operators. The following examples demonstrate operator precedence:

```cpp
a - b / c    means (b/c) (precedence of /)
-5 / a        means (-5)/a (precedence of unary)
a / -5        means a/(-5) (precedence of unary)
```

Arithmetic operators and most other operators are left-associative. That is, execute from left to right within an expression. Thus,

```cpp
a * b / c
```

```

The assignment operator and all unary operators are right-associative, as you will see later. You can use parentheses to override precedence and associativity.

Relational and logical expressions. You can combine variables and constants with the relational, or comparison, operators <, >, and the equality operators == (equal to) and != (not equal) to form a relational expression. Such an expression is true or false according to the validity of the specified expression 5 == 4 has a value of false because 5 is not equal to 4. Equality operators have a lower precedence than relational operators.

You can combine variables and constants of the arithmetic types, relational expressions, and the logical operators && (and) and || (or) to form logical expressions, which are either true or false. C++ evaluates logical expressions from left to right and stops as soon as the value of the entire expression is

2 A list of all C++ operators and their precedences appears inside the cover of this book.
3 A unary operator requires only one operand; for example, the - in -5. A binary operator requires two operands; for example, the + in 2+3.

## APPENDIX A Review of C++ Fundamentals

Sometimes the value of a logical expression is apparent before it is completely examined as C++ uses short-circuit evaluation. C++ determines the value of each of the following expressions without evaluating (a < b):

```cpp
(5 == 4) && (a < b) // False since (5 == 4)
(5 == 5) || (a < b) // True since (5 == 5) is true
```

> **Programming Tip:** Remember that = is the assignment operator; == is the equality operator.

## Conditional expressions. The expression

expression₁, expression₂ : expression₃
has value of either expression₁, or expression₂, according to which expression, is true or false, respectively. For the statement

```cpp
larger = ((a > b) ? a : b);
```

assigns the larger of a and b to larger, because the expression a > b is true if a is larger than b and if not.

## Implicit type conversions. Automatic conversions from one data type to another can occur during assignment and during evaluation. For assignments, the data type of the expression on the right-hand side of the assignment operator is converted to the data type of the item on the left-hand side just before the assignment occurs. Floating-point values are truncated—rounded—when they are converted to integer.

During the evaluation of an expression, values of char or short are converted to int. Similarly, any enumer value is converted to int if int represents all the values of that particular enumeration; otherwise, it is converted to unsigned. These conversions are called integral promotions. After these conversions, if the operator differs in data type, the data type that is lower in the following hierarchy is converted to one that is (in least):

```
int -> unsigned -> long -> unsigned long -> float -> double -> long double
```

For example, if a is long and b is float, a + b is float. Only of a’s long value is converted to float prior to the addition, so that the value stored at is unchanged.

## Explicit type conversions. You can explicitly convert from one data type to another using a static_cast<type>(expression) with the following notation:

```cpp
static_cast<type>(expression)
```

converts expression to the data type type. For example, static_cast<int>(14.9) converts the double value 14.9 to int 14. Thus, the sequence
```cpp
double value = 14.9;
cout << static_cast<int>(volume);
```

displays 14 does not change the value of the volume.

## Other assignment operators. In addition to the assignment operator =, C++ provides several two-character assignment operators that perform another operation before assignment. For example,

```cpp
a += b means a = a + b
```

Other operators, such as -=, *=, /, and %, have analogous meanings.
