The modulus operator (%) returns the remainder of a division:

```
int num1 = 6;
int num2 = 4;
int remainder = num1 % num2;
Console.WriteLine(remainder);  //---2---
```

The % operator is commonly used for testing whether a number is odd or even, like this:

```
if (num1 % 2 == 0)
    Console.WriteLine("Even");
else
    Console.WriteLine("Odd");
```

# Operator Precedence

When you use multiple operators in the same statement, you need be aware of the precedence of each operator (that is, which operator will evaluate first). The following table shows the various C# operators grouped in the order of precedence. Operators within the same group have equal precedence (operators include some keywords).

| Category | Operators |
|---|---|
| Primary | x.y f(x) a[x] x++ x-- new typeof checked unchecked |
| Unary | + - ! ~ ++x --x (T) x |
| Multiplicative | * / % |
| Additive | + - |
| Shift | << >> |
| Relational and type testing | < > <= >= is as |
| Equality | == != |
| Logical AND | & |
| Logical XOR | ^ |
| Logical OR | \| |
| Conditional AND | && |
| Conditional OR | || |
| Conditional | ? : |
| Assignment | = *= /= %= += -= <<= >>= &= ^= |= |