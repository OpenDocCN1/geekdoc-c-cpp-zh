
However, even with 256 characters, the extended ASCII character set cannot represent the world's alphabets, especially given the various Asian alphabets and their many thousands of ideograms. Therefore, the developers of the Java programming language chose the Unicode character set, which uses 16 bits per character, supporting 65,536 unique characters (and techniques that allow even more characters to be represented using multiple bytes). The characters and symbols from many languages are included in the Unicode definition. ASCII is a subset of the Unicode character set, comprising the first 128 characters. Appendix C discusses the Unicode character set in more detail.

A character set assigns a particular number to each character, so by definition the characters are in a particular order. This is referred to as lexicographic order. In the ASCII and Unicode ordering, the digit characters '0' through '9' are continuous (no other characters intervene) and in order. Similarly, the lowercase alphabetic characters 'a' through 'z' are continuous and in order, as are the uppercase alphabetic characters 'A' through 'Z'. These characteristics make it relatively easy to keep things in alphabetical order.

In Java, the data type char represents a single character. The following are some examples of character variable declarations in Java:

```java
char topGrade = 'A';
char symbol1, symbol2, symbol3;
char terminator = ';', separator = ' ';
```

## Booleans

A boolean value, defined in Java using the reserved word boolean, has only two valid values: true and false. A boolean variable is usually used to indicate whether a particular condition is true, but it can also be used to represent any situation that has two states, such as a light bulb being on or off.

A boolean value cannot be converted to any other data type, nor can any other data type be converted to a boolean value. The words true and false are reserved in Java as boolean literals and cannot be used outside of this context.

The following are some examples of boolean variable declarations in Java:

```java
boolean flag = true;
boolean tooHigh, tooSmall, tooRough;
boolean done = false;
```

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

- SR 2.14 What is primitive data? How are primitive data types different from objects?
- SR 2.15 How many values can be stored in an integer variable?
- SR 2.16 What are the four integer data types in Java? How are they different?
- SR 2.17 What type does Java automatically assign to an integer literal? How can you indicate that an integer literal should be considered a different type?
- SR 2.18 What type does Java automatically assign to a floating point literal? How can you indicate that a floating point literal should be considered a different type?
- SR 2.19 What is a character set?
- SR 2.20 How many characters are supported by the ASCII character set, the extended ASCII character set, and the Unicode character set?

## 2.4 Expressions

An *expression* is a combination of one or more operators and operands that usually perform a calculation. The value calculated does not have to be a number, but it often is. The operands used in the operations might be literals, constants, variables, or other sources of data. The manner in which expressions are evaluated and used is fundamental to programming. For now we will focus on arithmetic expressions that use numeric operands and produce numeric results.

> **KEY CONCEPT**
> Expressions are combinations of operators and operands used to perform a calculation.

### Arithmetic Operators

The usual arithmetic operations are defined for both integer and floating point numeric types, including addition (+), subtraction (-), multiplication (*), and division (/). Java also has another arithmetic operation: The *remainder operator* (%) returns the remainder after dividing the second operand into the first. The remainder operator is sometimes called the modulus operator. The sign of the result of a remainder operation is the sign of the numerator. Therefore:

| Operation | Result |
| --- | --- |
| 17 % 4 | 1 |
| -20 % 3 | -2 |
| 10 % -5 | 0 |
| 3 % 8 | 3 |

**VideoNote:** Review of primitive data and expressions.

As you might expect, if either or both operands to any numeric operator are floating point values, the result is a floating point value. However, the division operator produces results that are less intuitive, depending on the types of the operands. If both operands are integers, the / operator performs integer division, meaning that any fractional part of the result is discarded. If one or the other or both operands are floating point values, the / operator performs floating point division, and the fractional part of the result is kept. For example, the result of 10/4 is 2, but the results of 10.0/4 and 10/4.0 and 10.0/4.0 are all 2.5.

A unary operator has only one operand, while a binary operator has two. The + and − arithmetic operators can be either unary or binary. The binary versions accomplish addition and subtraction, and the unary versions represent positive and negative numbers. For example, −1 is an example of using the unary negation operator to make the value negative. The unary + operator is rarely used.

Java does not have a built-in operator for raising a value to an exponent. However, the Math class provides methods that perform exponentiation and many other mathematical functions. The Math class is discussed in Chapter 3.

### Operator Precedence

Operators can be combined to create more complex expressions. For example, consider the following assignment statement:

```java
result = 14 + 8 / 2;
```

> **KEY CONCEPT**
> Java follows a well-defined set of precedence rules that governs the order in which operators will be evaluated in an expression.

The entire right-hand side of the assignment is evaluated, and then the result is stored in the variable. But what is the result? If the addition is performed first, the result is 11; if the division operation is performed first, the result is 18. The order of operator evaluation makes a big difference. In this case, the division is performed before the addition, yielding a result of 18.

Note that in this and subsequent examples, we use literal values rather than variables to simplify the expression. The order of operator evaluation is the same if the operands are variables or any other source of data.

All expressions are evaluated according to an operator precedence hierarchy that establishes the rules that govern the order in which operations are evaluated. The arithmetic operators generally follow the same rules you learned in algebra. Multiplication, division, and the remainder operator all have equal precedence and are performed before (have higher precedence than) addition and subtraction. Addition and subtraction have equal precedence.

Any arithmetic operators at the same level of precedence are performed left to right. Therefore we say the arithmetic operators have a *left-to-right association*.

Precedence, however, can be forced in an expression by using parentheses. For instance, if we really wanted the addition to be performed first in the previous example, we could write the expression as follows:

```java
result = (14 + 8) / 2;
```

Any expression in parentheses is evaluated first. In complicated expressions, it is good practice to use parentheses, even when it is not strictly necessary, to make it clear how the expression is evaluated.

Parentheses can be nested, and the innermost nested expressions are evaluated first. Consider the following expression:

```java
result = 3 * ((18 - 4) / 2);
```

In this example, the result is 21. First, the subtraction is performed, forced by the inner parentheses. Then, even though multiplication and division are at the same level of precedence and usually would be evaluated left to right, the division is performed first because of the outer parentheses. Finally, the multiplication is performed.

After the arithmetic operations are complete, the computed result is stored in the variable on the left-hand side of the assignment operator (=). In other words, the assignment operator has a lower precedence than any of the arithmetic operators.

The evaluation of a particular expression can be shown using an *expression tree*, such as the one in Figure 2.3. The operators are executed from the bottom up, creating values that are used in the rest of the expression. Therefore, the operations lower in the tree have a higher precedence than those above, or they are forced to be executed earlier using parentheses.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_104_0.png)

**FIGURE 2.3** An expression tree
