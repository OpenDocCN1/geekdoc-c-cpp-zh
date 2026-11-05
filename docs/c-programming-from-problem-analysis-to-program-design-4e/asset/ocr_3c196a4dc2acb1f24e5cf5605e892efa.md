Notice how an arithmetic operator is part of one of the operands in the last row of Table 5-1. The expression 19 % 5 produces 4 as a remainder; thus 4 != (19 % 5) returns false. The operand can also include a call to a value-returning method. You can use any valid executable statement that produces or returns a value as an operand.

Consider the next conditional expression. When operand1 has a value of 25, the expression returns true (5² is equal to 25). When operand1 is not 25, the expression returns false.

```
(operand1 == Math.Pow(5,2))
```

> NOTE
> Although not a requirement when comparing a variable to a literal value, it is conventional to place the variable in the first operand location with a value in the second location.

When you use the equality operator with integral values, such as variables of type int, the results produced are what you would expect; however, you need to be cautious of making equality comparisons with floating-point (float and double) and decimal types. In the following code segment, consider the compile-time initialization of aValue followed by the conditional expression:

```
double aValue = 10.0 / 3.0;
if (aValue == 3.3333333333333)
```

The expression returns false. Floating-point division does not produce a finite value. Because of rounding, you often get unpredictable results when comparing floating-point variables for equality.

The == and != are overloaded operators. You learned about overloaded methods in Chapter 4. Overloaded operators are defined to perform differently based on their operands. In addition to being defined for numeric data types, == and != are defined for strings in C#. The operators perform a completely different function when the operands are of string data type in contrast to numeric type. When strings are compared, the first character in the first operand is compared against the first character in the second operand. If they are the same, the comparison moves to the second characters. The characters are compared lexicographically using the Unicode character set.

> NOTE
> Words are placed in a dictionary in lexicographical order. The word "Able" comes before "Ada" in the dictionary. The Unicode uppercase character A comes before the lowercase character a.

# EXAMPLE 5.2

```
("The class name is CS158" == "The class name is cs158")
```