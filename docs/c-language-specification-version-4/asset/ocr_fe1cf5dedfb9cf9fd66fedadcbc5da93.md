D. G takes precedence over C. G, and E. F takes precedence over both D. F and C. F.

# 7.6.5.3 Delegate invocations

For a delegate invocation, the primary-expression of the invocation-expression must be a value of a delegate-type. Furthermore, considering the delegate-type to be a function member with the same parameter list as the delegate-type, the delegate-type must be applicable (§7.5.3.1) with respect to the argument-list of the invocation-expression.

The run-time processing of a delegate invocation of the form D(A), where D is a primary-expression of a delegate-type and A is an optional argument-list, consists of the following steps:

+   - D is evaluated. If this evaluation causes an exception, no further steps are executed.
+   - The value of D is checked to be valid. If the value of D is null, a System.NullReferenceException is thrown and no further steps are executed.
+   - Otherwise, D is a reference to a delegate instance. Function member invocations (§7.5.4) are performed on each of the callable entities in the invocation list of the delegate. For callable entities consisting of an instance and instance method, the instance for the invocation is the instance contained in the callable entity.

# 7.6.6 Element access

An element-access consists of a primary-no-array-creation-expression, followed by a “[” token, followed by an argument-list, followed by a “]” token. The argument-list consists of one or more arguments, separated by commas.

```
element-access:
    primary-no-array-creation-expression [ argument-list ]
```

The argument-list of an element-access is not allowed to contain ref or out arguments.

An element-access is dynamically bound (§7.2.2) if at least one of the following holds:

+   - The primary-no-array-creation-expression has compile-time type dynamic.
+   - At least one expression of the argument-list has compile-time type dynamic and the primary-no-array-creation-expression does not have an array type.