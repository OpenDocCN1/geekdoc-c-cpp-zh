# 4.2.2 Type Coercion

As noted earlier, in the mixed-type expression 6.0 / 4 that involves both integer and real operands, C++ performs real division and produces the real value 1.5. This is because the compiler automatically converts the integer value 4 to a real value 4.0, and then performs the real division operation 6.0 / 4.0. This automatic type conversion by the compiler is known as type coercion. It also occurs in mixed-type expressions involving characters and integers or reals; the character values are automatically replaced by their numeric codes (see Section 3.3). For example, if characters are represented in ASCII, the value of the expression 'a' + 3 is 99 because 'a' is replaced by 96, its numeric code.

In general, these type conversions take place automatically in any mixed-type expression with “narrow” values—those stored in a smaller number of bits—being converted to “wider” values that occupy a larger number of bits. This automatic widening of a narrower value to the size of a wider value in an expression is known as promotion of the narrower value. It is what permits character, integer, and real values to be freely intermixed in C++ expressions. Two values are said to be compatible if (i) they have the same type, (ii) one can be promoted to the type of the other, or (iii) both can be promoted to the same type. For example, int and double are compatible, because int can be promoted to double.

# 4.2.2.1 Explicit Type Conversions

In addition to automatic type conversions, explicit conversions are also possible. For example, if intVal is an integer value, then either of the expressions double(intVal) or (double)intVal produces the double value equivalent to intVal. Similarly, if doubleVal is of type double, either of int(doubleVal) or (int)doubleVal will truncate the fractional part of doubleVal and produce its integer part.

In general, an expression of the form

```
type(expression)
```

or

```
(type)expression
```

where type is a valid C++ type can be used to convert the type of expression to type (if possible). The first form is sometimes referred to as functional notation and the last form as (C-style) cast notation.

# 4.3 ASSIGNMENT EXPRESSIONS

An assignment expression uses the assignment operator (=) to assign a value to a variable.

# ASSIGNMENT EXPRESSION

# Form:

```
variable = expression
```