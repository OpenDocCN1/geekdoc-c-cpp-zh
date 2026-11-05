> Note: Delegate creation expressions do not always create new instances. When the expression is processed in the same way as a method group conversion (§10.8) or an anonymous function conversion (§10.7) this may result in an existing delegate instance being reused. end note

# 12.8.16.2 Object creation expressions

An object_creation_expression is used to create a new instance of a class_type or a value_type.

```
object_creation_expression
  : 'new' type '(' argument_list? ')' object_or_collection_initializer?
  | 'new' type object_or_collection_initializer
  ;

object_or_collection_initializer
  : object_initializer
  | collection_initializer
  ;
```

The type of an object_creation_expression shall be a class_type, a value_type, or a type_parameter. The type cannot be a tuple_type or an abstract or static class_type.

The optional argument_list (§12.6.2) is permitted only if the type is a class_type or a struct_type.

An object creation expression can omit the constructor argument list and enclosing parentheses provided it includes an object initializer or collection initializer. Omitting the constructor argument list and enclosing parentheses is equivalent to specifying an empty argument list.

Processing of an object creation expression that includes an object initializer or collection initializer consists of first processing the instance constructor and then processing the member or element initializations specified by the object initializer (§12.8.16.3) or collection initializer (§12.8.16.4).

If any of the arguments in the optional argument_list has the compile-time type dynamic then the object_creation_expression is dynamically bound (§12.3.3) and the following rules are applied at run-time using the run-time type of those arguments of the argument_list that have the compile-time type dynamic. However, the object creation undergoes a limited compile-time check as described in §12.6.5.

The binding-time processing of an object_creation_expression of the form new T(A), where T is a class_type, or a value_type, and A is an optional argument_list, consists of the following steps:

+   - If T is a value_type and A is not present:
+     - The object_creation_expression is a default constructor invocation. The result of the object_creation_expression is a value of type T, namely the default value for T as defined in §8.3.3.
+   - Otherwise, if T is a type_parameter and A is not present:
+     - If no value type constraint or constructor constraint (§15.2.5) has been specified for T, a binding-time error occurs.
+     - The result of the object_creation_expression is a value of the run-time type that the type parameter has been bound to, namely the result of invoking the default constructor of that type. The run-time type may be a reference type or a value type.
+   - Otherwise, if T is a class_type or a struct_type:
+     - If T is an abstract or static class_type, a compile-time error occurs.
+     - The instance constructor to invoke is determined using the overload resolution rules of §12.6.4. The set of candidate instance constructors consists of all accessible instance constructors