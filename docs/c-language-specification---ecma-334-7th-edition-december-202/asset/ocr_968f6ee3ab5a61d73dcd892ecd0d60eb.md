Given a pattern input value (§11.1) e, if the simple_designation is the identifier _, it denotes a discard (§9.2.9.1) and the value of e is not bound to anything. (Although a declared variable with the name _ may be in scope at that point, that named variable is not seen in this context.) If simple_designation is any other identifier, a local variable (§9.2.9) of the given type named by the given identifier is introduced. That local variable is assigned the value of the pattern input value when the pattern matches the value.

Certain combinations of static type of the pattern input value and the given type are considered incompatible and result in a compile-time error. A value of static type E is said to be pattern compatible with the type T if there exists an identity conversion, an implicit or explicit reference conversion, a boxing conversion, or an unboxing conversion from E to T, or if either E or T is an open type (§8.4.3). A declaration pattern naming a type T is applicable to every type E for which E is pattern compatible with T.

Note: The support for open types can be most useful when checking types that may be either struct or class types, and boxing is to be avoided. endNoteExample: The declaration pattern is useful for performing run-time type tests of reference types, and replaces the idiom

```
var v = expr as Type;
if (v != null) { /* code using v */ }
```

with the slightly more concise

```
if (expr is Type v) { /* code using v */ }
```

end example

It is an error if type is a nullable value type.

Example: The declaration pattern can be used to test values of nullable types: a value of type Nullable<T> (or a boxed T) matches a type pattern T2 id if the value is non-null and T2 is T, or some base type or interface of T. For example, in the code fragment

```
int? x = 3;
if (x is int v) { /* code using v */ }
```

The condition of the if statement is true at runtime and the variable v holds the value 3 of type int inside the block. end example

# 11.2.3 Constant pattern

A constant_pattern is used to test the value of a pattern input value (§11.1) against the given constant value.

```
constant_pattern
  : constant_expression
  ;
```

A constant pattern P is applicable to a type T if there is an implicit conversion from the constant expression of P to the type T.

For a constant pattern P, its converted value is

+   - if the pattern input value's type is an integral type or an enum type, the pattern's constant value converted to that type; otherwise
+   - if the pattern input value's type is the nullable version of an integral type or an enum type, the pattern's constant value converted to its underlying type; otherwise
+   - the value of the pattern's constant value.

Given a pattern input value e and a constant pattern P with converted value v,