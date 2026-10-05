# 4.1. EXPRESSIONS

| Operator | Meaning |
| --- | --- |
| + | addition |
| - | subtraction |
| * | multiplication |
| / | division |
| % | modulus |

Table 4.1: The simple C++ arithmetic operators

x = y + z;

the right side is an addition expression y + z. The two operands of the + operator are y and z. Two of the operators above, + and -, serve as unary operators. A unary operator has only one operand. The unary operator expects a single numeric expression (literal number, variable, or complex numeric expression) immediately to its right; it computes the additive inverse of its operand. If the operand is positive (greater than zero), the result is a negative value of the same magnitude; if the operand is negative (less than zero), the result is a positive value of the same magnitude. Zero is unaffected. For, the following code sequence

```
int x = 3;
int y = -4;
int z = 0;
cout << -x << " " << -y << " " << -z << endl;
```

within a program would print

```
-3 4 0
```

The following statement

```
cout << - (4 - 5) << endl;
```

within a program would print

```
1
```

The unary + operator is used only for completeness; when applied to a numeric value, variable, or expression, the resulting value is no different from the original value of its operand. Omitting the unary + operator from the following statement

x = +y;

does not change the statement's behavior.
All the arithmetic objects are subject to the limitations of the data types on which they operate; for example, on a system where the largest int is 2,147,483,647, the expression
2147483647 + 1