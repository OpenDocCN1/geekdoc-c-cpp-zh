| Operators | Description | Associativity |
|---|---|---|
| `++` `--` | Prefix increment/decrement | right-to-left |
| `+` `-` | Unary plus/minus | right-to-left |
| `!` `~` | Logical negation/bitwise complement | right-to-left |
| `(type)` | Cast (convert value to temporary value of *type*) | right-to-left |
| `*` | Dereference | right-to-left |
| `&` | Address (of operand) | right-to-left |
| `sizeof` | Determine size in bytes on this implementation | right-to-left |
| `* / %` | Multiplication/division/modulus | left-to-right |
| `+ −` | Addition/subtraction | left-to-right |
| `<< >>` | Bitwise shift left, Bitwise shift right | left-to-right |
| `< <=`<br>`> >=` | Relational less than/less than or equal to<br>Relational greater than/greater than or equal to | left-to-right |
| `== !=` | Relational is equal to/is not equal to | left-to-right |
| `&` | Bitwise AND | left-to-right |
| `^` | Bitwise exclusive OR | left-to-right |
| `|` | Bitwise inclusive OR | left-to-right |
| `&&` | Logical AND | left-to-right |
| `||` | Logical OR | left-to-right |
| `? :` | Ternary conditional | right-to-left |
| `=` | Assignment | right-to-left |
| `+= -=` | Addition/subtraction assignment | right-to-left |
| `*= /=` | Multiplication/division assignment | right-to-left |
| `%= &=` | Modulus/bitwise AND assignment | right-to-left |
| `^= |=` | Bitwise exclusive/inclusive OR assignment | right-to-left |
| `<<= >>=` | Bitwise shift left/right assignment | right-to-left |
| `,` | Comma (separate expressions) | left-to-right |

# Expressions and statements

# Expression

+   - Expression is a sequence of operators and operands that specifies computation of a value. An expressions may consist of single entity or some combination of such entities interconnected by one or more operators.

In C every expression evaluates to a value i.e., every expression results in some value of a certain type(that can be assigned to a variable). Some examples of expression are shown in the table given below.

```
a+b
```

```
3.14*r*r
```