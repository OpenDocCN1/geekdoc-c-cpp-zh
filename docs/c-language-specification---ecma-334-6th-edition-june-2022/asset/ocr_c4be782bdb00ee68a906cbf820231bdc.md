# 11.7.7 Null Conditional Member Access

A *null_conditional_member_access* is a conditional version of *member_access* (§11.7.6) and it is a binding time error if the result type is *void*. For a null conditional expression where the result type may be *void* see (§11.7.9).

A *null_conditional_member_access* consists of a *primary_expression* followed by the two tokens "?" and ".", followed by an *identifier* with an optional *type_argument_list*, followed by zero or more *dependent_accesses*.

```
null_conditional_member_access
: primary_expression '?' '.' identifier type_argument_list? dependent_access*
;

dependent_access
: '.' identifier type_argument_list?    // member access
| '[' argument_list ']'    // element access
| '(' argument_list? ')'    // invocation
;

null_conditional_projection_initializer
: primary_expression '?' '.' identifier type_argument_list?
;
```

A *null_conditional_member_access* expression E is of the form P ?. A. Let T be the type of the expression P. A. The meaning of E is determined as follows:

+   - If T is a type parameter that is not known to be a reference type or a non-nullable value type, a compile-time error occurs.
+   - If T is a non-nullable value type, then the type of E is T?, and the meaning of E is the same as the meaning of:
+   
+     `((object)P == null) ? (T?)null : P.A`
+   
+     Except that P is evaluated only once.
+   - Otherwise the type of E is T, and the meaning of E is the same as the meaning of:
+   
+     `((object)P == null) ? null : P.A`
+   
+     Except that P is evaluated only once.

*Note:* In an expression of the form:

P ?. A₀ ?. A₁

then if P evaluates to *null* neither A₀ or A₁ are evaluated. The same is true if an expression is a sequence of *null_conditional_member_access* or *null_conditional_element_access* §11.7.11 operations.
*end note*

A *null_conditional_projection_initializer* is a restriction of *null_conditional_member_access* and has the same semantics. It only occurs as a projection initializer in an anonymous object creation expression (§11.7.15.7).

# 11.7.8 Invocation expressions

# 11.7.8.1 General

An *invocation_expression* is used to invoke a method.