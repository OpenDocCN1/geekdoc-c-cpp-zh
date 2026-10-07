# Bit Operators 211

Consider first the multiplication of f by i, which is the multiplication of a float by an int. From step 3, you know that, because f is of type float, the other operand (i) will also be converted to type float, and that will be the result of the multiplication.

Next, 1 is divided by s, which is the division of a long int by a short int. Step 4 tells you that the short int will be promoted to an int. Continuing, step 6 shows that because one of the operands (1) is a long int, the other operand will be converted to a long int, which will also be the result of the result. This division will produce a value of type long int, with any fractional part resulting from the division truncated.

Step 3 indicates that, if one of the operands in an expression is of type float (as the result of multiplying f * i), the other operand will be converted to type float, which will be the type of the result. Therefore, after the division of 1 by s, the result of the operation will be converted to type float and then added into the product of f and i. The final result of the preceding expression will therefore be a value of type float.

Remember, the type cast can always be used to explicitly force conversions and thereby control the way in which a particular expression is evaluated.
Thus, if you didn't want the division of 1 by s to be truncated in the preceding expression value, you could have type-cast one of the operands to type float, forcing the value to be performed as a floating-point division:

```
f * i + (float) 1 / s
```

# Bit Operators

Various operators in the Objective-C language with the particular bits used to represent an integer value. Table 10.1 presents these operators.

# Table 10.1 Bit Operators

| Symbol | Operation |
| --- | --- |
| & | Bitwise AND |
| | | Bitwise inclusive-OR |
| ^ | Bitwise OR |
| ~ | Ones complement |
| << | Left shift |
| >> | Right shift |