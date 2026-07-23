![](cover.jpg)

![cover](cover.jpg)

Problem Solving in C and Python

Programming Exercises and Solutions, Part I

By Yana Kortsarts, Yulia Kempner, Leonid Kugel & Adam Fischbach (Editor)

Copyright © 2018 Yana Kortsarts

Smashwords Edition, License Notes

Thank you for downloading this ebook. This book remains the copyrighted property of the author, and may not be redistributed to others for commercial or non-commercial purposes. If you enjoyed this book, please encourage your friends to download their own copy from their favorite authorized retailer. Thank you for your support.

Table of Contents

[Preface](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_002.html_Preface)

[Chapter 1: Variables, Input/Output, and Arithmetic Operators](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_003.html_Ch1)

[I. Theory Overview](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_003.html_TheoryOverview)

[1. Variables](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_003.html_Variables)

[2. Input, Output](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_003.html_InpuOutput)

[3. Assignment Operator and Assignment Statement](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_007.html_Assigment)

[4. Arithmetic Operators](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_008.html_ArithmeticOperators)

[a. Binary Arithmetic Operators](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_008.html_Binary)

[b. Unary Arithmetic Operators](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_008.html_Unary)

[c. Compound Assignment Statements](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_009.html_Compound)

[d. Operator Precedence](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_010.html_OpPrec)

[5. Constant Variables](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_016.html_ConstantVariables)

[6. Comments](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_016.html_Comments)

[II. Problem Solving Approach Guidelines](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_017.html_II)

[III. Sample Solutions in Python and C](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_018.html_III)

[IV. Practice Exercises](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_020.html_IV)

[V. Chapter 1 Appendix 1: Sample Quiz in Python](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_021.html_V)

[VI. Chapter 1 Appendix 2: Sample Quiz in C](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_023.html_VI)

[VII. Chapter 1 Appendix 3: Modulo Operator in Python - Negative Numbers Case](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_025.html_VII)

[VIII. Chapter 1 Appendix 4: Modulo Operator in C - Negative Numbers Case](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_026.html_VIII)

[IX. Chapter 1 Appendix 5: Increment and Decrement Operator in C – Special Cases](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_027.html_IX)

[Chapter 2: Decision Structures](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_028.html_Chapter2)

[I. Theory Overview](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_003.html_TheoryOverview)

[1. Relational Operators](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_028.html_Relational)

[2. Boolean Expression](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_028.html_BooleanExpression)

[3. Logical (Boolean) Operators and Boolean Logic](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_029.html_LogicalBoolean)

[4. IF Statement](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_031.html_IfStatement)

[5. IF ELSE Statement](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_032.html_IfELSE)

[6. IF ELIF ELSE Statement in Python and IF ELSE-IF ELSE Statement in C](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_034.html_Six)

[7. Nested Decision Structures](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_035.html_Seven)

[8. SWITCH Statement in C](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_037.html_Eight)

[II. Sample Solutions in Python and C](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_039.html_Sample)

[III. Practice Exercises](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_041.html_Practice)

[IV. Chapter 2 Appendix 1: Sample Quiz in Python](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_042.html_CH2IV)

[V. Chapter 2 Appendix 1: Sample Quiz Questions in Python](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_044.html_Ch2)

[Chapter 3: Loops](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_046.html_Ch3)

[I. Theory Overview](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_046.html_Ch3TheoryOverview)

[1. Loops in Python](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_046.html_Loops)

[i. while loop](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_046.html_While)

[ii. for loop](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_052.html_ForLoop)

[iii. nested loops](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_048.html_Nested)

[2. Loops in C](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_050.html_LoopsInC)

[i. while loop](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_050.html_WhileLoop)

[ii. do while loop](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_052.html_DoWhile)

[iii. for loop](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_052.html_ForLoop)

[iv. nested loops](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_055.html_NestedLoops)

[v. break statement](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_056.html_Break)

[II. Sample Solutions in Python and C](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_057.html_IISample)

[III. Practice Exercises](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_058.html_VPractice)

Preface

This book is a collection of exercises for the introductory programming course. We are focusing on two programming languages: Python and C. Each chapter provides a short overview of the necessary theoretical material for both programming languages, sample solutions written in C and Python 3 (version 3.5.1, the most recent version of Python at the time the book was written), and a list of practice exercises in increasing order of difficulty.

Disclaimer: most of the problems are not original problems; in some cases the appropriate references are provided, but in many cases the problems are drawn from mathematical and programming folklore.

Chapter 1: Variables, Input/Output, and Arithmetic Operators

I. Theory Overview

1\. Variables

Variables are placeholders for some values. Programs utilize variables to store data. Variables have three attributes: type, name, and value. In addition, each variable has a memory address. Memory addresses are used to access the variable to perform the following tasks: assign an initial value through input or declaration statements, retrieve the current value, and change the value. In most cases, the use of memory will be done automatically, but some statements require using specific syntax discussed later in this chapter.

Variables in Python

In Python, initialization is required. The type of the variable will be determined automatically based on the assigned value. There are two basic types: numeric and strings. Numeric types include integers (int) and floating point numbers (float). A string is a sequence of characters. String literals are enclosed in the single or double quotes. A character is not a separate data type but a string of exactly one character.

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_556d3f69.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_556d3f69.png)

Variables in C

In C, declaration is required prior using the variable and initialization is optional. In C, there are four standard signed integer types: char, short, int, and long; there are three real floating point types: float, double, and long double.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_1bb06e7d.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_1bb06e7d.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3c83f9.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3c83f9.jpg)

Declaration Statements Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6446e3a7.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6446e3a7.jpg)

Declaration and Initialization Statements Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4529b736.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4529b736.jpg)

2\. Input/Output

Input in Python

The input function is used to perform standard input – input from the keyboard.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4cb0fff0.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4cb0fff0.jpg)

Output in Python

The print function is used to perform standard output – output to the screen. To print text, single ('), double ("), or triple (""") quotes could be used. Triple quotes allow text to be printed on multiple lines. To print the value of the variable, use the name of the variable without any quotes. To format output, use the format function.

Basic Escape Sequences in Python

The backslash (\) character is used to *escape* characters that otherwise have a special meaning in Python.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3bb30a94.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3bb30a94.png)

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3d016fa1.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3d016fa1.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_1ca208b0.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_1ca208b0.png)

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_56d8fa87.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_56d8fa87.jpg)

For more information on printing and formatting floating point numbers see: [https://docs.python.org/3/tutorial/floatingpoint.html](https://docs.python.org/3/tutorial/floatingpoint.html)

Input in C

The scanf function is used to perform standard input – input from the keyboard. For the variable types we have introduced so far, the general syntax for a scanf statement is as follows:

scanf("list of format specifiers", list of variables);

Note:

1\. In the list of variables, each variable preceded by the ampersand sign (&) which denotes the address of the variable in the computer’s memory. For the variable types we have introduced so far, the ampersand sign is required before each variable name in order for scanf to be able to store the input value. Omitting the ampersand sign will not cause a compiler error, but instead can cause a segmentation fault, a run-time error which is a program error that occurs while the program is running. Run-time errors cause the immediate exit (termination) of the program.

2\. Most C compilers will not check the correspondence between the format specifier and the type of the variable. A format type mismatch will not cause a compiler error, but instead will result in a logic error. Logic errors will not terminate the program, but will cause the program to produce the wrong output.

3\. We advise not to include spaces or any other characters and numbers between format specifiers to avoid run-time and/or logic errors. Inconsistency between the scanf format string and the format your data is entered will result in run-time and/or logic errors. For example, the following statement,

scanf("%d,%d,%d", &a, &b, &c);

requires input integers to be separated by commas, otherwise a run-time and/or logic error occurs.

4\. For the variable types we have introduced so far, the scanf format specifiers, %d, %f, %lf, and %Lf, skip all leading whitespace characters and terminate on whitespace characters. In addition, %d terminates on any non-digit character. The format specifier, %c, does read whitespaces. This fact requires careful treatment while reading characters after numeric data.

Basic scanf Formatting Options

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_17e9cdcf.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_17e9cdcf.jpg)

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_8f4504.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_8f4504.png)

Reading characters after numeric data

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m17a25539.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m17a25539.jpg)

In addition, there are several functions that read a single character. In this book we will limit our use to the getchar() function that reads a character from standard input.

Example:

char c;
c=getchar();

Note: the storage sizes of the variables in C are platform dependent.

Output in C

The printf()function is used to perform standard output – output to the screen. To print text, the text must be enclosed in double quotes ("). To print the value of a variable, use the corresponding format specifier and the name of the variable without any quotes.

The general syntax for the printf statement is as follows:

printf("list of format specifiers", list of variables);

Note: Most C compilers will not check the correspondence between format specifier and the type of the variable. A format type mismatch will result in logical errors.

Basic printf Formatting Options

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m6ce61650.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m6ce61650.jpg)

Basic Escape Sequences in C

The backslash (\) character is used to *escape* characters that otherwise have a special meaning in C.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_31848d43.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_31848d43.jpg)

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_589b3268.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_589b3268.jpg)

Additional scanf/printf Formatting Options

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m1743cb18.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m1743cb18.jpg)

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_md653b57.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_md653b57.jpg)

3\. Assignment Operator and Assignment Statement

In C and Python, the = operator is called the assignment operator and is used to construct the assignment statement.

In Python, the assignment statement has the following form:
variable_name = expression

In C, the assignment statement has the following form:
variable_name = expression;

This statement is executed in the following order:

1\. Expression is evaluated

2\. Expression value is assigned to the variable.

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_abc0fa1.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_abc0fa1.jpg)

4\. Arithmetic Operators

Binary Arithmetic Operators in Python for Numeric Types (int and float)

(For references see:
[https://docs.python.org/3/library/stdtypes.html](https://docs.python.org/3/library/stdtypes.html),
[https://docs.python.org/3/reference/expressions.html](https://docs.python.org/3/reference/expressions.html))

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_61af76e1.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_61af76e1.jpg)

Unary Arithmetic Operator in Python for Numeric Types (int and float)

(For references see: [https://docs.python.org/3/library/stdtypes.html](https://docs.python.org/3/library/stdtypes.html))

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m407d996d.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m407d996d.jpg)

Note: Python fully supports mixed arithmetic: when a binary arithmetic operator has operands of different numeric types, the operand with the “narrower” type is widened to that of the other, where integer is narrower than floating point.

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m5413c68f.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m5413c68f.jpg)

Augmented (Compound) Assignment Operators and Statements in Python

(For reference see: [https://docs.python.org/3/reference/simple_stmts.html#augmented-assignment-statements](https://docs.python.org/3/reference/simple_stmts.html#augmented-assignment-statements))
Augmented assignment combines assignment and a binary arithmetic operator in a single statement.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m796abb4f.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m796abb4f.jpg)

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5c3ea68b.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5c3ea68b.jpg)

Basic Arithmetic Operator Precedence in Python in Descending Priority (from highest precedence to lowest precedence).

(For references see: [https://docs.python.org/3/reference/expressions.html#operator-precedence](https://docs.python.org/3/reference/expressions.html#operator-precedence))

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m1253ab5b.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m1253ab5b.jpg)

Note:

1) Parentheses will change the priority order. The expression in the parentheses will be evaluated first. See example below:
2–3*2 = 2–6 = -4 compare to (2-3)*2 = (-1)*2 = -2

2) The power operator binds more tightly than unary operators on its left; it binds less tightly than unary operators on its right: in the non-parenthesized sequence of power and unary operators, the operators are evaluated from right to left. See examples below:

-1 ** 2 = 1

10 ** -2 = 0.01

Basic Numeric Operators for String Type (For references see: [https://docs.python.org/3/library/stdtypes.html](https://docs.python.org/3/library/stdtypes.html))

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m2d4603e3.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m2d4603e3.jpg)

Basic Data Type Conversion in Python For references see: [https://docs.python.org/3/library/stdtypes.html](https://docs.python.org/3/library/stdtypes.html) [https://docs.python.org/3/library/functions.html](https://docs.python.org/3/library/functions.html))

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6696f8f4.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6696f8f4.jpg)

Binary Arithmetic Operators in C for Numeric Types (int, float, double)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_314c8d53.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_314c8d53.jpg)

Note: C fully supports mixed arithmetic: when a binary arithmetic operator has operands of different numeric types, the operand with the “narrower” type is widened to that of the other, where integer is narrower than float, and float is narrower than double.

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m62651ed8.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m62651ed8.jpg)

Unary Arithmetic Operator in C for Numeric Types (int, float, double)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4aae4ce5.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4aae4ce5.jpg)

*Note: in some cases using increment and decrement operators within expressions in combination with other operators result in undefined behavior. It is considered a good practice to avoid using these operators within expressions to avoid ambiguity and confusion* ([See Chapter 1 Appendix 3](#tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI.ch.fixed.fc.tidied.stylehacked.xfixed_split_025.html_ref_App3)).

Basic Arithmetic Operators Precedence in C in Descending Priority (from highest precedence to lowest precedence).

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_79db2db9.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_79db2db9.jpg)

Note:

1) Parentheses will change the priority order. The expression in the parentheses will be evaluated first.

2) Postfix increment/decrement have high precedence, but the actual increment or decrement of the operand is done at the end of statement execution.

Example:

If x=3 and y=5 then x*y++ is 15 and y=6 by the end of the statement execution. Pay attention, the value of y used in the calculation is 5, the value of y prior to increment.

Basic Data Type (Type Casting) Conversion in C

The C programming language allows conversion from one data type to another data type using the cast operator: (new_data_type)expression

Integer promotion: in C, integer data types smaller than int or unsigned int (for example char and short) are promoted automatically to int or unsigned int during the calculation process.

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4151c9cd.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4151c9cd.jpg)

Constant Variables

In **C**, constant variables (constants) are variables with a value that cannot be modified throughout the program. There are several ways to declare a constant variable in C:

1) Using the #define preprocessor directive as follows:

#define VARIABLE_NAME value

For example:

#define PI 3.14

#define PASSIGN_GRADE 60

Note: there is no semicolon at the end of the #define statement

The #define preprocessor directives usually follow #include directives at the top of your program.

2) Using the const keyword in the declaration statement before the name of the variable.

For example:

int const PASSING_GRADE = 60;

float const PI = 3.14;

To distinguish constants from the non-constant variables, it is advisable to name them using all capital letters with underscores separating the words.

**Python** does not have true constant variables, but we can use the same naming convention as above using all capital letters for certain variables to indicate that their values are not meant to be modified throughout the program.

For example:

PI = 3.14

PASS_GRADE = 60

Why use constants in your program?

In many programs you will have a situation when the same number or character is used repeatedly throughout the program. In this case, it is advisable to declare the constant variable to hold the repetitive number or character. This allows quick and easy access to the constant variable’s value. If we need to update our code and modify the initial value of the constant variable we only need to do it once in the declaration or #define statement. Declaring a constant variable also gives a number or a character a descriptive label explaining its meaning.

Comments

In Python, a comment starts with the hash character, #, and extends to the end of the physical line. Comments in Python can be anywhere in the program.

In C, a comment starts with a slash asterisk /* and ends with an asterisk slash */ and can be anywhere in the program. Comments can span several lines within a C program.

Note: later versions of C support // as a comment (C++ style). In this case, the comment starts with double slash, //, and extends to the end of the physical line and can be anywhere in the program.

II. Problem Solving Guidelines

1\. Read the problem thoroughly.

2\. Answer the questions using the discussion template below.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m69ba3839.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m69ba3839.jpg)

3\. Use meaningful variable names.

4\. Design an example of sample input/output. You can use this example to later test your program for correctness. Do calculations by hand to determine what the program must do to solve the problem.

5\. Note: in this chapter many problems will include input limitations such requiring the input variable to be positive or non-negative. In the next chapter you will learn how to resolve these limitations within the program.

III. Sample Problems and Solutions in Python and C

**Problem 1:** Write a program that reads two integers and calculates their sum, product, and difference.

Solution Version 1

Discussion

Input: two integers stored in variables first_num and second_num.

Output: sum, product and difference of the input numbers, stored in sum, product and difference, all integer types.

Calculations:

first_num+second_num assigned to variable sum first_num*second_num assigned to variable product first_num-second_num assigned to variable difference

Input Limitations: none.

Output Limitations: none.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m584935e.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m584935e.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m778bba95.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m778bba95.jpg)

Solution Version 2:

Discussion

This version demonstrates a different style of naming the variables and the ability to include calculations within a print statement.

Input: two integers, stored in variables firstNum and secondNum.

Output: sum, product and difference of the input numbers, all integer types, and calculations included within print/printf statement.

Calculations:
firstNum+secondNum (sum)
firstNum*secondNum (product)
firstNum-secondNum (difference)

Input Limitations: none.

Output Limitations: none.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_ma31ed17.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_ma31ed17.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m3d98c0e0.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m3d98c0e0.png)

**Problem 2:** Write a program that asks to user to enter cost of the electric bill, water bill and gas bill for one month and finds the total cost of utilities for that month.

Discussion

Input: three floating point numbers, stored in variables electricity, water and gas.

Output: the sum of all utility bills, stored in variable total, floating point.

Calculations: electricity + water + gas

Input Limitations: all input values must be non-negative.

Output Limitations: none.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_39298c9.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_39298c9.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m40dc3a20.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m40dc3a20.jpg)

**Problem 3:** Write a program that reads two integers and calculates their average

Discussion

Input: two integers, stored in variables firstNum and secondNum.

Output: the average of the input numbers, floating point.

Calculations: (firstNum+secondNum)/2

Input Limitations: none.

Output Clarification: the average of two integers is not necessary an integer. For example, the average of 1 and 2 is 1.5\. In C, division of integers yields a TRUNCATED integer. To find a quotient in C, at least one of the numbers must be cast to float or double.

The following formula will be used (firstNum+secondNum)/2.0 in C solution. In this case, mixed arithmetic rules are applied, the result has double type, and the fractional part will not be truncated.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m2339ebc5.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m2339ebc5.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m2e5c492e.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m2e5c492e.jpg)

**Problem 4:** Write a program that reads two integers and calculates their quotient (result of the division of the first number by the second number), integer quotient (integer division of the first number by the second number), and modulus (remainder from dividing the first number by the second number).

Discussion

Input: two integers, stored in variables firstNum and secondNum.

Output: quotient, result of integer division, and remainder, stored in variables quotient (floating point), integer_ quotient (integer), remainder (integer).

Calculations in Python:
firstNum/secondNum (quotient)
firstNum//secondNum (integer division)
firstNum%secondNum (remainder)

Calculations in C:
firstNum/secondNum (integer division)
firstNum%secondNum (remainder)
To find a quotient in C, at least one of the numbers must be cast to float or double.
(double) firstNum/secondNum (quotient)

Input Limitations: to avoid division by zero, secondNum cannot be zero.

Output Limitations: none.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m397da4b8.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m397da4b8.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3be57a7a.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3be57a7a.jpg)

**Problem 5:** Write a program that reads one three-digit positive integer and calculates the sum of its digits, and prints its digits on separate lines.

Discussion

Input: ONE integer between 100 and 999, stored in variable num.

Output: three digits, stored in variables lastDigit, middleDigit, and firstDigit, and their sum, stored in variable sum, all integers.

Calculations in Python: repeat three times the following sequence of calculations: modulo 10 (num%10), to find the last digit of num, and integer division, (num/10), to remove the last digit.

Calculations in C: repeat three times the following sequence of calculations: modulo 10 (num%10), to find the last digit of num, and integer division, (num//10), to remove the last digit.

Example:

num = 234
234%10 = 4 (last digit)
234 /10 = 23 in C and 234//10 = 23 in Python
23%10 = 3 (middle digit)
23/10 = 2 in C and 23//10 = 2 in Python
2%10 = 2 (fist digit)

Input Limitations: input number must be between 100 and 999.

Output Limitations: none.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_30ffbb85.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_30ffbb85.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3f69b0cf.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3f69b0cf.jpg)

**Problem 6:** Write a program that reads one character and prints the ASCII/Unicode value of the input character.

Discussion

Input: one character, stored in variable input_char.

Calculations and Output in Python: use the ord() function to convert the input character to its Unicode value.

Calculations and Output in C: use the %d format specifier in the printf statement, or assign the char variable into an int variable.

Input Limitations: none.

Output Limitations: none.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_c97e5ea.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_c97e5ea.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m699a6dd7.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m699a6dd7.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_2cd6a2ab.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_2cd6a2ab.jpg)

**Problem 7:** Write a program that reads two characters and prints the sum of their ASCII/Unicode values.

Discussion

Input: two characters, stored in variables input_char1 and input_char2.

Output: the sum of ASCII/Unicode values, stored in variable sum_code, integer.

Calculations and Input Limitations in Python: use the ord() function to convert each input character to its Unicode value.

Input Limitations in Python: the characters must be entered on separate lines - ONE character per line, the ENTER must be typed immediately after first character without any whitespaces. See example below:

Example of Input in Python:

a<ENTER>
B

Calculations in C: use the integer promotion

Input Limitations in C: the characters must be entered without any whitespaces in between. See example below:

Example of Input in C:

aB

Output Limitations: none.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m20f78080.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m20f78080.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_me63e7ff.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_me63e7ff.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m44101879.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m44101879.jpg)

Word Problems and Sample Solutions

**Problem 1:** Write a program that reads the number of nights a person stayed in a hotel, the price per night and the tax percent. The program calculates and prints the total cost of the hotel stay. For example, if the person stayed 3 nights, with $99.99 per night and a 14.5% tax, the total price for the hotel stay is $343.47.

Discussion

Input:

1\. the number of nights, stored in *nights*, integer

2\. the price per night, stored in *price*, floating point

3\. tax percent, stored in *tax*, floating point

Output: total price for hotel stay, stored in total, floating point.

Calculations:
full price per night: full_one_night = price+price*tax/100
full price per stay: total = nights*(price+price*tax/100)

Input Limitations: all input values must be positive. The number of nights must be of integer type, price per night and tax – float type.

Output Limitations: the output must be formatted with two decimal places since the program outputs the money value.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3088619b.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3088619b.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m6311d1f2.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m6311d1f2.jpg)

**Problem 2:** A dairy farm ships milk bottles using containers of a specific size. Each container holds a certain number of milk bottles. Write a program that reads the number of milk bottles to ship and the capacity of one container. The program calculates and prints the number of containers fully packed with milk bottles and the number of remaining milk bottles. For example, if the farm needs to ship 118 milk bottles and the capacity of one container is 24 bottles, then 4 containers will be fully packed and 22 bottles of milk will be leftover.

Discussion

Input:

1\. the number of milk bottles to ship, stored in *countMilk*, integer

2\. the capacity of a container - the number of milk bottles that fits into one container, stored in *perBox*, integer

Output:

1\. the number of containers fully packed, stored in *countBoxes*, integer

2\. the number of remaining bottles, stored in *remain*, integer

Calculations: using integer division and modulo
countBoxes = countMilk / perBox (in C)
countBoxes = countMilk // perBox (in Python)
remain = counMilk % perBox (in C and Python)

Input Limitations: both inputs, countMilk and perBox, must be positive.

Output Limitations: none.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m6a9cbad.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m6a9cbad.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7ad4a5a1.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7ad4a5a1.jpg)

**Problem 3:** Write a program that reads an initial loan amount, loan interest rate (as a percent), and the loan term. The program calculates and prints the monthly loan payment. Assume that the interest is applied to the initial loan amount upfront. For example, if the initial loan is $500, the interest is 10.5% and the loan term is 5 years, then the monthly payment is $9.21.

Discussion

Input:

1\. initial loan amount, stored in *loan*, floating point

2\. interest percent, stored in *interest*, floating point

3\. loan term, the length of the loan in years, stored in *loan_term*, integer

Output: monthly loan payment, stored in monthly_payment, floating point.

Calculations:
total amount you own is: total_own = loan*(1+interest/100)
loan term in months is loan_term * 12,
monthly_payment = total_own/(loan_term*12)

Input Limitations: term must be of integer type, the loan amount and interest must be of float type, all input values must be positive.

Output Limitations: the output must be formatted with two decimal places since the program outputs the money value.

Note: in this program we will demonstrate a use of constant variables. Variable MONTHS, a constant variable, will hold the number of months in a year.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m783b51f2.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m783b51f2.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3e817508.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_3e817508.jpg)

**Problem 4:** Write a program that reads the number of hours the person works per day, the number of working days per month, the hourly wage, and the monthly income tax withholding rate (as a percent). The program calculates and prints the monthly salary. For example, if the person works 7 hours per day for 22 days in a specific month with an hourly wage of $8.25 and an income tax rate of 10.2%, then the paycheck for that month is $ 1140.91.

Discussion

Input:

1\. number of hours per day, stored in *hours*, integer

2\. number of working days in a month, stored in *days*, integer

3\. hourly wage, stored in *perHour*, floating point

4\. income tax rate, stored in *taxRate*, floating point

Output: The paycheck for the month, stored in paycheck, floating point

Calculations:
total number of working hours per month: totalHours=hours*days
gross pay per month: gross=totalHours*perHour
income tax withholding: incomeTax=gross*(taxRate/100)
monthly salary: paycheck = gross - incomeTax

Input Limitations: hours and days must be of integer type, hourly wage and taxRate amount must be of float type, all input values must be positive.

Output Limitations: the output must be formatted with two decimal places since the program outputs the money value.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m165a498.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m165a498.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m5fcb5ba1.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m5fcb5ba1.jpg)

**Problem 5:** The final grade in our course is calculated according to the following rule:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4a316641.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4a316641.jpg)

Write a program that reads the final exam grade and homework assignments grade. The program calculates the final grade in the course.

Discussion

Input:

1\. grade for final exam, stored in *final_exam*, integer

2\. grade for homework assignments, stored in *homework*, integer

Output: final grade, stored in final, integer

Calculations:
final = final_exam*(90/100) + homework *(10/100)

Input Limitations: final_exam and homework must be of integer type, all input values must be integers between 0 and 100.

Output Limitations – type casting: the output must be a rounded integer. Since int()function in Python and type casting in C truncates towards zero, the following formula must be used: (int)(final + 0.5)

For example, if the final grade is 93.5 the output will be 94 and if the final grade is 93.4 the output will be 93

Note: in this program we will use constant variables, FINAL and HOMEWORK, to hold the weight of final exam and homework.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m7b15b7f0.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m7b15b7f0.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m248f5684.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m248f5684.jpg)

**Problem 6:** Two cars travel toward each other. Write a program that asks the user to enter the speed of each car in miles per hour, the starting distance between the cars, in miles, and the travel time, in hours. The program calculates and prints the distance between the cars at the end of the trip. For example, if the speeds are 55 mph and 45 mph, the starting distance is 5.3 miles, and the travel time is 2.5 hours, then the distance between cars at the end of the trip is 244.7 miles.

Discussion

Input:

1\. speed of the first car, stored in *speed1*, floating point

2\. speed of the second car, stored in *speed2*, floating point

3\. starting distance, stored in *start_distance*, floating point

4\. travel time, stored in *time*, floating point

Output: the distance between cars at the end of the trip, stored in final_distance, floating point.

Calculations:

final_distance = start_distance – time*(speed1+speed2)

Input Limitations: all input values must be positive.

Output Limitations: in this problem, cars can meet and then continue travel in opposite directions, and in some cases the formula above will produce a negative result. But the final output, final_distance, must be positive. The fabs()function is used to find the absolute value of the final_distance.

The final formula in C:
final_distance = fabs(start_distance – time*(speed1+speed2))
The final formula in Python:
final_distance=math.fabs(start_distance – time*(speed1+speed2))

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_65932c0f.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_65932c0f.jpg)

IV. Chapter 1 Practice Exercises

1\. Write a program that reads 3 integers and calculates and prints their sum, product and average. The program prints the average result using only 2 digits after the decimal point.

2\. Write a program that reads 2 positive integers and finds the sum, product and average of their last digits. The program prints the average with 2 digits after the decimal point.

3\. Write a program that prompts the user to enter a three-digit positive integer number. The program separates the input number into its individual digits and prints the digits on separate lines in reverse order. For example, if the input number is 236 the program will print

6

3

2

4\. Write a program that prompts the user to enter a three-digit positive integer number. The program calculates and prints the product of its digits.

5\. Write a program that calculates the perimeter and area of a rectangle, and the area of a circle. The program asks the user to enter length and width of the rectangle, and radius of the circle.

Use the following formulas:

area = width * length

perimeter= 2*length + 2*width

areaCircle = 3.14 * radius * radius

6\. Write a program that converts a Celsius temperature to the correspondent Fahrenheit temperature using the following conversion formula: Fahrenheit = (9*Celsius/5)+32

7\. Write a program that converts a Fahrenheit temperature to Celsius temperature using the following conversion formula: Celsius = (5/9)*(Fahrenheit - 32)

8\. A customer comes to the store and buys 1 bottle of milk, 1 tray of eggs, and 1 loaf of bread. Write a program that asks the user to enter the price for each item and finds the total price and the average price per item.

9\. The final grade in our course is calculated according to the following rule:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m127028b0.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m127028b0.jpg)

Write a program that asks the user to enter the average grade for all quizzes, average grade for all exams, average grade for all homework, and the lab grade. The program calculates and prints the final grade in the course as a rounded integer.

10\. An outdoor storage shed, which has the form of a rectangular prism, was recently built in the rectangular backyard. Write a program that asks the user to enter the length and width of the base of the shed and the length and width of the backyard. The program calculates and prints the area outside of the shed.

11\. Write a program that asks the user to enter the length of the legs of a right triangle. The program calculates and prints the area of the triangle using the following formula: area = (leg1*leg2)/2

12\. Write a program that asks the user to enter the height of a person in inches. The program calculates and prints the height in feet and inches. Both outputs must be whole numbers. For example, if the height in inches is 67, the program outputs 5 feet and 7 inches, since 1 feet = 12 inches.

13\. Write a program that converts inches to centimeters using the following formula: centimeters = inches*2.54

14\. Write a program that asks the user to enter the height of the person in centimeters. The program calculates and prints the height of the person in meters and centimeters. Both outputs must be whole numbers. For example, if the height in centimeters is 152 centimeters, the program outputs 1 meter and 52 centimeters.

15\. Write a program that converts miles to kilometers using the following conversion formula: kilometers = miles * 1.609344

16\. Write a program that converts kilometers to miles using the following conversion formula: miles = kilometers * 0.62137

17\. Write a program that converts a decimal value representing hours into the whole number of hours and the whole number of minutes (the minutes should be rounded down). For example, if the input is 2.44, the program outputs 2 hours and 26 minutes, and if the input is 2.68, the program outputs 2 hours and 40 minutes. Explanation: (int)(2.44) = 2 is the whole number of hours. To convert the 0.44 hours into a whole number of minutes, perform (int)(0.44*60)= (int)(26.4) = 26. In the second example, (int)(2.68) = 2 is the a whole number of hours. To convert the 0.68 hours into a whole number of minutes, perform (int)(0.68*60)= (int)(40.8) = 40. Pay attention, in the second example the number of minutes is 40 due to truncation toward 0.

18\. Write a program that finds the daily travel time to work. The program asks the user to enter a distance (in miles) and average speed (in miles per hour). The program calculates and prints the commute time in hours and minutes using the following formula: time = distance / speed

Both outputs must be whole numbers. Pay attention, the formula above outputs the decimal value representing the number of hours (in C in case of integer distance and speed, use the type casting: time = (double)(distance)/speed)to obtain the decimal value representing the number of hours). To convert it to hours and minutes see the explanation in Problem 17.

For example, if the distance to work is 135.5 miles and the average speed is 55.5 mph, then the commute time is 2 hours and 26 minutes.

Explanation: 135.5/55.5 = 2.44 is a decimal number representing the commute hours; 2.44 hours is 2 hours and 26 minutes (see explanation in Problem 17).

19\. Two cars travel in opposite directions along the road. Write a program that asks the user to enter the speed of each car in miles per hour, the starting distance between the cars in miles, and the travel time in hours. The program calculates and prints the distance between the cars at the end of the trip. For example, if the speeds are 55 mph and 45 mph, the starting distance is 5.3 miles, and the travel time is 2.5 hours, then the distance between cars at the end of the trip is 255.3 miles.

20\. Two cars travel toward each other. Write a program that asks the user to enter the speed of each car in miles per hour and the starting distance between the cars in miles. The program calculates and prints the travel time, in hours and minutes, until the cars collide. For example, if the speeds are 55.3 mph and 45.2 mph, and the starting distance is 125.8 miles, then the travel time until cars collide is 1 hour and 15 minutes. Explanation: the travel time until cars collide is 125.8/(55.3+45.2)=1.25 hours, which is 1 hour and 15 minutes (see Problem 17).

21\. Two cars travel toward each other. A fly starting out at the front of one car, flies towards the other. Upon reaching the other car, the fly turns around and continues towards the first car. Write a program that asks the user to enter the speed of each car in miles per hour, the starting distance between the cars, in miles, and the speed of the fly in miles per hour. The program calculates and prints the distance, in miles, the fly travels until the cars collide. Assume that the speed of the fly greater than the speed of the car. For example, if the speeds are 55.3 mph (first car), 45.2 mph (second car) and 65.7 mph (fly), and the starting distance is 125.8 miles, then the fly travels 82.24 miles. ([http://mathworld.wolfram.com/TwoTrainsPuzzle.html](http://mathworld.wolfram.com/TwoTrainsPuzzle.html)).

V. Chapter 1 Appendix 1: Sample Quiz in Python

Quiz Questions

1\. How many variables are in the program written below? For each variable, write the NAME, TYPE and VALUE of that variable.

X = "C++"

C = "Java"

D = C+X

E = 15

K = 2

M = E/K

Y = E//K**2

Z = Y%10

2\. How many variables are in the program written below? For each variable, write the NAME, TYPE and VALUE of that variable.

A=5

B=6.7

C ="Python"

D = A/2

E = A//2

Z = A%2

3\. What is the output of the following code?

num = 234

a = num%10

num = num//10

b = num%10

num = num//10

c = num%10

print(a, b, c, num)

4\. What is the output of the following code?

price = 93

ball = 8

result = price % ball

rest = price // ball

all = 0

print (result, rest, ball)

5\. What is the output of the following code?

Python = 5

D = 3

C = 13

K = C//D

M = C%D**2 - 2*K

print("Python",Python,K,M)

6\. What is the output of the following code?

A = 72

K = (A//10 +A%10)//2

print(K)

7\. What is the output of the following code?

A = 5

B = 4

C = A-B*A

D = C**2

E = -15**2

print(C, D, E)

Quiz Answers

1\. There are 8 variables in the program

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m670bbf0c.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m670bbf0c.jpg)

2\. There are 6 variables in the program

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m293bbcd3.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m293bbcd3.jpg)

3\. 4, 3, 2, 2,

4\. 5 11 0

5\. Python 5 4 -4

Explanation:

K = 13//3 = 4
D**2 = 3**2 = 9
C%(D**2) = 13%9 = 4
2*K = 2*4 = 8
4-8= -4

6\. 4

Explanation:

A=72

K=(A//10 +A%10)//2=(72//10+72%10)//2=(7+2)//2=9//2=4

7\. -15 225 -225

Explanation

B*A = 5*4 = 20

C = A-B*A = 5-20 = -15

D = C**2 = (-15)**2 = 225

E = -15**2 = -(15**2) = -225

VI. Chapter 1 Appendix 2: Sample Quiz in C

Quiz Questions

1\. What is the output of the following code fragment?

int a = 2, b = 3, c = 4, d, e;

d = a*b%c + b/a;

e = (int)((float)(a)/c + (float)(c/b));

printf("%d\n%d\n", d, e);

2\. What is the output of the following code fragment?

int num = 234, a, b, c;

a = num%10;

num = num/10;

b = num%10;

num = num/10;

c = num%10;

printf("%d,%d,%d,%d\n",a, b, c, num);

3\. What is the output of the following code?

int price, ball, result, rest;

price = 93;

ball = 8;

result = price % ball;

rest = price / ball;

ball = 0;

printf("%d,%d,%d\n",result, rest, ball);

4\. What is the output of the following code?

int A, K;

A = 72;

K = (A/10 +A%10)/2;

print("%d\n",K);

5\. What is the output of the following code? Refer to ASCII table
[http://www.asciitable.com/](http://www.asciitable.com/)

char letter1 = 'A', letter2='a';

int sum = letter1+letter2;

printf("%d\n", sum);

6\. What is the output of the following code?

int A, K;

A = 7;

A++;

K = A*2 - 2;

print("%d\n%d\n",K,A);

7\. What is the output of the following code?

int A, K;

A = 7;

A++;

K = A*2 - 2;

A--;
print("%d\n%d\n",K,A);

Quiz Answers

1\. 3

1

Explanation

a*b=2*3=6

6%4=2

3/2=1

d=2+1=3

(float)(a)/c=0.5

float(4/3)=1.0

0.5+1.0 = 1.5

(int)(1.5)= 1

2\. 4,3,2,2

3\. 5 11 0

4\. 4

Explanation

A/10 = 72/10 = 7

A%10= 72%10 = 2

(7+2)/2=4

5\. 162

Explanation

The integer promotion is applied.

The ASCII value of 'A' is 65 and the ASCII value of 'a' is 97. Both chars, letter1 and letter2, are first converted to int, and then summation is performed: sum = letter1+letter2 = 65+97 = 162

6\. 14

8

Explanation:

A++ increments A by 1

A equals 8 now

K = A*2 – 2 = 8*2–2 = 16–2 = 14

7\. 14

7

Explanation:

A++ increments A by 1

A equals 8 now

K = A*2 – 2 =

8*2–2 = 16–2 = 14

A-- decrements A by 1

A equals 7 now

VII. Chapter 1 Appendix 3: Modulo Operator in Python – Negative Numbers Case

1\. The floor (integer) division and modulo operators are connected by the following identity: x = (x//y)*y + (x%y). This identity applies to all numbers, positive and negative.

2\. The modulo operator always yields a result with the same sign as its second operand (or zero).

3\. For x < 0 and y > 0 the following formula could be applied:

x%y = y – abs(x)%y, where abs(x)is absolute value of x.

See also: [http://python-history.blogspot.com/2010/08/why-pythons-integer-division-floors.html](http://python-history.blogspot.com/2010/08/why-pythons-integer-division-floors.html)

4\. The arguments may be floating point numbers, but this material is outside of the scope of this book

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_61a7ed8c.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_61a7ed8c.jpg)

VIII. Chapter 1 Appendix 4: Modulo Operator in C – Negative Numbers Case

1\. The division and modulo operators are connected by the following identity:
x = (x/y)*y + (x%y). This identity applies to all numbers, positive and negative. Remember, division of integers yields a truncated integer: for positive results, it is always the floor of the division; for negative results, it is ceiling of the division.

2\. For x < 0 and y > 0: x%y = –(abs(x)%y), where abs(x)is absolute value of x.

3\. For x > 0 and y < 0: x%y = x%abs(y), where abs(y) is absolute value of y.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7ed10e1b.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7ed10e1b.jpg)

IX. Chapter 1 Appendix 5: Increment and Decrement Operator in C – Special Cases

The following examples should be avoided due to undefined behavior. Most compilers will produce results listed below but we encourage you to check the behavior of these statements on your own system.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5fb4457a.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5fb4457a.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5144760d.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5144760d.jpg)

Chapter 2: Decision Structures

I. Theory Overview

1\. Relational Operators in Python and C

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5d887b7c.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5d887b7c.jpg)

In Python, relational operators are also called comparisons, [https://docs.python.org/3/library/stdtypes.html#comparisons](https://docs.python.org/3/library/stdtypes.html#comparisons).

2\. Boolean Expression

A Boolean Expression is an expression that evaluates to the Boolean value, True or False.

In Python, True and False are built-in constants, [https://docs.python.org/3.1/library/constants.html](https://docs.python.org/3.1/library/constants.html).

In Python, any object has a Boolean value. For the data types we have introduced so far, the following objects have the value False: zero of any numeric type, for example, 0, 0.0; Boolean built-in constant False; and an empty string "" or ''. ([https://docs.python.org/3/library/stdtypes.html#truth-value-testing](https://docs.python.org/3/library/stdtypes.html#truth-value-testing))

In C, each number has a Boolean value: 0 has a False Boolean value and any non-zero number has a True Boolean value. The char type is considered an 8-bit integer, which is the corresponding ASCII value of the character. If the ASCII value is 0, then the Boolean value is False, otherwise, the Boolean value is True.

3\. Logical (Boolean) Operators and Boolean Logic

Mathematical Notation

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m50a3a76c.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m50a3a76c.jpg)

Programming Notation – Logical (Boolean) Operators Ordered by Ascending Priority

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m3af5f3d0.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m3af5f3d0.jpg)

4\. IF Statement

In Python Programming language:

if (expression):

if_statements

In C Programming Language:

if(expression){

if_statements;

}

How it works:

1\. The expression is evaluated.

2\. If the expression is TRUE the if_statements are executed; otherwise, when expression is FALSE, the if_statements are skipped and control is transferred to the next statement after the if block.

Examples in Python

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m5c241143.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m5c241143.jpg)

Examples in C

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_16f6ace1.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_16f6ace1.jpg)

5\. IF ELSE Statement

In Python Programming Language:

if(expression):

if_statements

else:

else_statements

In C Programming Language:

if(expression){

if_statements;

}

else{

else_statements;

}

How it works:

1\. The expression is evaluated.

2\. If the expression is TRUE, if_statements are executed and control is transferred to the next statement after if else block.

3\. Otherwise, if the expression is FALSE, else_statements are executed and control is transferred to the next statement after the if else block.

Examples in Python

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m3fd8c4d3.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m3fd8c4d3.jpg)

Examples in C

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m391bda92.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m391bda92.jpg)

6\. IF ELIF ELSE Statement in Python and IF ELSE-IF ELSE Statement in C:

IF ELIF ELSE Statement in Python

if(expression_1):

statements_1

elif(expression_2):

statements_2

elif(expression_3):

statements_3

…

#could be several elif statements

else:

else_statements

IF ELSE-IF ELSE Statement in C:

if(expression_1){

statements_1;

}

else if(expression_2){

statements_2;

}

else if(expression_3){

statements_3;

}

…

/* could be several else if statements */

…

else{

else_statements;

}

How it works:

1\. The expressions are evaluated one by one from top to bottom starting from expression_1.

2\. When the program reaches an expression evaluating to TRUE the corresponding statements are executed, the other statements are skipped, and control is transferred to the next statement after if else-if else (if elif else in Python) block.

3\. If none of the expressions evaluates to TRUE, then the else_statements are executed and control is transferred to the next statement after if else-if else (if elif else in Python) block.

Example:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m44e3f4d2.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m44e3f4d2.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_277df098.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_277df098.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6add64a4.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6add64a4.png)

**Note,** in the C programming language, the curly braces are optional when there is a single statement inside the if, else, or else if body. The curly braces are required in case of multiple statements. See examples below:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m1e8161f.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m1e8161f.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_56081d00.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_56081d00.jpg)

7\. Nested Decision Structures

Both programming languages, C and Python, support nested decision structure - decision statements placed inside decision statement.

Examples in Python

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_4e7b7251.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_4e7b7251.jpg)

Examples in C

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m32d68dc4.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m32d68dc4.jpg)

8\. SWITCH Statement in C (there is no SWITCH statement in Python)

switch(expression){

case case_constant:

case_statements;

break; /* optional */

case case_constant:

case_statements;

break; /* optional */

…

/* could be any number of case statements */

default: /* optional */

default_statements;

break; /* optional */

}

Note:

a. The expression in the switch statement must return an integral value (int or char variable type).

b. Case constants (case_constant) must be of the same data type as the switch expression, and they must be constant.

How it works:

1\. The switch expression is evaluated.

2\. The value is compared to case*_*constants top to bottom.

3\. When a case_constant that matches the switch expression is found, the corresponding case_statements are executed. Since the break statement is optional, in general, the program can fall through the cases and execute statements from multiple cases, until a break statement or the end of the switch statement is reached.

4\. If none of the case_constants match the switch expression value, the default_ statements from the default case are executed, if default case exists; otherwise, the control passes to the next statement after the switch block.

Example:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7c736f1c.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7c736f1c.jpg)

II. Sample Solutions in Python and C

**Problem 1:** Write a program that reads one integer and checks whether the input is even or odd. The program prints an appropriate message.

Discussion

Input: one integer stored in num.

Output: a message indicating whether the input is even or odd.

Calculations: an even number is a number that is evenly divisible by 2, meaning that num%2 is 0 if num is even. Use an if-else statement to determine whether num % 2 is 0 or not.

Input Limitations: input number is integer.

Output Limitations: None.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m42a67b00.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m42a67b00.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_18dbede0.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_18dbede0.jpg)

**Problem 2:** Write a program that reads three integers and finds the maximal value among the inputs.

Discussion

Input: three integers stored in num1, num2, and num3 Output: the maximal value among input values, stored in max_value.

Calculations Version 1:

1\. Find maximum between num1 and num2 using an if-else statement and store result in max_value.

2\. Compare max_value to num3 using an if statement and update the max_value if needed.

Calculations Version 2:

1\. Assign num1 to max_value. This is an initialization of the max_value.

2\. Compare num2 to current max_value and update max_value if needed.

3\. Compare num3 to current max_value and update max_value if needed.

Input Limitations: input numbers are integers.

Output Limitations: if any two numbers or all three numbers are the same, this algorithm will still work properly and print the correct maximal value, but the program will not print any message describing these special cases.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m6ca7ecef.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m6ca7ecef.png)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_364d6256.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_364d6256.png)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_361e9acd.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_361e9acd.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_2817a917.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_2817a917.jpg)

**Problem 3:** Saving accounts have different interest rates based on the deposit amount. In one bank, for example, if the deposit is 1000 dollars or less, the interest rate is 1% per year, otherwise, the interest rate is 2% per year. Write a program that inputs a deposit amount. The program first checks, that the input is valid. For valid input, the program calculates and prints the amount of money that will be in your saving account after one year. Apply the interest rate rule that is described above. For invalid input, program prints an error message.

Discussion

Input: deposit amount, stored in deposit, floating point value.

Output: the amount of money in account after one year, stored in total, floating point value.

Calculations:

1\. Determine the interest rate based on the deposit amount using an if-else statement

2\. Use the following formula to calculate the total amount that will be in the account after one year:
total = deposit*(1 + rate/100)

Input Limitations: deposit amount must be positive and this limitation could be checked in the program using an if-else statement.

Output Limitations: the output must be formatted to two decimal places since the program outputs the money value.

Constant Variables: in this problem there are three constant values that are defined in the problem description: 1000, 1 and 2\. To define constant values in C, we will continue to use the const keyword.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7cd3d188.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7cd3d188.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m5908cd13.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m5908cd13.jpg)

**Problem 4:** Write a program that reads a student’s grade for one course and finds whether the student passed or failed the course using the following rule: grades 60 and above are passing grades and grades below 60 are failing grades. Assume that the grade is an integer.

Discussion

Input: student grade, stored in grade, integer type.

Output: a message indicating whether student passed or failed the course.

Calculations: use if-else statement to determine whether
grade >= 60 or grade < 60 and print an appropriate message.

Input Limitations: grade is an integer; grade must be non-negative and this limitation should be checked in the program using an if-else statement.

Output Limitations: None.

Constant Variables: in this problem there is one constant value that is defined in the problem description: 60\. To define constant values in C, we will continue to use the const keyword.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_25ab89cf.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_25ab89cf.png)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5397d522.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5397d522.jpg)

**Problem 5:** A treasure bot with 1 million dollars inside has a lock combination using a 3-digit positive integer. To open the box, the following rules need to be satisfied: (1) first digit equals last digit; (2) middle digit is odd.

Write a program that reads one 3-digit integer and prints YES if the number opens the box and NO otherwise.

Discussion

Input: one 3-digit integer stored in num.

Output: message: YES or NO.

Calculations:

1\. Separate input number into digits, using divide by 10/mod 10\. Store digits in: first_digit, mid_digit, last_digit.

2\. Use an if-else statement to check the following conditions: first_digit == last_digit and (mid_digit % 2) != 0 (an odd number is a number that is not divisible by 2).

Input Limitations: num must be a positive 3-digit number and this limitation should be checked in the program using an if-else statement (num > 99 and num < 1000).

Output Limitations: None.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5fc0041c.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5fc0041c.png)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m16cb2ee3.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m16cb2ee3.jpg)

**Problem 6:** Write a program that reads one integer, a grade for some course, and prints the letter value of that grade using the following table:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7f3dffba.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7f3dffba.jpg)

Discussion

Input: one integer stored in grade.

Output: letter value of the input grade.

Calculations: use an if-else-if-else (if-elif-else in Python) statement to determine the numeric range of the input and the corresponding letter grade.

Input Limitations: grade must be a non-negative number less than or equal to 100\. This limitation should be checked in the program using an if-else statement (num >= 0 and num <= 100).

Output Limitations: None.

To demonstrate one of the common logic mistakes we provide one possible wrong solution along with correct one and explain the logic error.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_674459dd.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_674459dd.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5de94a68.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5de94a68.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_28cab15c.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_28cab15c.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4b31b4a8.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4b31b4a8.jpg)

**Problem 7:** Some credit cards charge a foreign transaction fee when items are purchased overseas. Fees tend to range from 1% to 3% of the transaction amount with a minimal flat fee. For example, if the foreign transaction fee rate is 2.5%, the flat fee is $5, and the purchase amount is $100.67, the total transaction amount is $105.67, since 2.5% of $100.67 is $2.52, which is less than the minimum fee of $5\. Write a program that reads a purchase amount, foreign transaction fee and minimal flat fee, and calculates the total transaction amount.

Discussion

Input:

1\. Purchase amount, stored in purchase, floating point number.

2\. Foreign transaction fee rate, stored in foreign_rate, floating point value.

3\. Flat fee, stored in flat_fee, floating point value.

Output: total transaction amount, stored in total, floating point value, and in addition, a message indicating whether the flat fee or foreign transaction fee percent was charged.

Calculations:

1\. Calculate foreign transaction fee percent.

2\. Using an if/else statement, compare percentage to flat fee to determine which one must be charged.

Input Limitations: all inputs must be positive. This limitation should be checked in the program using an if-else statement.

Output Limitations: the output must be formatted to two decimal places since the program outputs the money value.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m37113836.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m37113836.png)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7e4542ad.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7e4542ad.jpg)

**Problem 8:** In the Gregorian calendar,a year is a leap year when the number representing it is divisible by 4, but not by 100, unless it is divisible by 400\. Thus years such as 1996, 1992, 1988 and so on are leap years because they are divisible by 4 but not by 100\. For century years, the 400 rule is important. Thus, century years 1900, 1800 and 1700, while all still divisible by 4, are also divisible by 100\. As they are not further divisible by 400, they are not leap years. On the other hand, the year 2000 is a leap year since it is divisible by 4 and 100 but also by 400\. Also, you can assume that there were no leap years before 1582\. Write a program that asks the user for a year and computes whether or not that year is a leap year.

Example:
Input: 1980 Output: Leap Year
Input: 1900 Output: Not a Leap Year
Input: 1200 Output: Not a Leap Year
Input: 2000 Output: Leap Year
Input: 3000 Output: Not a Leap Year

Discussion

Input: one integer stored in year.
Output: a message indicating whether input is a leap year or not.

Calculations: use an if-else-if-else statement to check the following conditions:

1\. Years before 1582 are not leap years.

2\. For years 1582 and above, years divisible by 4 and not divisible by 100 are leap years, and years divisible by 400 are leap years, otherwise, the year is not a leap year.

Input Limitations: year must be non-negative and this limitation should be checked in the program using an if-else statement.

Output Limitations: None.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m78af6bdc.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m78af6bdc.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_587eb579.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_587eb579.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5c4c746e.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5c4c746e.jpg)

SWITCH statement examples

**Problem 9:** Write a menu for an online/mobile banking system. The menu includes the following options: deposit, withdraw, transfer, and exit from the menu. The program reads one character and prints the description of the operation corresponding to the input character. We will assume that deposit is represented by the letter D, withdraw by the letter W, transfer by the letter T, end exit from the menu by the letter E. Only D, W, T, and E are allowed. For any other character the program prints an error message.

Discussion

Input: one char representing menu choice, choice.

Output: a message describing the banking operation corresponding to the input character, or an error message.

Calculations: use an if-elif-else statement in Python, and switch statement in C.

Input Limitations: None.

Output Limitations: None.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6dfaf0a5.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6dfaf0a5.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_2f722004.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_2f722004.jpg)

**Problem 10:** Write a program that reads one integer**,** month, and prints the number of days in that month.

Discussion

Input: one integer, stored in month, representing the numeric number of the month: January is 1, February is 2, etc., and December is 12.

Output: the number of days in the specified month. For February, the program prints 28 or 29; there is no need to check if the year is a Leap year or not.

Calculations: use a switch statement in C and an if-elif-else statement in Python.

Input Limitations: the input must be a positive integer between 1 and 12\. This limitation should be checked in the program using an if-else statement in Python or a switch statement in C.

Output Limitations: the output for February will not specify the exact number of days since this program will not check the Leap year condition. To output the exact number of days in February, this program could be combined with Problem 8 but this would require additional input data – the numeric value of the year.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m2640a202.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m2640a202.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4d0f619c.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4d0f619c.jpg)

**Problem 11:** Write a program that simulates a simple calculator that performs addition, subtraction, multiplication, division, and remainder of the division of two integers. The program reads two integers and the operator (character), and performs the corresponding operation. Only addition, subtraction, multiplication, division and modulo (+, - , *, /, %) operators are allowed. For any other operator the program prints an error message. For division and remainder, the program checks validity of the input (division by zero is not allowed).

Discussion

Input: two integers, stored in num1 and num2, and the char representing the arithmetic operator, stored in operator.

Output: the result of the arithmetic operation or error message.

Calculations: use an if-elif-else statement in Python, and switch statement in C.

Input Limitations: for division and remainder (/ and %), the program checks that num2 is not equal to zero to avoid the division by zero error.

Output Limitations: None.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m7ccd5804.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m7ccd5804.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_mddfd73f.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_mddfd73f.jpg)

**Problem 12:** A grocery store sells perishable and nonperishable food. Each item in the store has a bar code, a 9-digit positive integer. The bar code of perishable items ends with 3, 4, or 7. Write a program that reads one integer, the barcode of a single item and checks whether the item is perishable or not. The program prints an appropriate message.

Discussion

Input: one 9-digit integer, stored in barcode.

Output: message: PERISHABLE or NONPERISHABLE.

Calculations:

1\. Use the modulo operator to find the last digit.

2\. Check whether the last digit equals 3, 4, or 7.

In Python, we will use an if-else statement. In C, it is possible to use an if-else or switch statement. In this example, we will show how to use the switch statement in C.

Input Limitations: the number representing the barcode must be between 100000000 and 999999999 inclusive. This limitation should be checked in the program.

Output Limitations: None.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5d520a6.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5d520a6.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m254b6e47.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m254b6e47.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m37b0b061.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m37b0b061.jpg)

**Problem 13:** Write a program that reads three integers, representing a date: month, day, and year**.** The program prints the next date. For example, if the input is 3 30 2015 (March 30, 2015) the output is 3 31 2015 (March 31, 2015), and if the input is 12 31 2016 (December 31, 2016) the output is 1 1 2017 (January 1, 2017). Pay attention, the program prints month first, followed by day and year.

Discussion

Input: three integers, stored in month, day, and year, representing the date.

Output: three integers representing the next date

Calculations: use a switch statement in C and an if-elif-else statement in Python. First, identify the number of the days in the input month (similar to the previous program), then determine if the input day is the last day of the month, and determine if the input month is the last month of the year.

Input Limitations: the number representing month must be between 1 and 12, the number representing day must be positive and correspond to the number representing month, and the number representing year must be positive. In this program we use a flag variable, input_valid, to check validity of the input. Flag variable is a Boolean variable that assigned True (1 in C) at the beginning of the program and then change to False (0 in C) as soon as invalid input encountered.

Output Limitations: None.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_15a2e112.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_15a2e112.jpg)![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4bf9379b.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m4bf9379b.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7aee409f.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7aee409f.jpg)

**Problem 14:** Many companies are using automated phone systems known as IVR (Interactive Voice Response). In many cases, these systems repeat customer choices and ask for additional confirmation before transferring the call. Write a program to simulate the simple system for a cable company that provides TV, Internet and Phone services. The menu options are listed in the table below. For all main menu options, except Exit, include the repeating feature. Assume that all customers have all three services and the monthly cost is $199.99\. Also, assume that for confirmation, 'Y' means "confirmed", and any other character, means "not confirmed".

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_31abe6a8.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_31abe6a8.jpg)

Discussion

Input:

1\. integer representing the main menu choice, stored in main_choice.

2\. integer indicating secondary menu choice, stored in second_choice.

3\. floating point number indicating payment amount, stored in payment (in case and main_choice is 2).

4\. character confirming the main menu or secondary menu choice, stored in confirm.

Output: the message describing the menu choice or account balance, or an error message; for main menu, the message indicating confirmation of the choice.

Calculations: Use an if-elif-else statement in Python, and switch statement in C.

Input Limitations: the payment amount must be positive.

Output Limitations: None.

Constant Variables: in this problem there is one constant value that is defined in the problem description: 199.99\. To define constant values in C, we will continue to use the const keyword.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m2d65eb60.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m2d65eb60.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_456913cd.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_456913cd.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m16f5cd64.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m16f5cd64.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m6e42bb1f.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m6e42bb1f.jpg)

III. Practice Exercises

For practice purposes not all programs explicitly state what input/output should be. Follow problem solving guidelines detailed in Chapter 1 to identify input and output as a first step in your solution.

1\. Write a program that reads one integer. The program checks whether the input is divisible by 3.

2\. Write a program that reads two integers and finds the maximum and the minimum among inputs.

3\. Write a program that reads two integers and checks whether the first input is evenly divisibly by the second input.

4\. Write a program that reads one integer and finds its absolute value without using any built-in functions.

5\. Write a program that reads one 3-digit positive integer. The program checks whether at least one of the digits equals 3.

6\. Write a program for a cash register that calculates the amount of change the customer should receive. The program reads the item price, number of items purchased and the amount of money paid. The program outputs the change amount the customer should receive from the cashier.

7\. Road speed limits are used in most countries to set the maximum (or minimum in some cases) speed at which road vehicles may legally travel on specific roads. Write a program that reads a maximum limit, minimum limit and car speed. The program checks whether the car is driving within the legal limits.

8\. Write a program that reads one integer and prints the corresponding day of the week. Assume that 1 corresponds to Sunday, 2 to Monday, etc., and 7 to Saturday.

9\. Write a program that reads the coordinates of three points on a number line. The program finds and prints which point lies between the other two.

10\. Write a program that solves the linear equation a*x + b = 0. Program reads two integers, a and b, coefficients of the linear equation and outputs the solution or a message indicating that there are no solutions or there is infinite number of solutions.

11\. Write a program that reads three positive numbers that are the lengths of a possible triangle. The programs checks whether these three numbers can form a valid triangle.

12\. Write a program that reads two integers which are the coordinates of a point in the Cartesian plain. The program finds the location of the given point in the Cartesian plain: axis or quadrant.

13\. Write a program that reads one 3-digit positive integer. The program checks whether the input number is numerical palindrome. A **numeral palindrome** is a number that remains the same when its digits are reversed. For example, the numbers 575 and 212 are numerical palindromes.

14\. Write a menu program that supports the actions listed in the table below. The program first reads a character, corresponding to the action, and then asks the user for additional input based on the action. Only actions described below are allowed. For any other character the program prints an error message.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m42b2c3d7.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m42b2c3d7.jpg)

15\. Write a program that reads a character, the first letter of a country’s name, and an integer, a number of minutes, and calculates the cost of the long distance phone call to that country based on the following rates per minute:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m726ab01b.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m726ab01b.jpg)

16\. Write a program that finds the discount percent based on the number of pounds of candy for Halloween that you purchased, and calculates the total cost of that candy, taking into account that in some cases the purchase is taxable, and in some cases it is not. The tax is applied on the discounted price. The program reads the following input: number of pounds, price per pound, tax, and an additional integer, tax indicator, that must be 1 or 0, where 1 indicates that the purchase is TAXABLE, and 0 that is not. Use the table below to find the total cost of your purchase. The table shows the discount percent based on the number of pounds you purchased. The program prints the discount percent and the final cost of your purchase.

Discount Percent

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m78e06be0.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m78e06be0.jpg)

Example 1: Input: number of pounds = 7, price per pound = 3.99, TAX = 6, tax indicator = 1
Output: $26.65

Explanation of the output: you bought 7 pounds, got a 10% discount, and the purchase is TAXABLE at 6%. Final price is $26.65

Example 2: Input: number of pounds = 15, price per pound = 2.99, TAX = 7, tax indicator = 0
Output: $35.88

Explanation of the output: you bought 15 pounds, got a 20% discount, and the purchase is NOT TAXABLE. Final price is $35.88

17\. There is a treasure chest with 1 million dollars. The chest has a 5-digit combination lock that opens under the following conditions: the first digit must be equal to the fifth digit, the second digit must be odd, and the product of the third and fourth digits must be divisible by 7\. Write a program that reads one 5-digit positive integer and checks whether the input number opens the chest or not. The output should be YES, if the chest opens, and NO otherwise.

18\. In most cases, buying in bulk is cheaper than buying smaller packaged food, but not always. Write a program that reads the price of an item per pound in bulk, the size of the smaller package (float, could be a half pound package, for example), and the price of the package. The program finds and prints which option is cheaper per pound, or notifies user that both options offer the same price per pound.

For example, organic quinoa in bulk cost $5.99 per pound, and a package of 2.5 pounds costs $12.90\. In this case, it is cheaper to buy the package, since the price per pound in the packaged version is $5.16, which is less than $5.99 bulk price.

For example: almonds in bulk s cost $7.99 per pound, and a package of 3/4 of a pound costs $6.99\. In this case it is cheaper to buy in bulk, since a pound of packaged almonds will cost $9.32.

For example: a pound of ham in bulk costs $10, and a 2 pound package costs $20\. In this case both options have equal value.

Pay attention, when you test your program, to test the third option, input whole numbers to avoid issues with floating point numbers rounding.

19\. Write a program that calculates the insurance points for speeding on the highway and the monthly insurance payments for the next insurance term after receiving the points. The program reads the upper speed limit on the highway, the current speed of the car, and the current insurance cost per year. You can assume that all inputs are integers. The program must print the following information: number of points, or message explaining the status (no points/ license suspended), the percent of insurance increase, the new yearly insurance premium, and the new monthly payment. Use the following table:

Speeding Points Table and Yearly Insurance Rate Increase

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_75b4a7aa.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_75b4a7aa.jpg)

20\. Write a program that calculates the insurance points that two different people will receive for speeding on the highway. The upper speed limit on the highway is 65 mph. You can assume that speed is an integer number. Use the following table:

Speeding Points Table

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_58bff16e.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_58bff16e.png)

21\. Write a program that finds the final score in a song competition. There are 4 judges in the competition.

Scoring rules:

- Each judge submits a score for the song. Assume that the score is an integer, which could be positive as well as negative, and could be zero.

- To calculate the final score: the highest score is dropped, the minimal score is squared, and then the average is calculated.

22\. Write a program that calculates the total cost of amusement park tickets for a family of 4 people. The input: full price of a ticket (integer), age of each family member (integer), tax (integer). Output: Total price after all discounts and taxes are taken into account. The tax is applied to the discounted total.

Ticket Price Rules:

a. children under age of 6: - free

b. age 6 - 10: 50% discount

c. age 11 - 13: 25% discount

d. age 14 - 18: 10% discount

e. adults: full price

23\. A company wants to transmit data over the telephone line, but they are concerned that their lines are tapped. All of their data is transmitted as four-digit integers. They decided to encrypt a four-digit number as follows: (1) they will replace each digit by ((digit + 7) mod 10); (2) they will then swap the first digit with the third digit and the second digit with the fourth. The resulting four-digit number is the encrypted number. To decrypt the number, the reverse procedure should be applied (you need to figure out the algorithm). Write a program that can do either encryption or decryption. The program must take two inputs. The first input must be either 1 or 2, with 1 signaling encryption and 2 signaling decryption. The second input is a positive integer less than 10,000 which will be either encrypted or decrypted depending on the first input. For example, if the input is 1 1234, the output will be 8901; if the input is 2 9605, the output will be 2938; if the input is 3367, the output will be 0034 (pay attention, in this case the output includes leading zeros hence it is advisable to print the output digit by digit instead of converting it to the integer).

24\. Write a program that prompts the user to enter three integers. The program will sort the input numbers and print the input numbers in increasing order. You can assume that the input numbers are different.

For example if the input was 4, -9 and 8, the program should output: -9, 4, 8
For example , if the input was 1, 0, -90, the program should output: -90, 0, 1

Try to find the most efficient solution.

25\. A Holiday Sale in one of the department stores has the following rules. All items receive a 30% discount except home and electronics. Home items receive 15% and electronics 10%. We will assume that ALL items are NOT taxable. In addition, if the discounted total is 40 dollars or more, an additional 10 dollars off is applied. We will assume that the user is purchasing 3 items. For each item, the program reads the price and the category. We will use the following category indicators: Home = 1, Electronics = 2, Everything else = 3\. Write a program that finds the final purchase amount.

Example 1: input (price and category for each item): 32.50, 1, 12.99, 2, 3.49, 3
Output: 31.76 (explanation: 32.5 received 15% discount, 12.99 received 10% discount, and 3.49 received 30% discount. The total after discount is taken is 41.76 dollars. Since this is over 40 dollars, an additional 10 dollars off is applied and the final total is 31.76)

Example 2: input: 15.99, 2, 10.99, 1, 1.99, 3
Output: 25.13

IV. Chapter 2 Appendix 1: Sample Quiz in Python

Quiz Questions

1\. For the following code fragment:

a = int(input("enter number "))

b = int(input("enter number "))

if(a + b > 10):

print("hello")

else:

print("python")

give an example of the input to receive the following output: hello

2\. For the following code fragment:

a = int(input("enter number "))

b = int(input("enter number "))

k = a%10 + b%10

if(k%2):

print("hello")

else:

print("python")

give an example of the input, if it exists, to receive the following output: python

3\. For the following code fragment:

a = int(input("enter number "))

b = int(input("enter number "))

if(a % 3 >= 2):

print("hello")

else:

print("python")

if((a + b) != (5//2)):

print("hello")

else:

print("python")

if(a == (2%3)):

print("hello")

else:

print("python")

give an example of the input, if it exists, to receive the following output:

hello

python

hello

4\. For the code fragment in the previous example, give an example of the input, if exists, to receive the following output:

python

python

hello

5\. What is the output of the following code fragment?

a = 17

b = 5

if((a % b > 5) or (a % 2)):

print("hello")

else:

print("python")

6\. What is the output of the following code fragment?

a = 17

b = 5

c = 6

d = not(c % 2 and a > b)

if(d):

print("hello")

else:

print("python")

7\. What is the output of the following code fragment?

int a = 17, b = 5, c = 6;

d = c % 4 and a < b or not(a)

if(d):

print("hello")

elif(c % 2):

print("python")

else:

print("program")

Answers to Quiz Questions:

1\. Input example: a = 5, b = 6

Explanation:

a + b = 11

11 > 10 TRUE

*if_statement* executes

hello will be printed

In general, a and b can be any two integers with their sum greater than 10.

2\. Input example: a = 123,b = 2677

Explanation:

k = 123 % 10 + 2677 % 10 = 3 + 7 = 10

10 % 2 = 0, 0 means FALSE

*else_statement* executes python will be printed.

In general, a and b can be any two integers with last digits that are either both even or odd.

3\. Input example: a = 2, b = 0

Explanation:

2 % 3 = 2

2 >= 2 TRUE

*if_statement* executes hello is printed.

2 + 0 = 2

5 // 2 = 2

2!=2 FALSE

else_statement executes python is printed .

a = 2

2 % 3 = 2

2 == 2 TRUE

*if_statement* executes hello is printed.

This is the only possible input.

4\. The input does not exist.
Explanation: the value of variable a is determined in the last if-else statement. In this case, in order to print hello, the value of a must be 2, since 2 % 3 equals 2. In order to print python in the first if-else statement, the expression, which is a % 3 >= 2, must be FALSE, which is impossible, since a = 2.

5\. hello

Explanation:

17 % 5 = 2

2 > 5 FALSE

17 % 2 = 1

1 has a value TRUE

FALSE or TRUE = TRUE

*if_statement* executes hello will be printed.

6\. hello

Explanation:

6 % 2 = 0, FALSE

17 > 5, TRUE

d = FALSE and TRUE = FALSE

*if_statement* executes hello will be printed.

7\. program

Explanation:

c % 4 = 6 % 4 = 2, TRUE

a < b = 17 < 5, FALSE

not(17)= not(TRUE) = FALSE

d = (TRUE and FALSE) or FALSE = FALSE

c % 2 = 6 % 2 = 0, FALSE

*else_statement* executes program will be printed.

V. Chapter 2 Appendix 2: Sample Quiz in C

Quiz Questions

1\. For the following code fragment:

int a, b;

scanf("%d%d", &a, &b);

if(a + b > 10)

printf("hello\n");

else

printf("C programming\n");

give an example of the input to receive the following output: hello

2\. For the following code fragment:

int a, b, k;

scanf("%d%d", &a, &b);

k = a%10 + b%10

if(k%2)

printf("hello\n");

else

printf("C programming\n");

give an example of the input, if it exists, to receive the following output:

C programming

3\. For the following code fragment:

int a, b;

scanf("%d%d", &a, &b);

if(a % 3 >= 2)

printf("hello\n");

else

printf("C programming\n");

if((a + b) != (5/2))

printf("hello\n");

else

printf("C programming\n");

if(a == (2%3))

printf("hello\n");

else

print("C programming\n");

give an example of the input, if it exists, to receive the following output:

hello

C programming

hello

4\. For the code fragment in the previous example, give an example of the input, if exists, to receive the following output:

C programming

C programming

hello

5\. What is the output of the following code fragment?

int a = 17, b = 5;

if((a % b > 5) || (a % 2))

printf("hello\n");

else

printf("C programming\n");

6\. What is the output of the following code fragment?

int a = 17, b = 5, c = 6;

if(!(c % 2 && a > b))

printf("hello\n");

else

printf("C programming \n");

7\. What is the output of the following code fragment?

int a = 17, b = 5, c = 6;

d = ((c%4) and (a<b)) or (not(a))

if(c % 4 && a < b || !(a))

printf("hello\n");

else if(c % 2)

printf("C\n");

else:

printf("program\n");

8\. What is the output of the following code fragment?

char choice = 'D';

switch(choice){

case 'A':

printf("1\n");

break;

case 'B':

printf("2\n");

break;

case 'C':

printf("3\n");

break;

case 'D':

printf("4\n");

default:

printf("bye\n");

break;

}

9\. What is the output of the following code fragment?

int a = 13, b = a % 3;

switch(b){

case 0:

printf("%d\n", b);

case 1:

printf("%d\n", b*b);

case 2:

printf("%d\n", b*b*b);

default:

printf("bye\n");

break;

}

Answers to Quiz Questions

1\. Input example: a = 5, b = 6

Explanation:

a + b = 11

11 > 10 TRUE

*if_statement* executes

hello will be printed

In general, a and b can be any two integers with their sum greater than 10.

2\. Input example: a = 123,b = 2677

Explanation:

k = 123 % 10 + 2677 % 10 = 3 + 7 = 10

10 % 2 = 0, 0 means FALSE

*else_statement* executes C programming will be printed.

In general, a and b can be any two integers with last digits that are either both even or odd.

3\. Input example: a = 2, b = 0

Explanation:

2 % 3 = 2

2 >= 2 TRUE

*if_statement* executes hello is printed.

2 + 0 = 2

5 // 2 = 2

2!=2 FALSE

else_statement executes C programming is printed .

a = 2

2 % 3 = 2

2 == 2 TRUE

*if_statement* executes hello is printed.

This is the only possible input.

4\. The input does not exist.

Explanation: the value of variable a is determined in the last if-else statement. In this case, in order to print hello, the value of a must be 2, since 2 % 3 equals 2. In order to print C programming in the first if-else statement, the expression, which is a % 3 >= 2, must be FALSE, which is impossible, since a = 2.

5\. hello

Explanation:

17 % 5 = 2

2 > 5 FALSE

17 % 2 = 1

1 has a value TRUE

FALSE or TRUE = TRUE

*if_statement* executes hello will be printed.

6\. hello

Explanation:

6 % 2 = 0, FALSE

17 > 5, TRUE

d = FALSE and TRUE = FALSE

*if_statement* executes hello will be printed.

7\. program

Explanation:

c % 4 = 6 % 4 = 2, TRUE

a < b = 17 < 5, FALSE

not(17)= not(TRUE) = FALSE

d = (TRUE and FALSE) or FALSE = FALSE

c % 2 = 6 % 2 = 0, FALSE

*else_statement* executes program will be printed.

8.

4

bye

Explanation:
The value of variable choice is D

The case corresponding 'D' is executed and 4 is printed. Since there is no break statement, the fall through cases occurs and the next case, default, is executed and bye is printed.

9.

1

1

bye

Explanation:
The value of variable b is 1. The case corresponding 1 is executed and 1 (1*1 = 1) is printed. Since there is no break statement, the fall through cases occurs and the next case, 2, is executed, and 1 (1*1*1 = 1) is printed, since, again, there is no break statement, the fall through cases occurs and the next case default, is executed and bye is printed.

Chapter 3: Loops

I. Theory Overview

Loops are control flow programming statements that allow a pogram to repeat the execution of a block of code multiple times. C supports three types of loops: while, for, and do-while. Python supports two types of loops: while and for. Both programming languages support nested loop: a loop inside another loop.

1\. Loops in Python

i. WHILE **loop**

A while loop in Python repeatedly executes a block of statements as long as a specified condition is true.

Syntax:

while(expression):

loop body statement(s)

Each repetitive execution of the loop body statement(s) is called an iteration.

How it works:

loop body statements are executed repeatedly while expression is True.

Note:

1\. Loop body can consist of a single statement or multiple statements.

2\. Loop expression can be any expression that has a Boolean value. *Remember:* in Python, all numbers have Boolean value: 0 has a False Boolean value and any non-zero number has a True Boolean value.

3\. Loop expression is checked at the start of each iteration.

4\. If expression is never False, the loop is an infinite loop.

5\. If expression has a False Boolean value at the beginning of the loop execution, the loop terminates immediately and loop body statements are not executed at all and control passes to the next statement in the program.

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m7e704a37.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m7e704a37.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m5706e1ab.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m5706e1ab.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_335c864b.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_335c864b.jpg)

Tracing Programs Example

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7bfbcdb1.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7bfbcdb1.jpg)

ii. FOR loop

A for loop in Python iterates over the items of any sequence in the order that they appear in the sequence, executing a block of statements until the iteration sequence is exhausted. The range()function can be used to iterate over a sequence of numbers.

The range(n) function generates the sequence 0, 1, … ,n-1. The given endpoint, n, is never part of the generated sequence. It is possible to let the range start at another number, or to specify a different increment (‘step’). The general form is range(start, end, step).

[https://docs.python.org/3/tutorial/controlflow.html#for-statements](https://docs.python.org/3/tutorial/controlflow.html#for-statements)

[https://docs.python.org/3/tutorial/controlflow.html#the-range-function](https://docs.python.org/3/tutorial/controlflow.html#the-range-function)

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_448cbff2.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_448cbff2.jpg)

In this chapter we will only consider examples of the for loop that iterates over sequences of numbers using the range() function.

FOR Loop Syntax:

for i in range(start, end, step):

loop body statement(s)

Examples

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7dc5d0ec.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7dc5d0ec.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_1bb89595.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_1bb89595.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m1d76de30.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m1d76de30.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_153cccf6.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_153cccf6.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_37133a3e.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_37133a3e.jpg)

iii. Nested Loops in Python

Python supports the nested loop structure – a loop inside another loop. The depth of the nested loop depends on the problem. Any type of loop could be placed inside the other loop.

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6a543ff3.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6a543ff3.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_28f43479.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_28f43479.jpg)

2\. Loops in C

i. WHILE loop

A while loop in C repeatedly executes a block of statements as long as a specified condition is true.

Syntax:

while(expression){

loop body statement(s);

}

Each repetitive execution of the loop body statement(s) is called an iteration.

How it works:

loop body statements are executed repeatedly while expression is True.

Note:

1\. while loop in C works exactly the same as in Python; the only difference is slightly different syntax.

2\. Loop body can consist of a single statement or multiple statements. In case of a single statement, the curly braces are optional.

3\. Loop expression could be any expression that has Boolean value. *Remember:* in C, all numbers have Boolean value: 0 has a False Boolean value and any non-zero number has a True Boolean value.

4 If expression is never False, the loop is an infinite loop.

5\. If expression has a False Boolean value at the beginning of the loop execution, the loop terminates immediately and loop body statements are not executed at all and control passes to the next statement in the program.

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_60c380d1.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_60c380d1.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_34bd8d9d.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_34bd8d9d.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_mf17fbe3.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_mf17fbe3.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m54df1074.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m54df1074.jpg)

Tracing Programs Example

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_2eb3b27.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_2eb3b27.jpg)

ii. DO WHILE loop

A do while loop in C repeatedly executes a block of statements as long as a specified condition is true. A do while loop is very similar to while loop with one difference: the do while condition is evaluated after executing the block of statements, resulting in at least one execution of the loop body statements.

Syntax:

do{

loop body statement(s);

} while(expression);

How it works:

loop body statements are executed repeatedly while expression is TRUE. The expression is evaluated after loop body statements are executed, thus do while loop executes loop body statements at least once.

Examples below compare do while and while loops.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m50afdfec.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m50afdfec.jpg)

**Example** below shows the code fragment that asks the user to enter valid grade, which must be an integer between 0 and 100, inclusive. Loops are used to agrantee input is valid. In this example, it is preferable to use do while loop to design shorter code.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6fba68ac.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6fba68ac.jpg)

iii. FOR loop

A for loop in C repeatedly executes a block of statements as long as a specified condition is true. A for loop has different syntax, but conceptually, it is similar to the while loop: the condition in a for loop is evaluated before executing the block of statements, and in the case of a False condition at the beginning of the loop execution, the for loop terminates immediately and loop body statements are not executed at all and control passes to the next statement in the program.

Syntax:

for(initialization; expression; loop value update){

loop body statement(s);

}

How it works:

1\. The initialization statement is executed. This statement is executed only one time: at the beginning of the loop execution, before the first iteration of the loop.

2\. The expression is evaluated. If it is True, the loop body statement(s) are executed, and the flow of control jumps to the loop value update statement.

3\. loop body statements and loop value update statement are executed repeatedly while expression is TRUE.

4\. When expression become False the loop terminates and the flow of control jumps to the next statement after the loop. The expression is only checked at the beginning of each iteration.

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_650ed719.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_650ed719.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m57c48b43.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m57c48b43.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_934d889.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_934d889.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_2fda506f.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_2fda506f.jpg)

Note:

The initialization, expression, and loop value update statements are optional and could be omitted, but the separating semi-colon (;) is required even if the statement is omitted. C supports multiple statements in the initialization and update part of the loop. In this case the statements must be separated by comas. The for loop can also have empty loop body statements (see examples below).

Example:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m3890fb6d.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m3890fb6d.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m33d2a470.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m33d2a470.jpg)

Note:

a. Loop body can consist of a single statement or multiple statements. In case of a single statement, the curly braces are optional.

b. Loop expression can be any expression that has a Boolean value. *Remember:* in C, all numbers have Boolean value: 0 has a False Boolean value and any non-zero number has a True Boolean value. The char type is considered as an 8-bit integer: the corresponding ASCII value of the character. If the ASCII value is 0, then the Boolean value is False, otherwise, the Boolean value is True.

c. If expression is never False the loop is infinite loop.

d. If expression has a False Boolean value at the beginning of the loop execution, the loop terminates immediately and loop body statements are not executed at all and control passes to the next statement in the program.

e. Loops while and for are always interchangeable:

for(initialization; expression; loop value update){

loop body statement(s);

}

Equivalent to:

initialization;

while(expression){

loop body statement(s);
loop value update;

}

**Example:** write a code fragment that evaluates 2^(10) using while loop and for loop.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m38a3da6f.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m38a3da6f.jpg)

Sentinel and Counter Controlled Repetitions

All loops may be classified into two general categories: counter controlled and sentinel controlled repetitions. The logical structure of the problem determines which type of loop will be implemented. Loops while, do while, and for could be counter controlled repetitions.

In the **counter controlled** loop, the number of iterations is known in advance, before execution of the loop. In this case, the loop is controlled by the counter variable, the expression checks whether counter variable has reached a certain predetermined value, and the update statement increments or decrements the counter variable.

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7b0e5347.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7b0e5347.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_21f2bcff.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_21f2bcff.jpg)

In the **sentinel controlled** loop, the number of iterations is unknown in advance. In this case, the loop is controlled by the sentinel value, a special value that is used to terminate the loop execution.

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m10462e63.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m10462e63.jpg)

It is advisable to use for loop in the case of counter controlled repetition and while loop in the case of sentinel controlled repetition.

iv. Nested Loops in C

C supports the nested loop structure – a loop inside another loop. The depth of the nested loop depends on the problem. Any type of loop can be placed inside another loop.

Examples:

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_30fe60be.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_30fe60be.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7beca6df.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7beca6df.jpg)

v. Break Statement in C

There are cases that require the termination of loop execution immediately without checking the expression and regardless of the expression value. To implement this logic behavior, C supports the break statement, which can be used with all three types of loops in C: while, do while, and for. It is also possible to use a break statement in nested loops.

Syntax:

break;

How it works:

1\. The break statement terminates the loop immediately when it is encountered, and the program control resumes at the next statement following the loop.

2\. In case of nested loops, the break statement terminates execution of the nearest enclosing loop and passes control to the outer loop. In the case of a nested loop, the break statement does not terminate the entire nested loop structure, but instead, terminates only the loop with the break statement in it.

Note:

It is advisable not use the break statement, but instead, to achieve the same logic behavior using flag variables.

Examples:

1\. Write a code fragment that finds the average grade for a graduating senior. Assuming the student took 10 courses, the code fragment reads the grade for each course, and finds and prints the final average grade. In order for the student to graduate, all grades must be passing grades (equal or above 60). If at least one grade is below 60, the student cannot graduate and the average final grade will not be calculated. In this case, the corresponding message is printed.

Below, the while loop and for loop implementations using the break statement. The loop is terminated in case of the failing grade and the sum is reset to 0. The control passes to the next statement after the loop that checks whether sum equals zero or not, and prints an appropriate result.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_14dbd88b.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_14dbd88b.jpg)

**To compare,** see below while and for loop implementations using the flag variable.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m1f79bdfb.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m1f79bdfb.jpg)

II. *Sample Solutions in Python and C*

**Problem 1:** Write a program that prints all integers divisible by 7 between 1 and 100.

Discussion

Input: none

Output: the sequence of integers divisible by 7 between 1 and 100

Calculations: Using a loop programming structure, for each number between 1 and 100, check whether it is divisible by 7 the using mod operator.

This is a counter controlled repetition since the number of iterations (100) is known in advance, since we need to check all numbers between 1 and 100\. The preferable loop structure is thefor loop.

Input Limitations: none

Output Limitations: none

Constant Variables: in this problem there are two constant values that are defined in the problem description: 1, the lower limit, and 100, the upper limit. To define constant values in C, we will continue to use the const keyword.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7b4a624f.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7b4a624f.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m67485d42.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m67485d42.jpg)

**Problem 2:** Write a program that counts the number of integers divisible by 7 between two input integers.

Discussion

Input: two integers, stored in limit1 and limit2

Output: the number of integers divisible by 7 between limit1 and limit2, stored in counter.

Calculations: Using a loop programming structure, for each number between limit1 and limit2, check whether it is divisible by 7 using the mod operator, and update the counter. Pay attention: in case limit1 > limit2, swap the values.

This is a counter controlled repetition. Since we need to check all numbers between limit1 and limit2, the number of iterations is known in advance and is equals to

abs(limit1 - limit2) + 1 (abs means absolute value).

The preferable loop structure is the for loop.

Input Limitations: none

Output Limitations: in case there are no numbers divisible by 7 in the specified range, program prints an appropriate message.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5d9a51e1.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5d9a51e1.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m59fd8884.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m59fd8884.jpg)

**Problem 3:** Write a program that reads a sequence of integers; -1 terminates the input sequence. The program counts and prints the number of inputs in the sequence. The terminator, -1, is not counted. For example, if the input is -3 4 -10 6 7 -1, the output is 5, and if the input is -1, the output is 0.

Discussion

Input: sequence of integers, current input number is stored in num

Output: the number of inputs not including terminator -1.

Calculations: Using a loop programming structure, repeat input integers untill -1 is entered.

This is a sentinel controlled repetition. The number of iterations in unknown and depends on the input.

The preferable loop structure is the while loop.

Input Limitations: pay attention: the first input must be done before the loop.

Output Limitations: in case of 0, consider printing the message: empty sequence

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m533da3ab.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m533da3ab.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_49901566.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_49901566.jpg)

**Problem 4:** Write a program that reads one positive integer and finds the sum of its digits.

Discussion

Input: positive integer, stored in num

Output: the sum of the digits of the input number, stored in sum, integer type

Calculations:

Using a loop programming structure repeat extracting the last digit (mod 10) and truncating the input number (integer division by 10) untill it reaches zero.

This is a sentinel controlled repetition since the number of iterations is unknown in advance and depends on the input. The number of iterations is equal to the number of digits in the input number. The preferable loop structure is the while loop.

Input Limitations: none, in case of negative input, the program will work with the absolute value of the input.

Output Limitations: none

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6be4c2f7.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6be4c2f7.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_423b041d.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_423b041d.jpg)

**Problem 5:** Write a program that reads a positive integer number and prints its reverse. For example, if the input is 2345, the output is 5432\. Assume the input is valid.

Discussion

Input: positive integer, stored in num

Output: the reverse number.
Solution 1: prints the reverse number digit by digit
Solution 2: calculates the reverse number first, and then prints it.

Calculations: In both solutions, using a loop programming structure, repeat extracting the last digit (mod 10) and truncating the input number (integer division by 10) untill it reaches zero. In the first solution, the next digit is printed. In the second solution, the sum building the reverse number is accumulated using corresponding the power of 10\. In both solutions, the processing starts from the last digit.

This is a sentinel controlled repetition since the number of iterations is unknown in advance and depends on the input. The number of iterations is equal to the number of digits in the input number. The preferable loop structure is the while loop.

Input Limitations: we will assume the input is valid: positive integer.

Output Limitations: in Python, to print digits on the same line in Solution 1, use separator end in the print statement.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_ccee8e7.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_ccee8e7.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_f9f01e9.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_f9f01e9.jpg)

**Problem 6:** Write a program that reads a sequence of **size** integers and finds the minimal and maximal values among the inputs.

Discussion

Input: size of the input sequence, stored in variable size, followed by size integers, with the current integer is stored in variable num

Output: maximal and minimal values, stored in max and min.

Calculations:

Initialization: assign first input number to max and min.

Using a loop programming structure, repeat reading next input number, compare to current max and min values, and replace if needed.

This is a counter controlled repetition since the number of iterations is known in advance and equals size. The number of iterations is equal to the number of inputs. The preferable loop structure is the for loop.

Input Limitations: size must be positive and this limitation can be checked in the program using an if-else statement

Output Limitations: none

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_4f6c9fc6.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_4f6c9fc6.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5bb5df31.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_5bb5df31.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_1736473b.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_1736473b.jpg)

**Problem 7:** Write a program that finds the average final grade in a course. The program reads the number of students in the class, and the final grade for each student, and outputs the average grade. Assume the input is valid.

Discussion

Input: number of students, stored in num_stud (integer type), and a grade for each student, stored in variable grade

Output: average final grade in the course, stored in average (double type)

Calculations:

Using a loop programming structure, repeat reading a grade for each student and accumulate the sum of all grades. After the loop is terminated, find the average grade, sum/num_stud

This is a counter controlled repetition since the number of iterations is known in advance and equals num_stud. The number of iterations equals the number of students in the class. The preferable loop structure is the for loop.

Input Limitations: in this example we will assume that the input is valid, num_stud > 0 and grade >= 0 and grade <= 100

Output Limitations: the average of the grades must be float or double type

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m685884c7.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m685884c7.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m730e0ef1.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m730e0ef1.jpg)

**Problem 8:** Write a program that reads a sequence of integers. The sequence is terminated when 100 is entered. The program finds the minimal value and its position from the beginning of the sequence and from the end of the sequence. Assume the input is not empty. For example, if the input is 8 4 -1 3 9 -2 10 6 100, the output is -2 (minimal value), 6 (position of the minimal value from the beginning), and 3(position of the minimal value from the end of the sequence). Pay attention: 100 is not part of the sequence sintce it is a terminating value.

Discussion

Input: sequence of integers. The current integer is stored in variable num.

Output: minimal value, stored in min, its position from the start of the sequence, stored in from_start, and its position from the end of the sequence, stored in from_end.

Calculations:
Initialization: assign first input number to min, and its position from start, from_start, to 1\. In addition, the number of inputs will be stored in variable total with initial value 1 since the input sequence is not empty.

Using a loop programming structure, repeat reading an input number, compare to current min value, replace if needed, and update the from_start value, increment the value of total which is used to update the from_start value. After loop is complete, evaluate from_end = total – from_start. Pay attention: 100 is not considered part of the sequence and should not count toward the total number of sequence elements.

This is a sentinel controlled repetition since the number of iterations is unknown in advance and depends on user input. The number of iterations equals the number of inputs. The preferable loop structure is the while loop.

Input Limitations: the input sequence is not empty

Output Limitations: none

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6a40432a.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6a40432a.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m8ae4c9c.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m8ae4c9c.jpg)

**Problem** 9: Write a program that first reads two integers n and lim, and then reads n additional integers. The program finds the minimal value greater than lim. Assume, n is positive.

Discussion

Input: the size of the input, stored in n, the upper bound, stored in lim, each input integer stored in num

Output: the minimal value greater than lim, stored in minBigger

Calculations: the program iterates through the input sequence untill the first number greater than lim is found. The program then continues to iterate through the input sequence and checks if there is a number that is less than the first found. The first loop is sentinel controlled repletion since the number of iterations is unknown and depends on the position of the first input number bigger than lim. The second loop is a counter controlled repetition, since the number of iterations is known. In Python, the while loop is a preferable loop structure for both loops. In C, we will show a solution using the for loop for both loops.

Input Limitations: in this example we will assume that the input is valid, n > 0

Output Limitations: in case no numb er larger than limit is found, the program prints an appropriate message.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_2ec4f70c.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_2ec4f70c.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_239ba619.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_239ba619.jpg)

**Problem** 10: Write a program that reads one positive integer n, and are finds the maximal integer number that is less than square root of n.

Discussion

Input: positive integer, stored in n.

Output: the maximal integer number that is less than square root of n.

Calculations:
Initialization: assign 1 to variable max.

Using a loop programming structure, repeat incrementing the value of max by 1 until max*max < n. The number of iterations equals the maximal integer number that is less than square root of n and is approximately equals sqrt(n). This is a sentinel controlled repetition. In Python, the preferable loop structure is the while loop; in C, while loop and for loop can be used.

For example, if n = 49, loop iterates 6 times, and the maximal integer number that is less than square root of 49 is 6; if n = 48, loop iterates 6 times, and the maximal integer number that is less than square root of 48 is 6; if n = 50, loop iterates 7 times, and the maximal integer number that is less than square root of 50 is 7;

Input Limitations: in this example we will assume that the input is valid, n > 0

Output Limitations: none

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6f65a446.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_6f65a446.jpg)

**Problem** 11: Write a program that first reads an integer a, and then reads a sequence of non-zero integers, first zero value terminates the input. The program outputs True if there are two input numbers such that their sum is less than a, and False otherwise.

Discussion

Input: an integer stored in a, followed by a sequence of non-zero integers, each input integer stored in num

Output: True if there are two input numbers such that their sum is less than a, and False otherwise.

Calculations: the program iterates through the input sequence untill two input numbers such that their sum is less than a are found. The loop is sentinel controlled repletion since the number of iterations is unknown. The while loop is a preferable loop structure.

Input Limitations: in this example we will assume that the input is valid, a > 0

Output Limitations: in case no numb er larger than limit is found, the program prints an appropriate message.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m569e7638.png](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m569e7638.png)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_78bcdf22.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_78bcdf22.jpg)

**Problem 12:** Write a program that finds the average final grade for each student in a department for a specific semester. The program reads the number of students in the department, the number of courses each student took in that semester (this number can be different for different students), and the final grade for each course. The program finds and prints the average final grade for each student. Assume the input is valid.

Discussion

Input: number of students in the department, stored in total_size, number of courses for each student, stored in num_courses, grade for each course, stored in grade. All inputs are integers.

Output: the average final grade for each student, stored in final_grade

Calculations: This problem uses nested loops. The outer loop iterates from 1 to total_size, and the inner loop iterates from 1 to num_courses. Both loops are counter controlled repetitions. To find the average grade, the sum of all grades for each student must be calculated. The sum value must be reset to zero prior processing grades for the next student.

Input Limitations: total_size must be positive; num_courses must be positive; grade must be between 0 and 100\. We assume the input is valid.

Output Limitations: none

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7a94d6c0.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_7a94d6c0.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m27863937.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m27863937.jpg)

**Problem 13:** Write a program that reads a sequence of n integers (n is the length of the sequence and it is an input as well). The program finds the number of monotonically (strictly) increasing maximal sub-sequences (a[i] < a[i+1]) of at least length 2 within the input sequence. A 'maximal' monotonically (strictly) increasing sub-sequence, is a monotonically (strictly) increasing sub-sequence where if you add the next element, it will not be a monotonically (strictly) increasing sub-sequence anymore.

For example, if the input sequence is: 3 1 5 7 2 -3 2 5 7 1 5 5 1 4 The program outputs 4, since there are four increasing sub-sequences:

1 5 7
-3 2 5 7
1 5
1 4

Note, in the example above, 1 5 7 is a maximal monotonically (strictly) increasing sub-sequence, but 1 5 is not. And also, -3 2 5 7 is a maximal monotonically (strictly) increasing sub-sequence but -3 2 and -3 2 5 are not.

For example if the input sequence is: 8 5 4 1, the program outputs 0, since there are no increasing sub-sequences within the input sequence.

Discussion

Input: length of the sequence, stored in n (integer type), followed by n integers. Since the program must compare previous and current sequence values, two variables are used to store these values: num_cur and num_prev

Output: the number of monotonically (strictly) increasing sub-sequences within the input sequence, stored in count_incr

Calculations: This problem could be solved using nested loops or a single loop with two flag variables.

The nested loop solution: the outer loop iterates through the input sequence and the inner loop iterates through the current increasing sub-sequence. The outer loop is a counter controlled repetition and the inner loop is a sentinel control repetition.

The single loop solution: iterates through the input sequence using a flag that indicates the beginning of the current increasing sub-sequence.

Input Limitations: the length of the sequence, n, must be positive and this limitation can be checked in the program using an if-else statement

Output Limitations: none

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m10acd2f3.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_m10acd2f3.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_52e2fc34.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_52e2fc34.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_f5a2749.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_f5a2749.jpg)

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_689b90b0.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_689b90b0.jpg)

III. Practice Exercises

1\. Write a program that reads one positive integer n and prints all integers between 1 and n inclusive.

2\. Write a program that reads one positive integer n and prints the squares of all integers between 1 and n inclusive.

3\. Write a program that reads one positive integer n and prints all even integers between 1 and n inclusive (write two different solutions, one using if statement, and one without using if statement).

4\. Write a program that reads one positive integer n and prints all odd integers between 1 and n inclusive (write two different solutions, one using if statement, and one without using if statement.

5\. Write a program that first reads one positive integer n, followed by n positive integers; each represents the side of a square. The program finds the square with the minimal perimeter. The program prints the minimal perimeter.

6\. Write a program that first reads one positive integer n, followed by 3*n positive integers; each triple represents the sides of a triangle. The program finds the triangle with the maximal perimeter. The program prints the maximal perimeter.

7\. Write a program that first reads two positive integers n and lim, and then reads n additional integers. The program finds the number of inputs less than lim.

8\. Write a program that first reads three positive integers, n, left and right, and then reads n additional integers. The program finds the number of inputs between left and right (inclusive). You may assume left < right.

9\. Write a program that first reads three positive integers, n, left and right, and then reads n additional integers. The program finds the number of inputs between left and right (inclusive) that are divisible by 3 and not divisible by 5\. You may assume left < right.

10\. Write a program that first reads two positive integers, n and lim, and then reads n additional integers. The program finds the maximal value less than lim.

11\. Write a program that reads one positive integer and finds its maximal digit.

12\. Write a program that reads one positive integer and finds the difference between its maximal and minimal digits.

13\. Write a program that reads a sequence of non-zero integers; the first zero value terminates the input. The program outputs True, if the current input number is equal to the sum of all previous inputs, and False otherwise.

Example 1:
Input: 2 2 4 8 16 0 Output: True

Example 2:
Input: 3 3 6 12 0 Output: True

Example 3:
Input: 3 3 7 13 20 0
Output: False

14\. Write a program that first reads one integer. If the integer is EVEN, the program reads 7 real numbers. Each number indicates the Fahrenheit temperature for one day. The program finds and prints the average Celsius temperature for these 7 days. Use the following formula to convert Fahrenheit to Celsius:

Celsius = (5/9)*(Fahrenheit-32)

If the integer is ODD, the program reads 7 real numbers. Each number indicates the Celsius temperature for one day. The program finds and prints the average Fahrenheit temperature for these 7 days. Use the following formula to convert Celsius to Fahrenheit:

Fahrenheit = (9/5)* Celsius + 32

15\. Write a program that first reads one positive integer that indicates the size of the sequence. The program then reads the sequence of integers and finds the average of the input numbers that are divisible by 4.

16\. Write a program that reads a sequence of non-zero integers; the first zero value terminates the input. Each number indicates the numeric value of the day of the week. The program prints the name of the day. For example, if the input is 5 the program outputs Thursday, if the input is 1, the program outputs Sunday, if the input is negative or greater than 7, the program outputs the error message.

17\. Write a program that reads a sequence of non-zero integers; the first zero value terminates the input. Each number indicates the numeric value of the month. The program prints the number of days in that month. In case the month is February (2), the program asks the user to enter an additional integer indicating the year. For example, if the input is 5 (May) the program outputs 30, if the input is 12 (December), the program outputs 31, if the input is 2 (February), the program checks the year and finds whether the number of days is 28 or 29 (Leap Year). If the input is negative or greater than 12, the program prints the message "Invalid month".

18\. Write a program that reads one positive integer and finds and prints the average of its EVEN digits. If there are no even digits, the program prints an appropriate message.

19\. Write a program that reads a sequence of non-zero integers. First zero value terminates the input. The program finds the number of negative inputs, and their sum and average. In case there are no negative inputs, the program prints an appropriate message.

Example 1:
Input: 2 -5 6 7 -8 -9 0
Output: there are 3 negative numbers, their sum is -22 and their average is -7.333333

Example 2:
Input: 2 6 7 0
Output: there are no negative inputs

20\. Write a program that reads 10 positive three-digit numbers and prints the last digit of each number. You may assume that input consists of 10 positive integers between 100 and 999.

21\. Write a program that reads one positive integer. The program finds and prints the sum of all divisors of the input number. For example, if the input is 12, the output will be 28\. Explanation: the divisors of 12 are: 1, 2, 3, 4, 6, and 12, and their sum is 28.

22\. Write a program that reads a sequence of positive integers greater than 10. The first negative integer terminates the input. The program finds the average of the last digits of the even numbers and first digits of the odd numbers. You can assume that the input is valid and not empty - there is at least one positive integer in the input. For example, if the user enters the positive numbers 23, 455, 668, and 24, the program will compute the average of the first digits of the odd numbers (2 and 4) and the last digits of the even numbers (8 and 4): (2 + 4 + 8 + 4) / 4 = 4.5

23\. Write a program that reads one positive integer representing the number of students in the course. The program then reads the final grade for each student and finds the number of students who failed the course (got grade below 60).

24\. Write a program that reads three values: deposit, interest and number of years. The program finds and prints the amount of money in the account at the end of the designated period.

25\. Write a program that reads an initial bank deposit and yearly interest. The program finds and prints the number of years it will take to receive $1,000,000. The interest is applied annually.

26\. Write a program that first reads the number of parking violations per year. The program reads the category for each violation (assume that the input is an integer 1, 2, or 3. Assume that the input is VALID). The program finds the total amount paid for parking violations and the average violation fine. Use the table below.

![tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_4d3182e0.jpg](tmp_034b4c16a5496d1faa828a97718c1803_1OXqjI_html_4d3182e0.jpg)

Example with explanation:
Input: 4 1 3 2 1 Output: 195 (35+75+50+35=195)

27\. Write a program that reads a sequence of non-zero integers. First zero value terminates the input. The program finds the number, the sum, and the average of the positive even numbers.

Example 1:
Input: 2 -6 6 7 8 -9 0

Output: there are 3 positive numbers, their sum is 16 and their average is 5.333333

Example 2:
Input: -4 -6 7 -8 0 Output: there are no positive even numbers in the input sequence

28\. Write a program that reads a sequence of non-zero integers. First zero value terminates the input. The program finds the number, the sum, and the average of the negative odd numbers.

Example 1:
Input: 2 -6 6 -7 8 -9 0
Output: there are 2 negative odd numbers, their sum is -16 and their average is -8.0

Example 2:
Input: 3 5 7 8 9 0 Output: there are no negative odd numbers in the input sequence

29\. Write a program that reads a sequence of non-zero integers. First zero value terminates the input. The program outputs True if the input sequence is a monotonic increasing sequence, and False, otherwise. A sequence (a[n]) is **monotonic increasing** if a[n+1] ≥ a[n] for all n*.*

Example 1:
Input: -2 4 4 10 0 Output: True

Example 2:
Input: -2 -3 -5 0
Output: False

Example 3:
Input: 1 3 5 2 4 6 -1 2 0 Output: False

Example 4:
Input: 4 4 4 0 Output: True

30\. Write a program that reads a sequence of non-zero integers. First zero value terminates the input. The program outputs True, if all inputs are positive integers, and False, otherwise.

31\. Write a program that first reads two integers, a and b, and then a sequence of non-zero integers. First zero value terminates the input. The program outputs True if all input numbers lay between a and b, and False, otherwise. You may assume a < b.

32\. Write a program that first reads two integers, a and b, and then a sequence of non-zero integers. First zero value terminates the input. The program prints all input numbers that lay between a and b. You may assume a < b.

33\. Write a program that first reads two integers, a and b, and then a sequence of non-zero integers. First zero value terminates the input. The program outputs True, if at least half of the input numbers lay between a and b, and False, otherwise.

34\. Write a program that reads the number of desserts the person is purchasing for Thanksgiving Dinner. The program reads the sugar content (in grams) for each dessert, and finds the total sugar content for all desserts and the average sugar content per dessert. According to the American Heart Association (AHA), the maximum amount of added sugars per day should be about 30 grams. The program checks if the average sugar content satisfies the recommendations of the American Heart Association (AHA) and prints an appropriate message.

35\. Write a program that reads the number of desserts the person is purchasing for Thanksgiving Dinner. The program reads the sugar content (in grams) and fat content (in grams) for each dessert. The program uses the following formula to find and print the rating for each dessert: rating = -0.5*sugar -1.5*fat + 50, and finds and prints the highest rating.

36\. In this program you need to implement the score system in the Figure Skating competition. There are 12 judges that are present. First step: all 12 judges submit their scores. Second step: the highest and lowest score are thrown out from the 12 submitted scores. Third step: the remaining 10 scores are averaged. Write a program that reads 12 scores submitted by 12 judges for the specific event and calculates the final score according to the rules written above. Each input score is an integer number between 0 and 100. You can assume that the input is valid.

37\. Write a program that reads two positive integers and prints all prime numbers between two inputs.

38Write a program that reads one positive integers and finds the sum of all prime divisors of the input number. For example, if the input is 12, the output will be 5. Explanation: only 2 and 3 are prime divisors of 12 (all divisors of 12 are: 1, 2, 3, 4, 6, and 12).

39\. Write a program that reads a sequence of non-zero integers, first zero value terminates the input. The program finds and prints the length of the longest sub-sequence of the positive input numbers.

Example 1:
Input: -3 7 -12 4 2 -3 7 12 11 7 -8 0 Output: 4

Example 2:
Input: -3 -4 8 -5 6 -7 0 Output: 1

40\. Write a program that reads two positive integers and prints all perfect numbers between the two inputs. A number is called perfect if the sum of the proper divisors is equal to the number itself. A positive divisor of some number K, which is different from K, is called a proper divisor of K. Example: 6 is a perfect number. Proper divisors of 6 are 1, 2, and 3 and their sum is 6. Other perfect numbers, for example, are 28, 496, 8128.

41\. A positive divisor of some number K, which is different from K, is called a proper divisor of K. For example, 1, 2, and 3 are proper divisors of 6. In number theory, an abundant number is a number that is less than the sum of its proper divisors. For example, 12 is an abundant number since it is less than 1+2+3+4+6 = 16. The number 15 is NOT an abundant number since the sum of the proper divisors is 1+3+5 = 9. The number 6 is also NOT an abundant number since 1+2+3 = 6. Write a program that reads one positive integer N and prints all ODD ABUNDANT numbers between 1 and N. If the number N is ODD and ABUNDANT, the program will print N as well.

Example 1:
Input 1000 Output: 945

Example 2:
Input: 2000
Output: 945 1575

42\. A happy number is defined by the following process. Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers, while those that do not end in 1 are unhappy numbers (or sad numbers). If n is not happy, then its sequence does not go to 1. What happens instead is that it ends up in a cycle such as: 4, 16, 37, 58, 89, 145, 42, 20, 4, 16, 37, 58, 89, 145, 42, 20, 4, 16, 37, 58, 89....

Write a program that reads one integer and outputs the following: if the number is happy, it outputs YES and the number of steps it took to get from the input to 1 (including the step that resulted in 1), otherwise, the program outputs NO and the number of steps it took to get to the beginning of the cycle (including the step that resulted in 4).

For example if n = 44, we get
Step 1: 4² + 4²= 32
Step 2: 3² + 2²= 13
Step 3: 1² + 3²= 10
Step 4: 1² + 0² = 1 - terminates the process and the output is: YES, 4

For example, if n = 43, we get
Step 1: 4² + 3² = 25
Step 2: 2² + 5² = 29
Step 3: 2² + 9² = 85
Step 4: 8² + 5² = 89
Step 5: 8² + 9² = 145
Step 6: 1² +4² +5² = 42
Step 7: 4² + 2² = 20
Step 8: 2² +0² = 4

Output NO, 8