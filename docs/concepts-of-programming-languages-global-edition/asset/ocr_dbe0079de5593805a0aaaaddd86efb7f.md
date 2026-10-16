When the nonarithmetic operators of the C-based languages are included, there are more than 40 operators and at least 14 different levels of precedence. This is clear evidence of the richness of the collections of operators and the complexity of expressions possible in these languages.

Readability dictates that a language should include a Boolean type, as was stated in Chapter 6, rather than simply using numeric types in Boolean expressions. Some error detection is lost in the use of numeric types for Boolean operands, because any numeric expression, whether intended or not, is a legal operand to a Boolean operator. In the other imperative languages, any non-Boolean expression used as an operand of a Boolean operator is detected as an error.

# 7.6 Short-Circuit Evaluation

A short-circuit evaluation of an expression is one in which the result is determined without evaluating all of the operands and/or operators. For example, the value of the arithmetic expression

```
(13 * a) * (b / 13 - 1)
```

is independent of the value of (b / 13 - 1) if a is 0, because 0 * x = 0 for any x. So, when a is 0, there is no need to evaluate (b / 13 - 1) or perform the second multiplication. However, in arithmetic expressions, this shortcut is not easily detected during execution, so it is never taken.

The value of the Boolean expression

```
(a >= 0) && (b < 10)
```

is independent of the second relational expression if a < 0, because the expression (FALSE && (b < 10)) is FALSE for all values of b. So, when a is less than zero, there is no need to evaluate b, the constant 10, the second relational expression, or the && operation. Unlike the case of arithmetic expressions, this shortcut can be easily discovered during execution.

To illustrate a potential problem with non-short-circuit evaluation of Boolean expressions, suppose Java did not use short-circuit evaluation. A table lookup loop could be written using the while statement. One simple version of Java code for such a lookup, assuming that list, which has listlen elements, is the array to be searched and key is the searched-for value, is

```
index = 0;
while ((index < listlen) && (list[index] != key))
    index = index + 1;
```

If evaluation is not short-circuit, both relational expressions in the Boolean expression of the while statement are evaluated, regardless of the value of the