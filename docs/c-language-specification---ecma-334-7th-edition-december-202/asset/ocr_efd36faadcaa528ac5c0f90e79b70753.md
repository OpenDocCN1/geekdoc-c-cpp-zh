+   - If T is an enum_type, the base types of T are the class types System.Enum, System.ValueType, and object.
+   - If T is a struct_type, the base types of T are the class types System.ValueType and object. Note: A nullable_value_type is a struct_type (§8.3.1). end note
+   - If T is a class_type, the base types of T are the base classes of T, including the class type object.
+   - If T is an interface_type, the base types of T are the base interfaces of T and the class type object.
+   - If T is an array_type, the base types of T are the class types System.Array and object.
+   - If T is a delegate_type, the base types of T are the class types System.Delegate and object.

# 12.6 Function members

# 12.6.1 General

Function members are members that contain executable statements. Function members are always members of types and cannot be members of namespaces. C# defines the following categories of function members:

+   - Methods
+   - Properties
+   - Events
+   - Indexers
+   - User-defined operators
+   - Instance constructors
+   - Static constructors
+   - Finalizers

Except for finalizers and static constructors (which cannot be invoked explicitly), the statements contained in function members are executed through function member invocations. The actual syntax for writing a function member invocation depends on the particular function member category.

The argument list (§12.6.2) of a function member invocation provides actual values or variable references for the parameters of the function member.

Invocations of generic methods may employ type inference to determine the set of type arguments to pass to the method. This process is described in §12.6.3.

Invocations of methods, indexers, operators, and instance constructors employ overload resolution to determine which of a candidate set of function members to invoke. This process is described in §12.6.4.

Once a particular function member has been identified at binding-time, possibly through overload resolution, the actual run-time process of invoking the function member is described in §12.6.6.

Note: The following table summarizes the processing that takes place in constructs involving the six categories of function members that can be explicitly invoked. In the table, e, x, y, and value indicate expressions classified as variables or values, T indicates an expression classified as a type, F is the simple name of a method, and P is the simple name of a property.