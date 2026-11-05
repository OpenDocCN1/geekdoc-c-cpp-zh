+   - Otherwise, if A exists and an implicit conversion exists from b to A, the result type is A. At run-time, a is first evaluated. If a is not null, a becomes the result. Otherwise, b is evaluated and converted to type A, and this becomes the result.
+   - Otherwise, if A exists and is a nullable value type, b has a type B and an implicit conversion exists from A₀ to B, the result type is B. At run-time, a is first evaluated. If a is not null, a is unwrapped to type A₀ and converted to type B, and this becomes the result. Otherwise, b is evaluated and becomes the result.
+   - Otherwise, if b has a type B and an implicit conversion exists from a to B, the result type is B. At run-time, a is first evaluated. If a is not null, a is converted to type B, and this becomes the result. Otherwise, b is evaluated and becomes the result.

Otherwise, a and b are incompatible, and a compile-time error occurs.

# 11.15 Conditional operator

The ?: operator is called the conditional operator. It is at times also called the ternary operator.

```
conditional_expression
    : null_coalescing_expression
    | null_coalescing_expression '?' expression ':' expression
    ;
```

A conditional expression of the form b ? x : y first evaluates the condition b. Then, if b is true, x is evaluated and becomes the result of the operation. Otherwise, y is evaluated and becomes the result of the operation. A conditional expression never evaluates both x and y.

The conditional operator is right-associative, meaning that operations are grouped from right to left.

Example: An expression of the form a ? b : c ? d : e is evaluated as a ? b : (c ? d : e). end example

The first operand of the ?: operator shall be an expression that can be implicitly converted to bool, or an expression of a type that implements operator true. If neither of these requirements is satisfied, a compile-time error occurs.

The second and third operands, x and y, of the ?: operator control the type of the conditional expression.

+   - If x has type X and y has type Y, then
+     - If X and Y are the same type, then this is the type of the conditional expression.
+     - Otherwise, if an implicit conversion (§10.2) exists from X to Y, but not from Y to X, then Y is the type of the conditional expression.
+     - Otherwise, if an implicit enumeration conversion (§10.2.4) exists from X to Y, then Y is the type of the conditional expression.
+     - Otherwise, if an implicit enumeration conversion (§10.2.4) exists from Y to X, then X is the type of the conditional expression.
+     - Otherwise, if an implicit conversion (§10.2) exists from Y to X, but not from X to Y, then X is the type of the conditional expression.
+     - Otherwise, no expression type can be determined, and a compile-time error occurs.
+   - If only one of x and y has a type, and both x and y are implicitly convertible to that type, then that is the type of the conditional expression.