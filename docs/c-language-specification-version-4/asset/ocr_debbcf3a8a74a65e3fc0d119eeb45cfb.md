```
class Test
{
    static void Main() {
        X<int>.PrintTypes();
    }
}
```

produces the following output:

```
System.Int32
System.Int32
System.String
System.Double[]
System.Void
System.Int32
X 1[System.Int32]
X 1[X 1[System.Int32]]
X 1[T]
```

Note that int and System.Int32 are the same type.

Also note that the result of typeof(X<>) does not depend on the type argument but the result of typeof(X<T>) does.

# 7.6.12 The checked and unchecked operators

The checked and unchecked operators are used to control the overflow checking context for integral-type arithmetic operations and conversions.

```
checked-expression:
    checked ( expression )
unchecked-expression:
    unchecked ( expression )
```

The checked operator evaluates the contained expression in a checked context, and the unchecked operator evaluates the contained expression in an unchecked context. A checked-expression or unchecked-expression corresponds exactly to a parenthesized-expression (§7.6.3), except that the contained expression is evaluated in the given overflow checking context.

The overflow checking context can also be controlled through the checked and unchecked statements (§8.11).

The following operations are affected by the overflow checking context established by the checked and unchecked operators and statements:

+   - The predefined ++ and -- unary operators (§7.6.9 and §7.7.5), when the operand is of an integral type.
+   - The predefined - unary operator (§7.7.2), when the operand is of an integral type.
+   - The predefined +, -, *, and / binary operators (§7.8), when both operands are of integral types.
+   - Explicit numeric conversions (§6.2.1) from one integral type to another integral type, or from float or double to an integral type.

When one of the above operations produce a result that is too large to represent in the destination type, the context in which the operation is performed controls the resulting behavior:

+   - In a checked context, if the operation is a constant expression (§7.19), a compile-time error occurs. Otherwise, when the operation is performed at run-time, a System.OverflowException is thrown.
+   - In an unchecked context, the result is truncated by discarding any high-order bits that do not fit in the destination type.