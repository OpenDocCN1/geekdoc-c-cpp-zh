# ## 5.2 ARITHMETIC OPERATORS

C provides all the basic arithmetic operators. They are listed in Table 5.1. The operators +, −, *, and / all work the same way as they do in other languages. These can operate on any built-in data type allowed in C. The unary minus operator, in effect, multiplies its single operand by −1. Therefore, a number preceded by a minus sign changes its sign.

**Table 5.1** *Arithmetic Operators*

| Operator | Meaning |
| :---: | :--- |
| + | Addition or unary plus |
| − | Subtraction or unary minus |
| * | Multiplication |
| / | Division |
| % | Modulo division |

Integer division truncates any fractional part. The modulo division operation produces the remainder of an integer division. Examples of use of arithmetic operators are:

```
    a − b        a + b
    a * b        a / b
    a % b       −a * b
```

Here **a** and **b** are variables and are known as *operands*. The modulo division operator % cannot be used on floating point data. Note that C does not have an operator for *exponentiation*. Older versions of C does not support unary plus but ANSI C supports it.

# ### 5.2.1 Integer Arithmetic

When both the operands in a single arithmetic expression such as a+b are integers, the expression is called an *integer expression*, and the operation is called *integer arithmetic*. Integer arithmetic always yields an integer value. The largest integer value depends on the machine, as pointed out earlier. In the above examples, if **a** and **b** are integers, then for **a** = 14 and **b** = 4 we have the following results:

```
    a − b = 10
    a + b = 18
    a * b = 56
    a / b = 3 (decimal part truncated)
    a % b = 2 (remainder of division)
```

During integer division, if both the operands are of the same sign, the result is truncated towards zero. If one of them is negative, the direction of truncation is implementation dependent. That is,

6/7 = 0 and −6/7 = 0

but −6/7 may be zero or −1. (Machine dependent)

Similarly, during modulo division, the sign of the result is always the sign of the first operand (the dividend). That is,

−14 % 3 = −2