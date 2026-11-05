For member lookups in types other than type parameters and interfaces, and member lookups in interfaces that are strictly single-inheritance (each interface in the inheritance chain has exactly zero or one direct base interface), the effect of the lookup rules is simply that derived members hide base members with the same name or signature. Such single-inheritance lookups are never ambiguous. The ambiguities that can possibly arise from member lookups in multiple-inheritance interfaces are described in §13.2.5.

# 7.4.1 Base types

For purposes of member lookup, a type T is considered to have the following base types:

+   - If T is object, then T has no base type.
+   - If T is an enum-type, the base types of T are the class types System.Enum, System.ValueType, and object.
+   - If T is a struct-type, the base types of T are the class types System.ValueType and object.
+   - If T is a class-type, the base types of T are the base classes of T, including the class type object.
+   - If T is an interface-type, the base types of T are the base interfaces of T and the class type object.
+   - If T is an array-type, the base types of T are the class types System.Array and object.
+   - If T is a delegate-type, the base types of T are the class types System.Delegate and object.

# 7.5 Function members

Function members are members that contain executable statements. Function members are always members of types and cannot be members of namespaces. C# defines the following categories of function members:

+   - Methods
+   - Properties
+   - Events
+   - Indexers
+   - User-defined operators
+   - Instance constructors
+   - Static constructors
+   - Destructors

Except for destructors and static constructors (which cannot be invoked explicitly), the statements contained in function members are executed through function member invocations. The actual syntax for writing a function member invocation depends on the particular function member category.

The argument list (§7.5.1) of a function member invocation provides actual values or variable references for the parameters of the function member.

Invocations of generic methods may employ type inference to determine the set of type arguments to pass to the method. This process is described in §7.5.2.

Invocations of methods, indexers, operators and instance constructors employ overload resolution to determine which of a candidate set of function members to invoke. This process is described in §7.5.3.

Once a particular function member has been identified at binding-time, possibly through overload resolution, the actual run-time process of invoking the function member is described in §7.5.4.