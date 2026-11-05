```
invocation_expression
  : primary_expression '(' argument_list? ')'
  ;
```

An *invocation_expression* is dynamically bound (§11.3.3) if at least one of the following holds:

+   - The *primary_expression* has compile-time type `dynamic`.
+   - At least one argument of the optional *argument_list* has compile-time type `dynamic`.

In this case, the compiler classifies the *invocation_expression* as a value of type `dynamic`. The rules below to determine the meaning of the *invocation_expression* are then applied at run-time, using the run-time type instead of the compile-time type of those of the *primary_expression* and arguments that have the compile-time type `dynamic`. If the *primary_expression* does not have compile-time type `dynamic`, then the method invocation undergoes a limited compile-time check as described in §11.6.5.

The *primary_expression* of an *invocation_expression* shall be a method group or a value of a *delegate_type*. If the *primary_expression* is a method group, the *invocation_expression* is a method invocation (§11.7.8.2). If the *primary_expression* is a value of a *delegate_type*, the *invocation_expression* is a delegate invocation (§11.7.8.4). If the *primary_expression* is neither a method group nor a value of a *delegate_type*, a binding-time error occurs.

The optional *argument_list* (§11.6.2) provides values or variable references for the parameters of the method.

The result of evaluating an *invocation_expression* is classified as follows:

+   - If the *invocation_expression* invokes a method or delegate that returns void, the result is nothing. An expression that is classified as nothing is permitted only in the context of a *statement_expression* (§12.7) or as the body of a *lambda_expression* (§11.16). Otherwise a binding-time error occurs.
+   - Otherwise, the result is a value, with an associated type of the return type of the method or delegate after any type argument substitutions (§11.7.8.2) have been performed. If the invocation is of an instance method, and the receiver is of a class type T, the associated type is picked from the first declaration or override of the method found when starting with T and searching through its base classes.

# 11.7.8.2 Method invocations

For a method invocation, the *primary_expression* of the *invocation_expression* shall be a method group. The method group identifies the one method to invoke or the set of overloaded methods from which to choose a specific method to invoke. In the latter case, determination of the specific method to invoke is based on the context provided by the types of the arguments in the *argument_list*.

The binding-time processing of a method invocation of the form M(A), where M is a method group (possibly including a *type_argument_list*), and A is an optional *argument_list*, consists of the following steps:

+   - The set of candidate methods for the method invocation is constructed. For each method F associated with the method group M:
+     - If F is non-generic, F is a candidate when:
+       - M has no type argument list, and
+       - F is applicable with respect to A (§11.6.4.2).
+     - If F is generic and M has no type argument list, F is a candidate when: