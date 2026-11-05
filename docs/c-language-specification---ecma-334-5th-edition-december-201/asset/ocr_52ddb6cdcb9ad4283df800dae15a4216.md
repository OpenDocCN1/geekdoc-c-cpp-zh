parameter with a constructor-constraint. [Note: The System.Nullable<T> type specifies the non-nullable value type constraint for T. Thus, recursively constructed types of the forms T?? and Nullable<Nullable<T>> are prohibited. end note]

Pointer types are never allowed to be type arguments and are not considered to satisfy either the reference type or value type constraints.

If a constraint is a class type, an interface type, or a type parameter, that type specifies a minimal “base type” that every type argument used for that type parameter shall support. Whenever a constructed type or generic method is used, the type argument is checked against the constraints on the type parameter at compile-time. The type argument supplied shall satisfy the conditions described in §9.4.5.

A class-type constraint shall satisfy the following rules:

+   - The type shall be a class type.
+   - The type shall not be sealed.
+   - The type shall not be one of the following types: System.Array, System.Delegate, System.Enum, or System.ValueType.
+   - The type shall not be object.
+   - At most one constraint for a given type parameter may be a class type.

A type specified as an interface-type constraint shall satisfy the following rules:

+   - The type shall be an interface type.
+   - A type shall not be specified more than once in a given where clause.

In either case, the constraint may involve any of the type parameters of the associated type or method declaration as part of a constructed type, and may involve the type being declared.

Any class or interface type specified as a type parameter constraint shall be at least as accessible (§8.5.5) as the generic type or method being declared.

A type specified as a type-parameter constraint shall satisfy the following rules:

+   - The type shall be a type parameter.
+   - A type shall not be specified more than once in a given where clause.

In addition there shall be no cycles in the dependency graph of type parameters, where dependency is a transitive relation defined by:

+   - If a type parameter T is used as a constraint for type parameter S then S depends on T.
+   - If a type parameter S depends on a type parameter T and T depends on a type parameter U then S depends on U.

Given this relation, it is a compile-time error for a type parameter to depend on itself (directly or indirectly).

Any constraints shall be consistent among dependent type parameters. If type parameter S depends on type parameter T then:

+   - T shall not have the value type constraint. Otherwise, T is effectively sealed so S would be forced to be the same type as T, eliminating the need for two type parameters.
+   - If S has the value type constraint then T shall not have a class-type constraint.
+   - If S has a class-type constraint A and T has a class-type constraint B then there shall be an identity conversion or implicit reference conversion from A to B or an implicit reference conversion from B to A.