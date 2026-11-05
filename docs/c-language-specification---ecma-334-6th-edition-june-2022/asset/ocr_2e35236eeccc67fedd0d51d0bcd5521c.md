+   - If M is a constant, field, property, event, enumeration member, or type declaration, then all members declared in an interface declaration are removed from the set.
+   - If M is a method, then all non-method members declared in an interface declaration are removed from the set, and all methods with the same signature as M declared in an interface declaration are removed from the set.
+   - Finally, having removed hidden members, the result of the lookup is determined:
+     - If the set consists of a single member that is not a method, then this member is the result of the lookup.
+     - Otherwise, if the set contains only methods, then this group of methods is the result of the lookup.
+     - Otherwise, the lookup is ambiguous, and a binding-time error occurs.

For member lookups in types other than type parameters and interfaces, and member lookups in interfaces that are strictly single-inheritance (each interface in the inheritance chain has exactly zero or one direct base interface), the effect of the lookup rules is simply that derived members hide base members with the same name or signature. Such single-inheritance lookups are never ambiguous. The ambiguities that can possibly arise from member lookups in multiple-inheritance interfaces are described in §17.4.6.

> Note: This phase only accounts for one kind of ambiguity. If the member lookup results in a method group, further uses of method group may fail due to ambiguity, for example as described in §11.6.4.1 and §11.6.2. end note

# 11.5.2 Base types

For purposes of member lookup, a type T is considered to have the following base types:

+   - If T is object or dynamic, then T has no base type.
+   - If T is an enum_type, the base types of T are the class types System.Enum, System.ValueType, and object.
+   - If T is a struct_type, the base types of T are the class types System.ValueType and object. Note: A nullable_value_type is a struct_type (§8.3.1). end note
+   - If T is a class_type, the base types of T are the base classes of T, including the class type object.
+   - If T is an interface_type, the base types of T are the base interfaces of T and the class type object.
+   - If T is an array_type, the base types of T are the class types System.Array and object.
+   - If T is a delegate_type, the base types of T are the class types System.Delegate and object.

# 11.6 Function members

# 11.6.1 General

Function members are members that contain executable statements. Function members are always members of types and cannot be members of namespaces. C# defines the following categories of function members:

+   - Methods