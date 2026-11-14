# Table C-1: Continued

| Description | Notation | Assoc. |
| :--- | :--- | :--- |
| Shift left | `expr << expr` | ←← |
| Shift right | `expr >> expr` | ←← |
| Less than | `expr < expr` | ←← |
| Less than or equal | `expr <= expr` | ←← |
| Greater than | `expr > expr` | ←← |
| Greater than or equal | `expr >= expr` | ←← |
| Equal | `expr == expr` | ←← |
| Not equal | `expr != expr` | ←← |
| Bitwise AND | `expr & expr` | ←← |
| Bitwise exclusive OR (XOR) | `expr ^ expr` | ←← |
| Bitwise inclusive OR | `expr | expr` | ←← |
| Bitwise inclusive OR | `expr || expr` | ←← |
| Logical OR | `expr || expr` | ←← |
| Logical expression | `expr ? expr : expr` | ←→ |
| Simple assignment | `lvalue = expr` | →→ |
| Multiply and assign | `lvalue *= expr` | →→ |
| Divide and assign | `lvalue /= expr` | →→ |
| Modulo and assign | `lvalue %= expr` | →→ |
| Add and assign | `lvalue += expr` | →→ |
| Subtract and assign | `lvalue -= expr` | →→ |
| Shift left and assign | `lvalue <<= expr` | →→ |
| Shift right and assign | `lvalue >>= expr` | →→ |
| Bitwise AND and assign | `lvalue &= expr` | →→ |
| Bitwise inclusive OR and assign | `lvalue |= expr` | →→ |
| Bitwise exclusive OR and assign | `lvalue ^= expr` | →→ |
| Throw an exception | `throw expr` | – |
| Comma (sequencing) | `expr , expr` | ←← |

The table is taken from [43, §10.3]; we provided the associativity of the binary and ternary operators. Unary operators of the same priority are evaluated from inside out. In expressions with left-associative operators, the left sub-expression is evaluated first; for instance:

```
a + b + c + d + e     // Corresponds to:
((((a + b) + c) + d) + e
```

Assignments are right-associative; that is:

```
a= b= c= d= e       // Corresponds to:
a= (b= (c= (d= e)))
```

A noteworthy detail is the definition of `sizeof`. It can be applied directly to expressions like objects but needs parentheses when applied to a type:

```
int i;
sizeof i;          // Okay: i is an expression
```