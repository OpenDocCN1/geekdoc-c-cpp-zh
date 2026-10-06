# 4. Data Types and Expressions

In this chapter, we take a look at the basic data types and describe some fundamental rules for forming arithmetic expressions in Objective-C.

# Data Types and Constants

You have already encountered the Objective-C basic data type int. As you will recall, a variable declared to be of type int can be used to contain integral values only—that is, values that do not contain decimal digits.

The Objective-C programming language provides three other basic data types: float, double, and char. A variable declared to be of type float can be used for storing floating-point numbers (containing decimal digits). The double type is the same as type float, typically with roughly twice the range. Finally, the char data type can be used to store a single character, such as the letter a, the digit character 6, or a semicolon (more on this later).

In Objective-C, any literal number, single character, or character string is known as a constant. For example, the number 58 represents a constant integer value. The string @"Programming in Objective-C is fun." is an example of a constant string object. Expressions consisting entirely of constant values are called constant expressions. So this expression is a constant expression because each of the terms of the expression is a constant value:

```
128 + 7 - 17
```