# A.1.9 Assignments and Expressions

You are an expression by combining variables, constants, operators, and parentheses. The assign- statement

```
volume = 4 * PI * radius * radius * radius / 3;
```

assigns to the previously declared volume the value of the arithmetic expression on the right- hand of the arithmetic operator = ; assigning that PI and radius have values. The assignment statement

```
double volume = 4 * PI * radius * radius * radius / 3;
```

appears in line 10 of Figure A-1, also declares volume's data type, since it was not declared previously.
The various kinds of expressions that you can use in an assignment statement are discussed next.
Arithmetic expressions. You can combine variables and constants with arithmetic operators and parentheses to form arithmetic expressions. The arithmetic operators are

+   - Binary add or unary plus
- Binary subtract or unary minus
- Multiply
- Divide
- Remainder after division

The operators *, /, and % have the same precedence, which is higher than of + and - ; unary operators' have higher precedence than binary operators. The following examples demonstrate operator precedence:

```
a - b / c    means (b/c) (precedence of over /)
-5 / a      means (-5)/a (precedence of unary operator -)
a / -5      means a/ -5 (precedence of unary operator -)
```

Arithmetic operators and most other operators are left-associative. That is, the precedence execute from left to right within an expression. Thus,

```
a * c
```

means

```
(a / b) * c
```

The assignment operator and all unary operators are right-associative, as you will see later. You can use parentheses to override precedence and associativity.

Relational and logical expressions. You can combine variables and constants with parentheses; with the relational, or comparison, operators <, >, and with the equality operators == (equal to) and != (not equal) to form a relational expression. Such an expression is true or false according to the validity of the specified. The expression 5 == 4 has a value of false because 5 is not equal to 4. Equality operators have a lower precedence than relational operators.
You can combine variables and constants of the arithmetic types, relational expressions, and the logical operators && (and) and || (or) to form logical expressions, which are either true or false. C++ evaluates logical expressions from left to right and stops as soon as the value of the entire expression

2 A list of all C++ operators and their precedences appears inside the cover of this book.
3 A unary operator requires only one operand; for example, the - in -5. A binary operator requires two operands; for example, the + in 2+3.