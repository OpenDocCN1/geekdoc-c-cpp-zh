
the base class declaration, the corresponding type-argument of the constructed type. Given the generic class declarations

```csharp
class B<U,V> { ... }
class G<T> : B<string,T[]> { ... }
```

the base class of the constructed type G<int> would be B<string,int[]>.

The direct base class of a class type must be at least as accessible as the class type itself (§3.5.2). For example, it is a compile-time error for a public class to derive from a private or internal class.

The direct base class of a class type must not be any of the following types: System.Array, System.Delegate, System.MulticastDelegate, System.Enum, or System.ValueType. Furthermore, a generic class declaration cannot use System.Attribute as a direct or indirect base class.

While determining the meaning of the direct base class specification A of a class B, the direct base class of B is temporarily assumed to be object. Intuitively, this ensures that the meaning of a base class specification cannot recursively depend on itself. The example

```csharp
class A<T> {
    public class B{}
}
class C : A<C,B> {}
```

is in error since in the base class specification A<C,B>, the direct base class of C is considered to be object; hence (by the rules of §3.8), C is not considered to have a member B.

The base classes of a class type are the direct base class and its base classes. In other words, the set of base classes is the transitive closure of the direct base class relationship. Referring to the example above, the base classes of B are A and object. In the example

```csharp
class A { ... }
class B<T> : A { ... }
class C<T> : B<IComparable<T>> { ... }
class D<T> : C<T[]> { ... }
```

the base classes of D<int> are C<int[]>, B<IComparable<int[]>>, A, and object.

Except for class object, every class type has exactly one direct base class. The object class has no direct base class and is the ultimate base class of all other classes.

When a class B derives from a class A, it is a compile-time error for A to depend on B. A class directly depends on its direct base class (if any) and directly depends on the class within which it is immediately nested (if any). Given this definition, the complete set of classes upon which a class depends is the reflexive and transitive closure of the *directly depends on relationship*.

> **VLADIMIR RESHETNIKOV** For the purposes of this rule, type arguments, if any, are ignored. For instance, although A<T> and A<A<T>> are different types, the following declaration is still invalid:
>
> ```csharp
> class A<T> : A<A<T>> { }
> ```
>
> Conversely, it is perfectly valid for a class to appear within a type argument for a constructed type specified as its base class:
>
> ```csharp
> class A<T> { }
> class B : A<B[]> { } // Okay
> ```

The example

```csharp
class A: A { }
```

is erroneous because the class depends on itself. Likewise, the example

```csharp
class A: B { }
class B: C { }
class C: A { }
```

is in error because the classes circularly depend on themselves. Finally, the example

```csharp
class A: B.C { }
class B: A
{
    public class C { }
}
```

results in a compile-time error because A depends on B.C (its direct base class), which depends on B (its immediately enclosing class), which circularly depends on A.

Note that a class does not depend on the classes that are nested within it. In the example

```csharp
class A
{
    class B: A { }
}
```

B depends on A (because A is both its direct base class and its immediately enclosing class), but A does not depend on B (because B is neither a base class nor an enclosing class of A). Thus the example is valid.

It is not possible to derive from a sealed class. In the example

```csharp
sealed class A {}
class B: A {}    // Error: cannot derive from a sealed class
```

class B is in error because it attempts to derive from the sealed class A.

## 10.1.4.2 Interface Implementations

A class-base specification may include a list of interface types, in which case the class is said to directly implement the given interface types. Interface implementations are discussed further in §13.4.

## 10.1.5 Type Parameter Constraints

Generic type and method declarations can optionally specify type parameter constraints by including type-parameter-constraints-clauses.

```text
type-parameter-constraints-clauses:
  type-parameter-constraints-clause
  type-parameter-constraints-clauses type-parameter-constraints-clause

type-parameter-constraints-clause:
  where type-parameter : type-parameter-constraints

type-parameter-constraints:
  primary-constraint
  secondary-constraints
  constructor-constraint
  primary-constraint , secondary-constraints
  primary-constraint , constructor-constraint
  secondary-constraints , constructor-constraint
  primary-constraint , secondary-constraints , constructor-constraint

primary-constraint:
  class-type
  class
  struct

secondary-constraints:
  interface-type
  type-parameter
  secondary-constraints , interface-type
  secondary-constraints , type-parameter

constructor-constraint:
  new ( )
```

Each type-parameter-constraints-clause consists of the token where, followed by the name of a type parameter, followed by a colon and the list of constraints for that type parameter. There can be at most one where clause for each type parameter, and the where clauses can be listed in any order. Like the get and set tokens in a property accessor, the where token is not a keyword.

The list of constraints given in a where clause can include any of the following components, in this order: a single primary constraint, one or more secondary constraints, and the constructor constraint, new().

A primary constraint can be a class type or the reference type constraint class or the value type constraint struct. A secondary constraint can be a type-parameter or interface-type.

The reference type constraint specifies that a type argument used for the type parameter must be a reference type. All class types, interface types, delegate types, array types, and type parameters known to be a reference type (as defined below) satisfy this constraint.

The value type constraint specifies that a type argument used for the type parameter must be a non-nullable value type. All non-nullable struct types, enum types, and type parameters having the value type constraint satisfy this constraint. Although it is classified as a value type, a nullable type (§4.1.10) does not satisfy the value type constraint. A type parameter having the value type constraint cannot also have the constructor-constraint.

> **BILL WAGNER** At one point, I found this set of constraints very limiting. I wanted to do meta-programming with generics, being able to specify any arbitrary set of members as constraints—things like other constructor signatures, or operators. Now that C# 3.0 has lambdas and more natural support for the use of methods as parameters, that feeling is gone. By specifying delegate signatures as type parameters, or as parameters to methods, C# programmers can achieve almost anything.

Pointer types are never allowed to be type arguments and are not considered to satisfy either the reference type or value type constraints.

If a constraint is a class type, an interface type, or a type parameter, that type specifies a minimal “base type” that every type argument used for that type parameter must support. Whenever a constructed type or generic method is used, the type argument is checked against the constraints on the type parameter at compile time. The type argument supplied must satisfy the conditions described in §4.4.4.

A class-type constraint must satisfy the following rules:

- The type must be a class type.
- The type must not be sealed.
- The type must not be one of the following types: System.Array, System.Delegate, System.Enum, or System.ValueType.

> **JON SKEET** I know of no reason to prohibit System.Enum or System.Delegate as the type here—although it would certainly be more friendly to be able to write "where T : enum" than "where T : struct, Enum", which would be the most common use. Although C# is specified separately from the CLI, you might suspect that this is a CLI limitation—but it's not. Indeed, ECMA-335 explicitly lists this and other constraints that are prohibited in C#. Perhaps this restriction will be removed from a future version of the language; there are plenty of situations where it would be useful.

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
