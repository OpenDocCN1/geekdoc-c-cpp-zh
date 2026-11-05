In this example, all four tuple expressions are valid. The first two, t1 and t2, do not use the type of the tuple expression, but instead apply an implicit tuple conversion. In the case of t2, the implicit tuple conversion relies on the implicit conversions from 2 to long and from null to string. The third tuple expression has a type (int i, string), and can therefore be reclassified as a value of that type. The declaration of t4, on the other hand, is an error: The tuple expression has no type because its second element has no type.

```
if ((x, y).Equals((1, 2))) { ... };
```

This example shows that tuples can sometimes lead to multiple layers of parentheses, especially when the tuple expression is the sole argument to a method invocation.

*end example*

# 12.8.7 Member access

# 12.8.7.1 General

*A member_access consists of a primary_expression, a predefined_type, or a qualified_alias_member, followed by a '.' token, followed by an identifier, optionally followed by a type_argument_list.*

```
member_access
: primary_expression '.' identifier type_argument_list?
| predefined_type '.' identifier type_argument_list?
| qualified_alias_member '.' identifier type_argument_list?
;
```

```
predefined_type
: 'bool' | 'byte' | 'char' | 'decimal' | 'double' | 'float' | 'int'
| 'long' | 'object' | 'sbyte' | 'short' | 'string' | 'uint' | 'ulong'
| 'ushort'
;
```

The qualified_alias_member production is defined in §14.8.

*A member_access is either of the form E . I or of the form E . I <A1, ..., An>, where E is a primary_expression, predefined_type or qualified_alias_member, I is a single identifier, and <A1, ..., An> is an optional type_argument_list. When no type_argument_list is specified, consider e to be zero.*

A member_access with a primary_expression of type dynamic is dynamically bound (§12.3.3). In this case, the compiler classifies the member access as a property access of type dynamic. The rules below to determine the meaning of the member_access are then applied at run-time, using the run-time type instead of the compile-time type of the primary_expression. If this run-time classification leads to a method group, then the member access shall be the primary_expression of an invocation_expression.

The member_access is evaluated and classified as follows:

+   - If E is zero and E is a namespace and E contains a nested namespace with name I, then the result is that namespace.
+   - Otherwise, if E is a namespace and E contains an accessible type having name I and K type parameters, then the result is that type constructed with the given type arguments.
+   - If E is classified as a type, if E is not a type parameter, and if a member lookup (§12.5) of I in E with K type parameters produces a match, then E . I is evaluated and classified as follows:
+     Note: When the result of such a member lookup is a method group and K is zero, the method group