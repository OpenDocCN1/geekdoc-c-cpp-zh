+   - If `T` is a type parameter that is not known to be a reference type or a non-nullable value type, a compile-time error occurs.
+   - If `T` is a non-nullable value type, then the type of `E` is `T?`, and the meaning of `E` is the same as the meaning of:
+     `((object)P == null) ? (T?)null : P[A]B`
+     Except that `P` is evaluated only once.
+   - Otherwise the type of `E` is `T`, and the meaning of `E` is the same as the meaning of:
+     `((object)P == null) ? null : P[A]B`
+     Except that `P` is evaluated only once.

Note: In an expression of the form:
P?[A0]?[A1]
if P evaluates to null neither A0 nor A1 are evaluated. The same is true if an expression is a sequence of null_conditional_element_access or null_conditional_member_access §11.7.7 operations.
end note

# 11.7.12 This access

A this_access consists of the keyword this.

```
this_access
: 'this'
;
```

A this_access is permitted only in the block of an instance constructor, an instance method, an instance accessor (§11.2.1), or a finalizer. It has one of the following meanings:

+   - When this is used in a primary_expression within an instance constructor of a class, it is classified as a value. The type of the value is the instance type (§14.3.2) of the class within which the usage occurs, and the value is a reference to the object being constructed.
+   - When this is used in a primary_expression within an instance method or instance accessor of a class, it is classified as a value. The type of the value is the instance type (§14.3.2) of the class within which the usage occurs, and the value is a reference to the object for which the method or accessor was invoked.
+   - When this is used in a primary_expression within an instance constructor of a struct, it is classified as a variable. The type of the variable is the instance type (§14.3.2) of the struct within which the usage occurs, and the variable represents the struct being constructed.
+     - If the constructor declaration has no constructor initializer, the this variable behaves exactly the same as an out parameter of the struct type. In particular, this means that the variable shall be definitely assigned in every execution path of the instance constructor.
+     - Otherwise, the this variable behaves exactly the same as a ref parameter of the struct type. In particular, this means that the variable is considered initially assigned.
+   - When this is used in a primary_expression within an instance method or instance accessor of a struct, it is classified as a variable. The type of the variable is the instance type (§14.3.2) of the struct within which the usage occurs.