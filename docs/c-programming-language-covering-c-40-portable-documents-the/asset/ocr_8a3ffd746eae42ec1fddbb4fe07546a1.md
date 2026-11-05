+   * The best indexer of the set of candidate indexers is identified using the overload resolution rules of §7.5.3. If a single best indexer cannot be identified, the indexer access is ambiguous, and a binding-time error occurs.
+   * The index expressions of the argument-list are evaluated in order, from left to right. The result of processing the indexer access is an expression classified as an indexer access. The indexer access expression references the indexer determined in the step above, and has an associated instance expression of P and an associated argument list of A.

Depending on the context in which it is used, an indexer access causes invocation of either the get-accessor or the set-accessor of the indexer. If the indexer access is the target of an assignment, the set-accessor is invoked to assign a new value (§7.17.1). In all other cases, the get-accessor is invoked to obtain the current value (§7.1.1).

> **VLADIMIR RESHETNIKOV** If the corresponding accessor is missing or is not accessible, a compile-time error occurs.

# 7.6.7 this Access

A this-access consists of the reserved word this.

```
```
this-access:
    this
```
```

A this-access is permitted only in the block of an instance constructor, an instance method, or an instance accessor. It has one of the following meanings:

+   * When this is used in a primary-expression within an instance constructor of a class, it is classified as a value. The type of the value is the instance type (§10.3.1) of the class within which the usage occurs, and the value is a reference to the object being constructed.
+   * When this is used in a primary-expression within an instance method or instance accessor of a class, it is classified as a value. The type of the value is the instance type (§10.3.1) of the class within which the usage occurs, and the value is a reference to the object for which the method or accessor was invoked.
+   * When this is used in a primary-expression within an instance constructor of a struct, it is classified as a variable. The type of the variable is the instance type (§10.3.1) of the struct within which the usage occurs, and the variable represents the struct being constructed. The this variable of an instance constructor of a struct behaves exactly the same as an out parameter of the struct type—in particular, this means that the variable must be definitely assigned in every execution path of the instance constructor.