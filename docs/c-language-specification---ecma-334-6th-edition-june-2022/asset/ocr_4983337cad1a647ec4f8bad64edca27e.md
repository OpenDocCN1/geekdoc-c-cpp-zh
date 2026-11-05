+   - Otherwise, both operands are converted to type int.

*Note:* The first rule disallows any operations that mix the `decimal` type with the `double` and `float` types. The rule follows from the fact that there are no implicit conversions between the `decimal` type and the `double` and `float` types. *end note*

*Note:* Also note that it is not possible for an operand to be of type `ulong` when the other operand is of a signed integral type. The reason is that no integral type exists that can represent the full range of `ulong` as well as the signed integral types. *end note*

In both of the above cases, a cast expression can be used to explicitly convert one operand to a type that is compatible with the other operand.

*Example:* In the following code

```
decimal AddPercent(decimal x, double percent) => x * (1.0 + percent / 100.0);
```

a binding-time error occurs because a `decimal` cannot be multiplied by a `double`. The error is resolved by explicitly converting the second operand to `decimal`, as follows:

```
decimal AddPercent(decimal x, double percent) => x * (decimal)(1.0 + percent / 100.0);
```

*end example*

**End of informative text.**

# 11.4.8 Lifted operators

**Lifted operators** permit predefined and user-defined operators that operate on non-nullable value types to also be used with nullable forms of those types. Lifted operators are constructed from predefined and user-defined operators that meet certain requirements, as described in the following:

+   - For the unary operators +, ++, -, --, !, and ~, a lifted form of an operator exists if the operand and result types are both non-nullable value types. The lifted form is constructed by adding a single ? modifier to the operand and result types. The lifted operator produces a null value if the operand is null. Otherwise, the lifted operator unwraps the operand, applies the underlying operator, and wraps the result.
+   - For the binary operators +, -, *, /, %, &, |, ^, <<, and >>, a lifted form of an operator exists if the operand and result types are all non-nullable value types. The lifted form is constructed by adding a single ? modifier to each operand and result type. The lifted operator produces a null value if one or both operands are null (an exception being the & and | operators of the bool? type, as described in §11.12.5). Otherwise, the lifted operator unwraps the operands, applies the underlying operator, and wraps the result.
+   - For the equality operators == and !=, a lifted form of an operator exists if the operand types are both non-nullable value types and if the result type is bool. The lifted form is constructed by adding a single ? modifier to each operand type. The lifted operator considers two null values equal, and a null value unequal to any non-null value. If both operands are non-null, the lifted operator unwraps the operands and applies the underlying operator to produce the bool result.
+   - For the relational operators <, >, <=, and >=, a lifted form of an operator exists if the operand types are both non-nullable value types and if the result type is bool. The lifted form is constructed by adding a single ? modifier to each operand type. The lifted operator produces the value false if one or both operands are null. Otherwise, the lifted operator unwraps the operands and applies the underlying operator to produce the bool result.