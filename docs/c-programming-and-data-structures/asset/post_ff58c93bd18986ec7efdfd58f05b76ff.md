
Correctness depends on the solution procedure, the clarity depends on the way the output is presented. Following are some of the steps we can take to improve the clarity and hence the readability and understandability of outputs.

- 1. Provide enough blank space between two numbers.
- 2. Introduce appropriate headings and variable names in the output.
- 3. Print special messages whenever a peculiar condition occurs in the output.
- 4. Introduce blank lines between the important sections of the output.

The system usually provides two blank spaces between the numbers. However, this can be increased by selecting a suitable field width for the numbers or by introducing a 'tab' character between the specifications. For example, the statement

```
printf("a = %d\t b = %d", a, b);
```

will provide four blank spaces between the two fields. We can also print them on two separate lines by using the statement

```
printf("a = %d\n b = %d", a, b);
```

### Table 1.16 Commonly used printf Format Codes

| Code | Meaning |
|------|---------|
| %c | print a single character |
| %d | print a decimal integer |
| %e | print a floating point value in exponent form |
| %f | print a floating value without exponent |
| %g | print a floating point value either e-type or f-type depending on |
| %i | print a signed decimal integer |
| %o | print an octal integer, without leading zero |
| %s | print a string |
| %u | print an unsigned decimal integer |
| %x | print a hexadecimal integer, without leading 0x |

### Table 1.17 Commonly used Output Format Flags

| Flag | Meaning |
|------|---------|
| - | Output is left-justified within the field. Remaining field will be blank. |
| + | + or – will precede the signed numeric item. |
| 0 | Causes leading zeros to appear. |
| # (with o or x) | Causes octal and hex items to be preceded by 0 and 0x, respectively. |
| # (with e, f or g) | Causes a decimal point to be present in all floating point numbers, even if it is whole number. Also prevents the truncation of trailing zeros in g-type conversion. |

Messages and headings can be printed by using the character strings directly in the printf statement. Examples:

```
printf("\n OUTPUT RESULTS \n");
printf("Code\t Name\t Age\n");
printf("Error in input data\n");
printf("Enter your name\n");
```

## 1.44 INTRODUCTION TO OPERATORS AND EXPRESSIONS

C supports a rich set of built-in operators. We have already used several of them, such as =, +, -, *, & and <. An operator is a symbol that tells the computer to perform certain mathematical or logical manipulations.

Operators are used in programs to manipulate data and variables. They usually form a part of the mathematical or logical expressions.

C operators can be classified into a number of categories. They include:

- 1. Arithmetic operators
- 2. Relational operators
- 3. Logical operators
- 4. Assignment operators
- 5. Increment and decrement operators
- 6. Conditional operators
- 7. Bitwise operators
- 8. Special operators

An expression is a sequence of operands and operators that reduces to a single value. For example, 10 + 15 is an expression whose value is 25. The value can be any type other than void.

## 1.45 ARITHMETIC OPERATORS

C provides all the basic arithmetic operators. They are listed in Table 1.18. The operators +, -, *, and / all work the same way as they do in other languages. These can operate on any built-in data type allowed in C. The unary minus operator, in effect, multiplies its single operand by -1. Therefore, a number preceded by a minus sign changes its sign.

### Table 1.18 Arithmetic Operators

| Operator | Meaning |
|---|---|
| + | Addition or unary plus |
| - | Subtraction or unary minus |
| * | Multiplication |
| / | Division |
| % | Modulo division |

Integer division truncates any fractional part. The modulo division operation produces the remainder of an integer division. Examples of use of arithmetic operators are:

```
a - b   a + b
a * b   a / b
a % b   -a * b
```

Here a and b are variables and are known as operands. The modulo division operator % cannot be used on floating point data. Note that C does not have an operator for exponentiation. Older versions of C does not support unary plus but ANSI C supports it.

### 1.45.1 Integer Arithmetic

When both the operands in a single arithmetic expression such as a+b are integers, the expression is called an integer expression, and the operation is called integer arithmetic. Integer arithmetic always yields an integer value. The largest integer value depends on the machine, as pointed out earlier. In the above examples, if a and b are integers, then for a = 14 and b = 4 we have the following results:

- a - b = 10
- a + b = 18
- a * b = 56
- a / b = 3 (decimal part truncated)
- a % b = 2 (remainder of division)

During integer division, if both the operands are of the same sign, the result is truncated towards zero. If one of them is negative, the direction of truncation is implementation dependent. That is,

6/7 = 0 and -6/-7 = 0

but -6/7 may be zero or -1. (Machine dependent)

Similarly, during modulo division, the sign of the result is always the sign of the first operand (the dividend). That is

- -14 % 3 = -2
- -14 % -3 = -2
- 14 % -3 = 2

### EXAMPLE 1.34

The program in Fig. 1.87 shows the use of integer arithmetic to convert a given number of days into months and days.

```
Program
main ()
{
    int months, days ;

    printf("Enter days\n") ;
    scanf("%d", &days) ;

    months = days / 30 ;
    days = days % 30 ;
    printf("Months = %d Days = %d", months, days) ;
}

Output
Enter days
265
Months = 8 Days = 25
Enter days
364
Months = 12 Days = 4
Enter days
45
Months = 1 Days = 15
```

Fig. 1.87 Illustration of integer arithmetic

The variables months and days are declared as integers. Therefore, the statement months = days/30; truncates the decimal part and assigns the integer part to months. Similarly, the statement days = days%30; assigns the remainder part of the division to days. Thus the given number of days is converted into an equivalent number of months and days and the result is printed as shown in the output.

### 1.45.2 Real Arithmetic

An arithmetic operation involving only real operands is called real arithmetic. A real operand may assume values either in decimal or exponential notation. Since floating point values are rounded to the number of significant digits permissible, the final value is an approximation of the correct result. If x, y, and z are floats, then we will have:

```
x = 6.0/7.0 = 0.857143
y = 1.0/3.0 = 0.333333
z = -2.0/3.0 = -0.666667
```

The operator % cannot be used with real operands.

### 1.45.3 Mixed-mode Arithmetic

When one of the operands is real and the other is integer, the expression is called a mixed-mode arithmetic expression. If either operand is of the real type, then only the real operation is performed and the result is always a real number. Thus

15/10.0 = 1.5

whereas

15/10 = 1

More about mixed operations will be discussed later when we deal with the evaluation of expressions.

## 1.46 RELATIONAL OPERATORS

We often compare two quantities and depending on their relation, take certain decisions. For example, we may compare the age of two persons, or the price of two items, and so on. These comparisons can be done with the help of relational operators. We have already used the symbol '<', meaning 'less than'. An expression such as

a < b or 1 < 20

containing a relational operator is termed as a relational expression. The value of a relational expression is either one or zero. It is one if the specified relation is true and zero if the relation is false. For example

10 < 20 is true

but

20 < 10 is false

C supports six relational operators in all. These operators and their meanings are shown in Table 1.19.

### Table 1.19 Relational Operators

| Operator | Meaning |
|---|---|
| < | is less than |
| <= | is less than or equal to |
| > | is greater than |
| >= | is greater than or equal to |
| == | is equal to |
| != | is not equal to |
