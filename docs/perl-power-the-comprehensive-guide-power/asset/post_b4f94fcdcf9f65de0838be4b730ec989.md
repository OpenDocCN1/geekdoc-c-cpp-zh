
## CHAPTER 5 Scalars and Formatting

$ThirdValue) to which you assigned values. Figure 5.2 illustrates the output as items 1.1 and 1.3.

The lines at comment #3 call the `undef()` function to remove the definition you have given the identifier `$FirstValue`. Given this operation, the `defined()` function in the selection statement returns false. In Figure 5.2, you see no message printed for item 2.1. This proves somewhat unhelpful if you are trying to debug code. The code associated with the final comment, comment #4, provides an alternative. You use the negation of the `defined()` function (!) to allow the selection statement to print a message that confirms that the identifiers `$FirstValue` and `$SecondValue` have not been defined. The output, as shown in items 3.1 and 3.2 of Listing05_02, tells the story.

## Figure 5.2

Use the `undef()` and `defined()` functions to establish legitimate values.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_120_0.png)

## Operations with Numbers

When you perform operations on numbers in Perl, the operators you employ differ from the operators that apply to strings. For example, you employ `eq` to test for the equality of strings, but you employ double equal signs (`==`) to perform a similar operation with numbers. Generally, the numeric operators that Perl provides resemble those of other programming languages (such as C or C++). Table 5.1 provides a summary of operators that the Perl interpreter allows you to use.

The operators for both strings and numbers are characterized by how they can be associated (associativity) and what precedence they have with relation to each other. Precedence has to do with the order in which the interpreter performs operations. The operators listed in Table 5.1 appear in a top-down scheme of precedence. At the top are the parentheses, which stand as what might be viewed as the super operators of operators, for they allow you to arbitrarily enforce the precedence of almost any operation you want to perform.

As Figure 5.3 illustrates, associativity involves how the interpreter reads an expression. In some cases, it reads left to right. In other cases it reads right to left. In still other cases, associativity does not apply. Left-to-right associations characterize all the arithmetic operators. If you add the variables a and b (a + b), the interpreter reads b, reads the addition operator, and then reads a. On the other hand, with the assignment operator (=), the association is from right to left. When you assign the sum of a and b to an identifier named c (c = a + b), the interpreter attends first to the addition (a + b), then to the assignment operator (=), and then to the target identifier (c), which lies on the left side of the assignment operator.

## Associativity

$ValueC = $ValueA + $ValueB;

$ValueA + $ValueB;

Right-to-left

Left-to-right

## Precedence

$ValueE = ($ValueA + $ValueB * $ValueC) + $ValueD;

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_121_0.png)

## Table 5.1 Numerical Operators

| Category | Operators | Description |
|---|---|---|
| Grouping | ( ) | Ensures that you can control how operations impact each other. Parentheses allow you to group operations visually if you lack certainty about the precedence of operators. The interpreter associates items in parentheses from left to right. |
| Unary | ++$c $c++ --$d $d-- | Allows you to successively increment or decrement a value. Unary operators immediately affect variables, so next to the parentheses, they have the highest precedence of any operator. Since unary operators involve only one operand (identifier), there is no associativity. |
| Arithmetic | * / % + - | Standard arithmetic operators. Multiplication and division have higher precedence than the modulus (remainder) operator, and these three operators in turn have higher precedence than addition and subtraction. All math operations are associated on a left-to-right basis. |
| Relational | > < >= <= | Allows you to evaluate the relations that pertain between values. After you increment, decrement, or perform arithmetic operations, you conduct relational evaluations. Since relational operators do not involve combinations of values, they have no associativity. |
| Equality | == != | Boolean operations require you to evaluate expressions according to equality or lack of equality. Equality and inequality have no associativity. |
| Assignment | = | You assign the results of operations after performing them, so it makes sense that the assignment operator has relatively low precedence. Assignment always proceeds according to a right-to-left association. On the left of the assignment operator you create an expression and then assign it to the value on the right of the assignment operator. |
| Augmentation | += -= *= /= *= **= | Allows you to augment a variable and assign the result of the augmentation back to the variable. The double asterisks (**) relates to powers (exponents). These operators have slightly lower precedent than the lone assignment operator. If you lined up three values, two related by the assignment operator and two by one of the augmentation operators, the assignment would occur prior to the augmentation. Augmentation proceeds according to right-to-left associativity. You create an expression on the right side of the augmentation operator, and the interpreter assigns the result to the value on the left. |

## Numbers and Built-In Functions

As with string operations, life becomes particularly interesting when you begin using Perl’s built-in functions to perform operations that only painstaking hours of labor would allow you to perform if you were to work from scratch with the basic operators and create your own functions. Although programmers often report that it does not provide an ideal language for mathematical programming (C is generally viewed as the best of all languages in this respect), Perl makes use of the C math library and provides a good set of math functions. Table 5.2 lists some of these functions.

## Table 5.2 Perl Math Functions

| Function | Discussion |
|---|---|
| abs() | Returns the absolute value of the number you supply. |
| atan2() | Returns the arctangent of the value you supply. The return value is in the range of pi to–pi (in radians). |
| `cos()` | Returns the cosine of the argument you supply. The return value is in radians. |
| `exp()` | Returns e to the power of the argument you supply. To raise a number to a power, use the double asterisks (number ** 3). |
| `hex()` | Returns the decimal value of a hexadecimal number. |
| `int()` | If you have a decimal number, this function returns the integer part of the number. |
| `log()` | Returns the natural logarithm of a number. |
| `sin()` | Returns the sine of the argument you supply. The return value is in radians. |
| `sqrt()` | Returns the square root of the number you supply to it. |
| `square()` | Returns the square of the number you supply to it. |
| `oct()` | Returns the decimal value of an octal number. |
| `ord()` | If you supply a character (in single quotes `c`) to this number, it returns the ASCII value of the character. |
| `rand()` | Returns a rational number greater than or equal to 0 and less than 1 (0.1, 0.2, and so on). However, if you supply an integer argument to the `rand()` function, it generates an integer that is greater than or equal to 0 and less than the number you supply. To deal with most situations, programmers use a tactic called shifting. To shift the return of `rand()` so that you get randomly generated values of 1, 2, 3, 4, and 5, you use an expression along the following lines: `1 + int(rand(5))`. |
| `sin()` | Returns the sine of the number you supply. The value returned is in radians. |
| `srand()` | To make it so that you get different results each time you call the `rand()` function, you help it out by seeding a different starting value into the formula the `rand()` function uses. To accomplish this, you use the `srand()` (for “seed” random) function. |
| `time()` | The number of seconds since January 1, 1970. There are 3,600 seconds in an hour, so the numbers tend to be large. |

## Standard Presentation Using the print() Function

To gain a sense of some of the basic alternatives that exist for you as you formulate numeric expressions in Perl, consider Listing05_03. This program provides a set of numeric identifiers and a display of the values the identifiers store. The program provides a starting point for experimentation in the use of formatting, conversion, printing, and other Perl capabilities.

```perl
#Listing05_03
#Scalars initialized to numbers
# Integers
```
