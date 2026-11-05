# 7. General syntax for overloading binary operator

```
public static ret-type operator op(parameter-type operand1, parameter-type operand1)
{
}
```

# 8. Following is the list of operators that can be overloaded

| Category | Operators | Associativity |
|---|---|---|
| Primary | x.y f(x) a[x] x++ x-- new typeof checked unchecked default delegate | left to right |
| Unary | + - ! ~ ++x --x (T)x true false sizeof | left to right |
| Multiplicative | * / % | left to right |
| Additive | + - | left to right |
| Shift | << >> | left to right |
| Relational and Type testing | < <= > >= is as | left to right |
| Equality | == != | left to right |
| Logical/bitwise And | & | left to right |
| Logical/bitwise Xor | ^ | left to right |
| Logical/bitwise Or | | | left to right |
| Conditional And | && | left to right |
| Conditional Or | || | left to right |
| Conditional | ?: | right to left |
| Assignment | = *= /= %= += -= <<= >>= &= ^= |= ?? => | right to left |