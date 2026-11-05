# 7.6.12 The checked and unchecked Operators

The checked and unchecked operators are used to control the *overflow checking context* for integral-type arithmetic operations and conversions.

```
checked-expression:
    checked   (  expression  )

unchecked-expression:
    unchecked   (  expression  )
```

The checked operator evaluates the contained expression in a checked context, and the unchecked operator evaluates the contained expression in an unchecked context. A *checked-expression* or *unchecked-expression* corresponds exactly to a *parenthesized-expression* (§7.6.3), except that the contained expression is evaluated in the given overflow checking context.

> > **JON SKEET**  In most cases, overflow indicates an error—but in my experience, most developers (including myself) usually build without the checking feature on by default. Obviously, this approach has a performance penalty, but that's usually preferable to silently corrupted data. It would possibly make sense to make `/checked+` the default for debug builds and `/checked-` the default for release builds—although I’m generally wary of behavioral changes between debug and release. This would be a little like the behavior of cross-thread exceptions in Windows Forms.
> >
> > One situation where unchecked overflow behavior is almost always appropriate is in GetHashCode implementations, where the magnitude of the value generated doesn't really matter; in essence, it's just an arbitrary bit pattern.

The overflow checking context can also be controlled through the checked and unchecked statements (§8.11).

The following operations are affected by the overflow checking context established by the checked and unchecked operators and statements:

+   - The predefined `++` and `--` unary operators (§7.6.9 and §7.7.5), when the operand is of an integral type.
+   - The predefined `-` unary operator (§7.7.2), when the operand is of an integral type.
+   - The predefined `+`, `-`, `*`, and `/` binary operators (§7.8), when both operands are of integral types.