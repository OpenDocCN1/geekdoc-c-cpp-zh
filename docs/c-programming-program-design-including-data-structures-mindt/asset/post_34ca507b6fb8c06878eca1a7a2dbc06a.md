
## Order of Precedence

Consider the following expressions, which you have been accustomed to working with since high school: -5, 8 - 7, 3 + 4, 2 + 3 * 5, 5.6 + 6.2 * 3, and x + 2 * 5 + 6 / y, where x and y are unknown numbers. These are examples of **arithmetic expressions**. The numbers appearing in the expressions are called **operands**. The numbers that are used to evaluate an operator are called the operands for that operator.

In expression -5, the symbol - specifies that the number 5 is negative. In this expression, - has only one operand. Operators that have only one operand are called **unary operators**.

In expression 8 - 7, the symbol - is used to subtract 7 from 8. In this expression, - has two operands, 8 and 7. Operators that have two operands are called **binary operators**.

**Unary operator**: An operator that has only one operand.

**Binary operator**: An operator that has two operands.

In expression 3 + 4, 3 and 4 are the operands for the operator +. In this expression, the operator + has two operands and is a binary operator. Moreover, in the expression +27, the operator + indicates that the number 27 is positive. Here, + has only one operand and so acts as a unary operator.

From the preceding discussion, it follows that - and + are both unary and binary arithmetic operators. However, as arithmetic operators, *, /, and % are binary and so must have two operands.

### Order of Precedence

When more than one arithmetic operator is used in an expression, C++ uses the operator precedence rules to evaluate the expression. According to the order of precedence rules for arithmetic operators, `*`, `/`, and `%` are at a higher level of precedence than `+` and `-`.

Note that the operators *, /, and % have the same level of precedence. Similarly, the operators + and - have the same level of precedence.

When operators have the same level of precedence, the operations are performed from left to right. To avoid confusion, you can use parentheses to group arithmetic expressions. For example, using the order of precedence rules,

```
3 * 7 - 6 + 2 * 5 / 4 + 6
```

means the following:

```
(((3 * 7) - 6) + ((2 * 5) / 4)) + 6
= ((21 - 6) + (10 / 4)) + 6          (Evaluate *)
= ((21 - 6) + 2) + 6                 (Evaluate /. Note that this is an integer division.)
= (15 + 2) + 6                       (Evaluate -)
= 17 + 6                             (Evaluate first +)
= 23                                 (Evaluate +)
```

Note that the use of parentheses in the second example clarifies the order of precedence. You can also use parentheses to override the order of precedence rules.

Because arithmetic operators, using the precedence rules, are evaluated from left to right, unless parentheses are present, the **associativity** of the arithmetic operators is said to be from left to right.

> **NOTE**
>
> **(Character Arithmetic)** Because the `char` data type is also an integral data type, C++ allows you to perform arithmetic operations on `char` data. However, you should use this ability carefully. There is a difference between the character `'8'` and the integer `8`. The integer value of `8` is `8`. The integer value of `'8'` is `56`, which is the ASCII collating sequence of the character `'8'`.
>
> When evaluating arithmetic expressions, `8 + 7 = 15`; `'8' + '7' = 56 + 55`, which yields `111`; and `'8' + 7 = 56 + 7`, which yields `63`. Furthermore, because `'8' * '7' = 56 * 55 = 3080` and the ASCII character set has only `128` values, `'8' * '7'` is undefined in the ASCII character data set.
>
> These examples illustrate that many things can go wrong when you are performing character arithmetic. If you must employ them, use arithmetic operations on the `char` data type with caution.

The following example shows how arithmetic operators work.

### EXAMPLE 2-5

```cpp
// This program illustrates how arithmetic operators work.

#include <iostream>

using namespace std;

int main()
{
    cout << "2 + 5 = " << 2 + 5 << endl;
    cout << "13 + 89 = " << 13 + 89 << endl;
    cout << "34 - 20 = " << 34 - 20 << endl;
    cout << "45 - 90 = " << 45 - 90 << endl;
    cout << "2 * 7 = " << 2 * 7 << endl;
    cout << "5 / 2 = " << 5 / 2 << endl;
    cout << "14 / 7 = " << 14 / 7 << endl;
    cout << "34 % 5 = " << 34 % 5 << endl;
    cout << "4 % 6 = " << 4 % 6 << endl << endl;

    cout << "5.0 + 3.5 = " << 5.0 + 3.5 << endl;
    cout << "3.0 + 19.4 = " << 3.0 + 19.4 << endl;
    cout << "16.3 - 5.2 = " << 16.3 - 5.2 << endl;
    cout << "4.2 * 2.5 = " << 4.2 * 2.5 << endl;
    cout << "5.0 / 2.0 = " << 5.0 / 2.0 << endl;
    cout << "34.5 / 6.0 = " << 34.5 / 6.0 << endl;
    cout << "34.5 / 6.5 = " << 34.5 / 6.5 << endl;

    return 0;
}
```

### Sample Run

```text
2 + 5 = 7
13 + 89 = 102
34 - 20 = 14
45 - 90 = -45
2 * 7 = 14
5 / 2 = 2
14 / 7 = 2
34 % 5 = 4
4 % 6 = 4

5.0 + 3.5 = 8.5
3.0 + 19.4 = 22.4
16.3 - 5.2 = 11.1
4.2 * 2.5 = 10.5
5.0 / 2.0 = 2.5
34.5 / 6.0 = 5.75
34.5 / 6.5 = 5.30769
```

> **NOTE**
> You should be careful when evaluating the mod operator with negative integer operands. You might not get the answer you expect. For example, `-34 % 5 = -4`, because in the division `-34 / 5`, the quotient is `-6` and the remainder is `-4`. Similarly, `34 % -5 = 4`, because in the division `34 / -5`, the quotient is `-6` and the remainder is `4`. Also `-34 % -5 = -4`, because in the division `-34 / -5`, the quotient is `6` and the remainder is `-4`.

## Expressions

There are three types of arithmetic expressions in C++:

- **Integral expressions**—all operands in the expression are integers. An integral expression yields an integral result.
- **Floating-point (decimal) expressions**—all operands in the expression are floating points (decimal numbers). A floating-point expression yields a floating-point result.
- **Mixed expressions**—the expression contains both integers and decimal numbers.

Looking at some examples will help clarify these definitions.

### EXAMPLE 2-6

Consider the following C++ integral expressions:

```
2 + 3 * 5
3 + x - y / 7
x + 2 * (y - z) + 18
```

In these expressions, x, y, and z are variables of type int.

### EXAMPLE 2-7

Consider the following C++ floating-point expressions:

```
12.8 * 17.5 - 34.50
x * 10.5 + y - 16.2
```

Here, x and y are variables of type double.

Evaluating an integral or a floating-point expression is straightforward. As before, when operators have the same precedence, the expression is evaluated from left to right. You can always use parentheses to group operands and operators to avoid confusion.

Next, we discuss mixed expressions.

### Mixed Expressions

An expression that has operands of different data types is called a **mixed expression**. A mixed expression contains both integers and floating-point numbers. The following expressions are examples of mixed expressions:

```
2 + 3.5
6 / 4 + 3.9
5.4 * 2 - 13.6 + 18 / 2
```

In the first expression, the operand + has one integer operand and one floating-point operand. In the second expression, both operands for the operator / are integers, the first operand of + is the result of 6 / 4, and the second operand of + is a floating-point number. The third example is an even more complicated mix of integers and floating-point numbers. The obvious question is: How does C++ evaluate mixed expressions?

Two rules apply when evaluating a mixed expression:

- 1. When evaluating an operator in a mixed expression:
  - a. If the operator has the same types of operands (that is, either both integers or both floating-point numbers), the operator is evaluated according to the type of operands. Integer operands thus yield an integer result; floating-point numbers yield a floating-point number.
  - b. If the operator has both types of operands (that is, one is an integer and the other is a floating-point number), then during calculation, the integer is changed to a floating-point number with the decimal part of zero and the operator is evaluated. The result is a floating-point number.
- 2. The entire expression is evaluated according to the precedence rules; the multiplication, division, and modulus operators are evaluated before the addition and subtraction operators. Operators having the same level of precedence are evaluated from left to right. Grouping using parentheses is allowed for clarity.

From these rules, it follows that when evaluating a mixed expression, you concentrate on one operator at a time, using the rules of precedence. If the operator to be evaluated has operands of the same data type, evaluate the operator using Rule 1(a). That is, an operator with integer operands will yield an integer result, and an operator with floating-point operands will yield a floating-point result. If the operator to be evaluated has one integer operand and one floating-point operand, before evaluating this operator, convert the integer operand to a floating-point number with the decimal part of 0. The following examples show how to evaluate mixed expressions.

### EXAMPLE 2-8

| Mixed Expression | Evaluation | Rule Applied |
|---|---|---|
| `3 / 2 + 5.5` | `= 1 + 5.5`<br>`= 6.5` | `3 / 2 = 1` (integer division; Rule 1(a))<br>`1 + 5.5 = 1.0 + 5.5` (Rule 1(b))<br>`= 6.5` |
| `15.6 / 2 + 5` | `= 7.8 + 5`<br>`= 12.8` | `15.6 / 2 = 15.6 / 2.0` (Rule 1(b))<br>`= 7.8`<br>`7.8 + 5 = 7.8 + 5.0` (Rule 1(b))<br>`= 12.8` |
| `4 + 5 / 2.0` | `= 4 + 2.5`<br>`= 6.5` | `5 / 2.0 = 5.0 / 2.0` (Rule 1(b))<br>`= 2.5`<br>`4 + 2.5 = 4.0 + 2.5` (Rule 1(b))<br>`= 6.5` |
| `4 * 3 + 7 / 5 - 25.5` | `= 12 + 7 / 5 - 25.5`<br>`= 12 + 1 - 25.5`<br>`= 13 - 25.5`<br>`= -12.5` | `4 * 3 = 12` (Rule 1(a))<br>`7 / 5 = 1` (integer division; Rule 1(a))<br>`12 + 1 = 13` (Rule 1(a))<br>`13 - 25.5 = 13.0 - 25.5` (Rule 1(b))<br>`= -12.5` |
