# 12.8.12 Null Conditional Element Access

A null_conditional_element_access consists of a primary_no_array_creation_expression followed by the two tokens "?" and "[", followed by an argument_list, followed by a "]" token, followed by zero or more dependent_accesses.

```
null_conditional_element_access
    : primary_no_array_creation_expression '?' '[' argument_list ']'
      dependent_access*
    ;
```

A null_conditional_element_access is a conditional version of element_access (§12.8.11) and it is a binding time error if the result type is void. For a null conditional expression where the result type may be void see (§12.8.10).

A null_conditional_element_access expression E is of the form P?[A]B; where B are the dependent_accesses, if any. The meaning of E is determined as follows:

+   - If the type of P is a nullable value type:
+     Let T be the type of the expression P.Value[A]B.
+     - If T is a type parameter that is not known to be either a reference type or a non-nullable value type, a compile-time error occurs.
+     - If T is a non-nullable value type, then the type of E is T?, and the meaning of E is the same as the meaning of:
+       ((object)P == null) ? (?T)null : P.Value[A]B
+       Except that P is evaluated only once.
+     - Otherwise the type of E is T, and the meaning of E is the same as the meaning of:
+       ((object)P == null) ? null : P.Value[A]B
+       Except that P is evaluated only once.
+   - Otherwise:
+     Let T be the type of the expression P[A]B.
+     - If T is a type parameter that is not known to be either a reference type or a non-nullable value type, a compile-time error occurs.
+     - If T is a non-nullable value type, then the type of E is T?, and the meaning of E is the same as the meaning of:
+       ((object)P == null) ? (?T)null : P[A]B
+       Except that P is evaluated only once.
+     - Otherwise the type of E is T, and the meaning of E is the same as the meaning of:
+       ((object)P == null) ? null : P[A]B
+       Except that P is evaluated only once.

Note: In an expression of the form:
P?[A₀]?[A₁]
if P evaluates to null neither A₀ or A₁ are evaluated. The same is true if an expression is a sequence of null_conditional_element_access or null_conditional_member_access §12.8.8 operations.