+   - The saved value of x becomes the result of the operation.

The ++ and -- operators also support prefix notation (§7.7.5). Typically, the result of x++ or x-- is the value of x before the operation, whereas the result of ++x or --x is the value of x after the operation. In either case, x itself has the same value after the operation.

An operator ++ or operator -- implementation can be invoked using either postfix or prefix notation. It is not possible to have separate operator implementations for the two notations.

# 7.6.10 The new operator

The new operator is used to create new instances of types.

There are three forms of new expressions:

+   - Object creation expressions are used to create new instances of class types and value types.
+   - Array creation expressions are used to create new instances of array types.
+   - Delegate creation expressions are used to create new instances of delegate types.

The new operator implies creation of an instance of a type, but does not necessarily imply dynamic allocation of memory. In particular, instances of value types require no additional memory beyond the variables in which they reside, and no dynamic allocations occur when new is used to create instances of value types.

# 7.6.10.1 Object creation expressions

An object-creation-expression is used to create a new instance of a class-type or a value-type.

```
object-creation-expression:
    new type ( argument-list_opt ) object-or-collection-initializer_opt
    new type object-or-collection-initializer

object-or-collection-initializer:
    object-initializer
    collection-initializer
```

The type of an object-creation-expression must be a class-type, a value-type or a type-parameter. The type cannot be an abstract class-type.

The optional argument-list (§7.5.1) is permitted only if the type is a class-type or a struct-type.

An object creation expression can omit the constructor argument list and enclosing parentheses provided it includes an object initializer or collection initializer. Omitting the constructor argument list and enclosing parentheses is equivalent to specifying an empty argument list.

Processing of an object creation expression that includes an object initializer or collection initializer consists of first processing the instance constructor and then processing the member or element initializations specified by the object initializer (§7.6.10.2) or collection initializer (§7.6.10.3).

If any of the arguments in the optional argument-list has the compile-time type dynamic then the object-creation-expression is dynamically bound (§7.2.2) and the following rules are applied at run-time using the run-time type of those arguments of the argument-list that have the compile time type dynamic. However, the object creation undergoes a limited compile time check as described in §7.5.4.

The binding-time processing of an object-creation-expression of the form new T(A), where T is a class-type or a value-type and A is an optional argument-list, consists of the following steps:

+   - If T is a value-type and A is not present: