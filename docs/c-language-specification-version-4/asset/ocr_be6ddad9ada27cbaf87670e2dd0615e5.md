+   - The value of E is checked to be valid. If the value of E is null, a System.NullReferenceException is thrown and no further steps are executed.
+   - The function member implementation to invoke is determined:
+     - If the binding-time type of E is an interface, the function member to invoke is the implementation of M provided by the run-time type of the instance referenced by E. This function member is determined by applying the interface mapping rules (§13.4.4) to determine the implementation of M provided by the run-time type of the instance referenced by E.
+     - Otherwise, if M is a virtual function member, the function member to invoke is the implementation of M provided by the run-time type of the instance referenced by E. This function member is determined by applying the rules for determining the most derived implementation (§10.6.3) of M with respect to the run-time type of the instance referenced by E.
+     - Otherwise, M is a non-virtual function member, and the function member to invoke is M itself.
+   - The function member implementation determined in the step above is invoked. The object referenced by E becomes the object referenced by this.

# 7.5.5.1 Invocations on boxed instances

A function member implemented in a value-type can be invoked through a boxed instance of that value-type in the following situations:

+   - When the function member is an override of a method inherited from type object and is invoked through an instance expression of type object.
+   - When the function member is an implementation of an interface function member and is invoked through an instance expression of an interface-type.
+   - When the function member is invoked through a delegate.

In these situations, the boxed instance is considered to contain a variable of the value-type, and this variable becomes the variable referenced by this within the function member invocation. In particular, this means that when a function member is invoked on a boxed instance, it is possible for the function member to modify the value contained in the boxed instance.

# 7.6 Primary expressions

Primary expressions include the simplest forms of expressions.

```
primary-expression:
  primary-no-array-creation-expression
  array-creation-expression
```