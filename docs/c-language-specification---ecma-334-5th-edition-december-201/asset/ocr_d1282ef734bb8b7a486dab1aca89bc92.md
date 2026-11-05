the usage occurs, and the value is a reference to the object for which the method or accessor was invoked.

+   - When this is used in a primary-expression within an instance constructor of a struct, it is classified as a variable. The type of the variable is the instance type (§15.3.2) of the struct within which the usage occurs, and the variable represents the struct being constructed.
+     - If the constructor declaration has no constructor initializer, the this variable behaves exactly the same as an out parameter of the struct type. In particular, this means that the variable shall be definitely assigned in every execution path of the instance constructor.
+     - Otherwise, the this variable behaves exactly the same as a ref parameter of the struct type. In particular, this means that the variable is considered initially assigned.
+   - When this is used in a primary-expression within an instance method or instance accessor of a struct, it is classified as a variable. The type of the variable is the instance type (§15.3.2) of the struct within which the usage occurs.
+     - If the method or accessor is not an iterator (§15.14) or async function (§15.15), the this variable represents the struct for which the method or accessor was invoked, and behaves exactly the same as a ref parameter of the struct type.
+     - If the method or accessor is an iterator or async function, the this variable represents a copy of the struct for which the method or accessor was invoked, and behaves exactly the same as a value parameter of the struct type.

Use of this in a primary-expression in a context other than the ones listed above is a compile-time error. In particular, it is not possible to refer to this in a static method, a static property accessor, or in a variable-initializer of a field declaration.

# 12.7.9 Base access

A base-access consists of the keyword base followed by either a “.” token and an identifier and optional type-argument-list or an argument-list enclosed in square brackets:

```
base-access:
    base . identifier type-argument-list_opt
    base [ argument-list ]
```

A base-access is used to access base class members that are hidden by similarly named members in the current class or struct. A base-access is permitted only in the block of an instance constructor, an instance method, an instance accessor (§12.2.1), or a finalizer. When base . I occurs in a class or struct, I shall denote a member of the base class of that class or struct. Likewise, when base[E] occurs in a class, an applicable indexer shall exist in the base class.

At binding-time, base-access expressions of the form base . I and base[E] are evaluated exactly as if they were written ((B)this).I and ((B)this)[E], where B is the base class of the class or struct in which the construct occurs. Thus, base . I and base[E] correspond to this . I and this[E], except this is viewed as an instance of the base class.

When a base-access references a virtual function member (a method, property, or indexer), the determination of which function member to invoke at run-time (§12.6.6) is changed. The function member that is invoked is determined by finding the most derived implementation (§15.6.4) of the function member with respect to B (instead of with respect to the run-time type of this, as would be usual in a non-base access). Thus, within an override of a virtual function member, a base-access can be used to invoke the inherited implementation of the function member. If the function member referenced by a base-access is abstract, a binding-time error occurs.

> [Note: Unlike this, base is not an expression in itself. It is a keyword only used in the context of a base-access or a constructor-initializer (§15.11.2). end note]