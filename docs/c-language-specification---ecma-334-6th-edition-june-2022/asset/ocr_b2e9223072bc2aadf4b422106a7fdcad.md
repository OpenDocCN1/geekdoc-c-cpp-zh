# ## 11.12.2 Integer logical operators

The predefined integer logical operators are:

```
```csharp
int operator &(int x, int y);
uint operator &(uint x, uint y);
long operator &(long x, long y);
ulong operator &(ulong x, ulong y);

int operator |(int x, int y);
uint operator |(uint x, uint y);
long operator |(long x, long y);
ulong operator |(ulong x, ulong y);

int operator ^(int x, int y);
uint operator ^(uint x, uint y);
long operator ^(long x, long y);
ulong operator ^(ulong x, ulong y);
```
```

The & operator computes the bitwise logical AND of the two operands, the | operator computes the bitwise logical OR of the two operands, and the ^ operator computes the bitwise logical exclusive OR of the two operands. No overflows are possible from these operations.

Lifted (§11.4.8) forms of the unlifted predefined integer logical operators defined above are also predefined.

# ## 11.12.3 Enumeration logical operators

Every enumeration type `E` implicitly provides the following predefined logical operators:

```
```csharp
E operator &(E x, E y);
E operator |(E x, E y);
E operator ^(E x, E y);
```
```

The result of evaluating `x <op> y`, where x and y are expressions of an enumeration type `E` with an underlying type `U`, and `<op>` is one of the logical operators, is exactly the same as evaluating `(E)((U)x <op> (U)y)`. In other words, the enumeration type logical operators simply perform the logical operation on the underlying type of the two operands.

Lifted (§11.4.8) forms of the unlifted predefined enumeration logical operators defined above are also predefined.

# ## 11.12.4 Boolean logical operators

The predefined Boolean logical operators are:

```
```csharp
bool operator &(bool x, bool y);
bool operator |(bool x, bool y);
bool operator ^(bool x, bool y);
```
```

The result of `x & y` is `true` if both x and y are `true`. Otherwise, the result is `false`.

The result of `x | y` is `true` if either x or y is `true`. Otherwise, the result is `false`.

The result of `x ^ y` is `true` if x is `true` and y is `false`, or x is `false` and y is `true`. Otherwise, the result is `false`. When the operands are of type `bool`, the `^` operator computes the same result as the `!=` operator.