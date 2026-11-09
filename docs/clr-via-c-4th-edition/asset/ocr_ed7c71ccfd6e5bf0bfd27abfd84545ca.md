C# also allows you to apply operators to nullable instances. The following code shows examples of this.

```
```csharp
private static void Operators() {
    Int32? a = 5;
    Int32? b = null;

    // Unary operators (+  ++  -  --  !  ~)
    a++;
    b = -b; // b = null

    // Binary operators (+  -  *  /  %  &  |  ^  <<  >>)
    a = a + 3; // a = 9
    b = b * 3; // b = null;

    // Equality operators (==  !=)
    if (a == null) { /* no */ } else { /* yes */ }
    if (b == null) { /* yes */ } else { /* no */ }
    if (a != b)    { /* yes */ } else { /* no */ }

    // Comparison operators (<  <=  >  >=)
    if (a < b)     { /* no */ } else { /* yes */ }
}
```
```

Here is how C# interprets the operators:

+   - **Unary operators (+, ++, −, --, !, ~)** If the operand is null, the result is null.
+   - **Binary operators (+, −, *, /, %, &, |, ^, <<, >>)** If either operand is null, the result is null. However, an exception is made when the `&` and `|` operators are operating on Boolean operands, so that the behavior of these two operators gives the same behavior as demonstrated by SQL’s three-valued logic. For these two operators, if neither operand is null, the operator performs as expected, and if both operands are null, the result is null. The special behavior comes into play when just one of the operands is null. The following table lists the results produced by these two operators for all combinations of `true`, `false`, and `null`.
+   - **Equality operators (==, !=)** If both operands are null, they are equal. If one operand is null, they are not equal. If neither operand is null, compare the values to determine if they are equal.
+   - **Relational operators (<, >, <=, >=)** If either operand is null, the result is false. If neither operand is null, compare the values.

| Operand1 → Operand2 ↓ | true | false | null |
|---|---|---|---|
| True | `& = true`<br>`| = true` | `& = false`<br>`| = true` | `& = null`<br>`| = true` |
| False | `& = false`<br>`| = true` | `& = false`<br>`| = false` | `& = false`<br>`| = null` |
| Null | `& = null`<br>`| = true` | `& = false`<br>`| = null` | `& = null`<br>`| = null` |