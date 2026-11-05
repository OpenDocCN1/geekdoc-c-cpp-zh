pointer types cannot be used as type arguments, and there are no conversions from pointer types to non-pointer types.

+   - The explicit reference conversion (§6.2.4) from System.Array and the interfaces it implements to any array-type applies to pointer arrays.
+   - The explicit reference conversions (§6.2.4) from System.Collections.Generic.IList<S> and its base interfaces to a single-dimensional array type T[] never applies to pointer arrays, since pointer types cannot be used as type arguments, and there are no conversions from pointer types to non-pointer types.

These restrictions mean that the expansion for the foreach statement over arrays described in §8.8.4 cannot be applied to pointer arrays. Instead, a foreach statement of the form

```
foreach (V v in x) embedded-statement
```

where the type of x is an array type of the form T[, ...], n is the number of dimensions minus 1 and T or V is a pointer type, is expanded using nested for-loops as follows:

```
{
    T[, ...] a = x;
    V v;
    for (int i0 = a.GetLowerBound(0); i0 <= a.GetUpperBound(0); i0++)
    for (int i1 = a.GetLowerBound(1); i1 <= a.GetUpperBound(1); i1++)
    for (int i_n = a.GetLowerBound(n); i_n <= a.GetUpperBound(n); i_n++) {
        v = (V)a.GetValue(i0,i1,...,i_n);
        embedded-statement
    }
}
```

The variables a, i0, i1, ... i_n are not visible to or accessible to x or the embedded-statement or any other source code of the program. The variable v is read-only in the embedded statement. If there is not an explicit conversion (§18.4) from T (the element type) to V, an error is produced and no further steps are taken. If x has the value null, a System.NullReferenceException is thrown at run-time.

# 18.5 Pointers in expressions

In an unsafe context, an expression may yield a result of a pointer type, but outside an unsafe context it is a compile-time error for an expression to be of a pointer type. In precise terms, outside an unsafe context a compile-time error occurs if any simple-name (§7.6.2), member-access (§7.6.4), invocation-expression (§7.6.5), or element-access (§7.6.6) is of a pointer type.

In an unsafe context, the primary-no-array-creation-expression (§7.6) and unary-expression (§7.7) productions permit the following additional constructs:

```
primary-no-array-creation-expression:
...
pointer-member-access
pointer-element-access
sizeof-expression

unary-expression:
...
pointer-indirection-expression
addressof-expression
```

These constructs are described in the following sections. The precedence and associativity of the unsafe operators is implied by the grammar.