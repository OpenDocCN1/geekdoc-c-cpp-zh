At run-time, all of the code within a generic type declaration is executed in the context of a closed constructed type that was created by applying type arguments to the generic declaration. Each type parameter within the generic type is bound to a particular run-time type. The run-time processing of all statements and expressions always occurs with closed types, and open types occur only during compile-time processing.

Each closed constructed type has its own set of static variables, which are not shared with any other closed constructed types. Since an open type does not exist at run-time, there are no static variables associated with an open type. Two closed constructed types are the same type if they are constructed from the same unbound generic type, and their corresponding type arguments are the same type.

# 8.4.4 Bound and unbound types

The term unbound type refers to a non-generic type or an unbound generic type. The term bound type refers to a non-generic type or a constructed type.

An unbound type refers to the entity declared by a type declaration. An unbound generic type is not itself a type, and cannot be used as the type of a variable, argument or return value, or as a base type. The only construct in which an unbound generic type can be referenced is the typeof expression (§11.7.16).

# 8.4.5 Satisfying constraints

Whenever a constructed type or generic method is referenced, the supplied type arguments are checked against the type parameter constraints declared on the generic type or method (§14.2.5). For each where clause, the type argument A that corresponds to the named type parameter is checked against each constraint as follows:

+   - If the constraint is a class type, an interface type, or a type parameter, let C represent that constraint with the supplied type arguments substituted for any type parameters that appear in the constraint. To satisfy the constraint, it shall be the case that type A is convertible to type C by one of the following:
+     - An identity conversion (§10.2.2)
+     - An implicit reference conversion (§10.2.8)
+     - A boxing conversion (§10.2.9), provided that type A is a non-nullable value type.
+     - An implicit reference, boxing or type parameter conversion from a type parameter A to C.
+   - If the constraint is the reference type constraint (class), the type A shall satisfy one of the following:
+     - A is an interface type, class type, delegate type, array type or the dynamic type.
+       Note: System.ValueType and System.Enum are reference types that satisfy this constraint. end note
+     - A is a type parameter that is known to be a reference type (§8.2).
+   - If the constraint is the value type constraint (struct), the type A shall satisfy one of the following:
+     - A is a struct type or enum type, but not a nullable value type.
+       Note: System.ValueType and System.Enum are reference types that do not satisfy this constraint. end note
+     - A is a type parameter having the value type constraint (§14.2.5).
+   - If the constraint is the constructor constraint new(), the type A shall not be abstract and shall have a public parameterless constructor. This is satisfied if one of the following is true: