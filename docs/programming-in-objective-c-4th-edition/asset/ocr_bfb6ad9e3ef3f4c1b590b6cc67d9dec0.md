+   1. If either operand is of type long double, the other is converted to long double, and that is the type of the result.

+   2. If either operand is of type double, the other is converted to double, and that is the type of the result.

+   3. If either operand is of type float, the other is converted to float, and that is the type of the result.

+   4. If either operand is of type _Bool, char, short int, or bit field,or of an enumerated data type, it is converted to int.

+   5. If either operand is of type long long int, the other is converted to long long int, and that is the type of the result.

+   6. If either operand is of type long int, the other is converted to long int, and that is the type of the result.

+   7. If this step is reached, both operands are of type int, and that is the type of the result.

This is actually a simplified version of the steps involved in converting operands in an expression. The rules get more complicated when unsigned operands are involved, but this is detailed enough for this text.

Realize from this series of steps that whenever you reach a step that says “that is the type of the result,”you’re done with the conversion process.

As an example of how to follow these steps, let’s see how the following expression would be evaluated, where f is defined to be a float, i a long int, and s a short int variable:

```
f * i + l / s
```

Consider first the multiplication of f by i, which is the multiplication of a float by an int. From step 3, you know that, because f is of