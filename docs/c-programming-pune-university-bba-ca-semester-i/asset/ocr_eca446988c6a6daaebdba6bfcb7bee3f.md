# ### Example #5: Shift Operators

```
```c
#include <stdio.h>
void main()
{
    int num=212, i;
    for (i=0; i<=2; ++i)
        printf("Right shift by %d: %d\n", i, num>>i);

    printf("\n");

    for (i=0; i<=2; ++i)
        printf("Left shift by %d: %d\n", i, num<<i);
    getch( );
}
```
```

Right Shift by 0: 212
Right Shift by 1: 106
Right Shift by 2: 53
Left Shift by 0: 212
Left Shift by 1: 424
Left Shift by 2: 848

(f) Comma Operator: Comma operators are used to link related expressions together. For example:
    int a, c = 5, d;

# ## 1.4.2 Precedence and Associativity

# ### C Operator Precedence Table

This page lists C operators in order of *precedence* (highest to lowest). Their *associativity* indicates in what order operators of equal precedence in an expression are applied.

| Operator | Description | Associativity |
| --- | --- | --- |
| ( ) | Parentheses (function call) (see Note 1) | left-to-right |
| [ ] | Brackets (array subscript) | left-to-right |
| . | Member selection via object name | left-to-right |
| -> | Member selection via pointer | left-to-right |
| ++ -- | Postfix increment/decrement (see Note 2) | left-to-right |
| ++ -- | Prefix increment/decrement | right-to-left |
| + - | Unary plus/minus | right-to-left |
| ! ~ | Logical negation/bitwise complement | right-to-left |
| (type) | Cast (convert value to temporary value of type) | right-to-left |
| * | Dereference | right-to-left |
| & | Address (of operand) | right-to-left |
| sizeof | Determine size in bytes on this implementation | right-to-left |
| * / % | Multiplication/Division/Modulus | left-to-right |