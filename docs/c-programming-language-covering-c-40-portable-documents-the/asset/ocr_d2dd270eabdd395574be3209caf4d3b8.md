- The type must not be one of the following types: System.Array, System.Delegate, System.Enum, or System.ValueType.

> > **JON SKEET** I know of no reason to prohibit System.Enum or System.Delegate as the type here—although it would certainly be more friendly to be able to write "where T : enum" than "where T : struct, Enum", which would be the most common use. Although C# is specified separately from the CLI, you might suspect that this is a CLI limitation—but it's not. Indeed, ECMA-335 explicitly lists this and other constraints that are prohibited in C#. Perhaps this restriction will be removed from a future version of the language; there are plenty of situations where it would be useful.

- The type must not be object. Because all types derive from object, such a constraint would have no effect if it were permitted.
- At most one constraint for a given type parameter can be a class type.

A type specified as an interface-type constraint must satisfy the following rules:

- The type must be an interface type.
- A type must not be specified more than once in a given where clause.

In either case, the constraint can involve any of the type parameters of the associated type or method declaration as part of a constructed type, and can involve the type being declared.

Any class or interface type specified as a type parameter constraint must be at least as accessible (§3.5.4) as the generic type or method being declared.

A type specified as a type-parameter constraint must satisfy the following rules:
- The type must be a type parameter.
- A type must not be specified more than once in a given where clause.
In addition, there must be no cycles in the dependency graph of type parameters, where dependency is a transitive relation defined as follows:
- If a type parameter T is used as a constraint for type parameter S, then S depends on T.
- If a type parameter S depends on a type parameter T and T depends on a type parameter U, then S depends on U.
Given this relation, it is a compile-time error for a type parameter to depend on itself (directly or indirectly).