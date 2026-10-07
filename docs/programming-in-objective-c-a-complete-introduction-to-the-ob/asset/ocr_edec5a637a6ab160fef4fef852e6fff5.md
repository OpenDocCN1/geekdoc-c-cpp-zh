unary operators. Just as the expression -a has no permanent effect on the value of a, neither the expression (float) a.

The type cast operator has higher precedence than all the arithmetic operators except the unary minus and plus. Of, if necessary, you can always use parentheses to force the terms to be evaluated in any desired order.

Another example of the use of the type cast operator, the expression

```
(int) 29.55 + (int) 21.99
```

is evaluated in Objective-C as

```
29 + 21
```

because the effect of casting a float value to an integer is one of truncating the floating-point value. The expression

```
(float) 6 / (float) 4
```

produces a result of 1.5, as does the following expression:

```
(float) 6 / 4
```

The type cast operator is often used to coerce an object that is a generic type into an object of a particular class. For example, the following lines typecasts the value of the variable myNumber to a Fraction object:

```
id myNumber;
Fraction *myFraction;
..
```

```
myFraction = (Fraction *) myNumber;
```

The result of the casting is assigned to the Fraction variable myFraction.

# Assignment Operators

The Objective-C language permits you to combine the arithmetic operators with the assignment operator using the following general format:

```
op=
```

In this format, op is any of the arithmetic operators, including +, -, *, /, or %. In addition, op can be any of the bit operators for shifting and masking, discussed later. Consider this statement:

```
count += 10;
```

The effect of the so-called "plus equals" operator += is to add the expression on the right side of the operator to the expression on the left side of the operator, and to store the result back into the variable on the left side of the operator. So the previous statement is equivalent to this statement:

```
count = count + 10;
```