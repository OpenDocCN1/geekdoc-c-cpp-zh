In unsafe contexts, expressions can result in point types but, if that happened outside of the unsafe context, you would get an error at compile time. So, if any of the following results in a pointer type outside an unsafe context, you would get the error:

+   - `simple_name`
+   - `member_access`
+   - `invocation_expression`
+   - `element_access`

The `primary_no_array_creation_expression` and `unary_expression` will allow these constructs in an unsafe context:

```
primary_no_array_creation_expression_unsafe
    : pointer_member_access
    | pointer_element_access
    | sizeof_expression
    ;
```

```
unary_expression_unsafe
    : pointer_indirection_expression
    | addressof_expression
    ;
```

We’ll discuss these constructs now; associativity and precedence of unsafe operators are implied in the grammar.

# Pointer Indirection

This expression is an asterisk (*) and a unary_expression:

```
pointer_indirection_expression
    : '*' unary_expression
    ;
```