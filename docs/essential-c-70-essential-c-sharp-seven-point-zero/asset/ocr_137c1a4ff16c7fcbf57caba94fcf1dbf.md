It is not necessary to evaluate both sides of an OR expression, because if either operand is true, the result is known to be true regardless of the value of the other operand. Like all operators in C#, the left operand is evaluated before the right one, so if the left portion of the expression evaluates to true, the right portion is ignored. In the example in Listing 4.32, if hourOfTheDay has the value 33, then (hourOfTheDay > 23) will evaluate to true and the OR operator will ignore the second half of the expression, short-circuiting it. Short-circuiting an expression also occurs with the Boolean AND operator. (Note that the parentheses are not necessary here; the logical operators are of higher precedence than the relational operators. However, it is clearer to the novice reader to parenthesize the subexpressions for clarity.)

# AND Operator (&&)

The Boolean AND operator, &&, evaluates to true only if both operands evaluate to true. If either operand is false, the result will be false. Listing 4.33 writes a message if the given variable is both greater than 10 and less than 24.4 Similarly to the OR operator, the AND operator will not always evaluate the right side of the expression. If the left operand is determined to be false, the overall result will be false regardless of the value of the right operand, so the runtime skips evaluating the right operand.

```
LISTING 4.33: Using the AND Operator

```
if ((10 < hourOfTheDay) && (hourOfTheDay < 24))
    System.Console.WriteLine(
        "Hi-Ho, Hi-Ho, it's off to work we go.");
```
```

# Exclusive OR Operator (^)

The caret symbol, ^, is the exclusive OR (XOR) operator. When applied to two Boolean operands, the XOR operator returns true only if exactly one of the operands is true, as shown in Table 4.3.

4. The typical hours that programmers work each day.