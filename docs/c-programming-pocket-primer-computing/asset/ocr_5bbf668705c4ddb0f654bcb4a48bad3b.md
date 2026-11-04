arithmetic operators, increment/decrement operators, and ternary operators. The following subsections provide more details about each type of operator.

# Arithmetic Operators

Arithmetic operators are “+”, “-”, “*”, and “/” for addition, subtraction, multiplication, and division, respectively. Arithmetic operators have the following precedence levels in expressions that do not contain parentheses:

+   * * and / have the same level (left-to-right if both appear)
+   * + and - have the same level (left-to-right if both appear)

Parentheses can override the default precedence levels (and can also be nested). The main purpose of parentheses is to alter the default order of execution in expressions that contain arithmetic operators, as shown here:

```
7-5+8 = 2+8 = 10 (left-to-right precedence)
7-(5+8) = 7 - 13 = -6
3*8/4 = 24/4 = 6 (left-to-right precedence)
3*(8/4) = 3*2 = 6
```

When in doubt, use parentheses in an expression. For example, the expression 8*x+y*z/10 is the same as (8*x)+(y*z)/10, but the latter is clearer.

Another arithmetic operator is the modulus % operator, which provides the integer remainder from dividing an integer by a non-zero integer:

```
7 % 4 = 3
10 % 10 = 0
```