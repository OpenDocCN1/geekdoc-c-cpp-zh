© ISO/IEC 2011 – All rights reserved

ISO/IEC 9899:2011 (E)

```
int f(void) {
char c;
/* */
if ((c = f()) == -1)
/* ... */
}
```

the int returned by the function may be truncated when stored in the char, and converted back to int width prior to conversion. In an implementation where "plain" char has the same range of values as unsigned char (and char is narrower than int), the result of the conversion cannot be negative, the operands of the comparison can never come equal. Therefore, for full portability, the c should be converted as int.

EXAMPLE 2 In the fragment:
char c;
int i;
long l;
l1 = (c = i);

the value of i is converted to the type of the assignment c = i, that is, char type. The value of the expression in parentheses is then converted to the type of the outer assignment expression, that is, long int type.

EXAMPLE 3 Consider the fragment:
const char **cpp;
char *p;
const char c = 'A';

cpp = &p; // constraint violation
*cpp = &c; // valid
*p = 0; // valid

The first assignment is unsafe because it would allow the following valid code to attempt to change the value of the const object c.

# 6.5.16.2 Compound assignment

# Constraints

For the operators += and -= only, if either left operand shall be atomic, qualified, or unqualified pointer to a complete object, and the right shall have integer type; or the left shall have atomic, qualified, or unqualified arithmetic type, and the right shall have arithmetic type.

For the other operators, the left operand shall have atomic, qualified, or unqualified arithmetic type, and (considering the type the left operand would have Aftervalue conversion) each operand shall have arithmetic type consistent with those allowed by the binary operator.

# Semantics

A compound assignment of the form E1 op = E2 is equivalent to the simple assignment E1 = E1 op E2), except that the Value E1 is evaluated only once, and with respect to independently-sequenced function call, the operation of a compound

Language

ISO/IEC 9516.2

103