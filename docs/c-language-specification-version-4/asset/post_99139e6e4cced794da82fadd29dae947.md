
```
      static void F(long l) {}
    }
```

the call F(1) invokes the F declared in Inner because all outer occurrences of F are hidden by the inner declaration. For the same reason, the call F("Hello") results in a compile-time error.

## 3.7.1.2 Hiding through inheritance

Name hiding through inheritance occurs when classes or structs redeclare names that were inherited from base classes. This type of name hiding takes one of the following forms:

- A constant, field, property, event, or type introduced in a class or struct hides all base class members with the same name.
- A method introduced in a class or struct hides all non-method base class members with the same name, and all base class methods with the same signature (method name and parameter count, modifiers, and types).
- An indexer introduced in a class or struct hides all base class indexers with the same signature (parameter count and types).

The rules governing operator declarations (§10.10) make it impossible for a derived class to declare an operator with the same signature as an operator in a base class. Thus, operators never hide one another.

Contrary to hiding a name from an outer scope, hiding an accessible name from an inherited scope causes a warning to be reported. In the example

```csharp
class Base
{
    public void F() {}
}
class Derived: Base
{
    public void F() {}      // warning, hiding an inherited name
}
```

the declaration of F in Derived causes a warning to be reported. Hiding an inherited name is specifically not an error, since that would preclude separate evolution of base classes. For example, the above situation might have come about because a later version of Base introduced an F method that wasn't present in an earlier version of the class. Had the above situation been an error, then any change made to a base class in a separately versioned class library could potentially cause derived classes to become invalid.

The warning caused by hiding an inherited name can be eliminated through use of the new modifier:

```csharp
class Base
{
    public void F() {}
}
class Derived: Base
{
    new public void F() {}
}
```

The new modifier indicates that the F in Derived is “new”, and that it is indeed intended to hide the inherited member.

A declaration of a new member hides an inherited member only within the scope of the new member.

```csharp
class Base
{
    public static void F() {}
}
class Derived: Base
{
    new private static void F() {}    // Hides Base.F in Derived only
}
class MoreDerived: Derived
{
    static void G() { F(); }          // Invokes Base.F
}
```

In the example above, the declaration of F in Derived hides the F that was inherited from Base, but since the new F in Derived has private access, its scope does not extend to MoreDerived. Thus, the call F() in MoreDerived.G is valid and will invoke Base.F.

## 3.8 Namespace and type names

Several contexts in a C# program require a namespace-name or a type-name to be specified.

```
namespace-name:
    namespace-or-type-name

type-name:
    namespace-or-type-name

namespace-or-type-name:
    identifier type-argument-list_opt
    namespace-or-type-name . identifier type-argument-list_opt
    qualified-alias-member
```

A namespace-name is a namespace-or-type-name that refers to a namespace. Following resolution as described below, the namespace-or-type-name of a namespace-name must refer to a namespace, or otherwise a compile-time error occurs. No type arguments (§4.4.1) can be present in a namespace-name (only types can have type arguments).

A type-name is a namespace-or-type-name that refers to a type. Following resolution as described below, the namespace-or-type-name of a type-name must refer to a type, or otherwise a compile-time error occurs.

If the namespace-or-type-name is a qualified-alias-member, its meaning is as described in §9.7. Otherwise, a namespace-or-type-name has one of four forms:

- I
- I<A₁, ..., Aₙ>
- N.I
- N.I<A₁, ..., Aₙ>

where I is a single identifier, N is a namespace-or-type-name and <A₁, ..., Aₙ> is an optional type-argument-list. When no type-argument-list is specified, consider K to be zero.

The meaning of a namespace-or-type-name is determined as follows:

- If the namespace-or-type-name is of the form I or of the form I<A₁, ..., Aₙ>:
  - If K is zero and the namespace-or-type-name appears within a generic method declaration (§10.6) and if that declaration includes a type parameter (§10.1.3) with name I, then the namespace-or-type-name refers to that type parameter.
  - Otherwise, if the namespace-or-type-name appears within a type declaration, then for each instance type T (§10.3.1), starting with the instance type of that type declaration and continuing with the instance type of each enclosing class or struct declaration (if any):
    - If K is zero and the declaration of T includes a type parameter with name I, then the *namespace-or-type-name* refers to that type parameter.
    - Otherwise, if the *namespace-or-type-name* appears within the body of the type declaration, and T or any of its base types contain a nested accessible type having name I and K type parameters, then the *namespace-or-type-name* refers to that type constructed with the given type arguments. If there is more than one such type, the type declared within the more derived type is selected. Note that non-type members (constants, fields, methods, properties, indexers, operators, instance constructors, destructors, and static constructors) and type members with a different number of type parameters are ignored when determining the meaning of the *namespace-or-type-name*.
    - If the previous steps were unsuccessful then, for each namespace N, starting with the namespace in which the *namespace-or-type-name* occurs, continuing with each enclosing namespace (if any), and ending with the global namespace, the following steps are evaluated until an entity is located:
      - If K is zero and I is the name of a namespace in N, then:
        - If the location where the *namespace-or-type-name* occurs is enclosed by a namespace declaration for N and the namespace declaration contains an *extern-alias-directive* or *using-alias-directive* that associates the name I with a namespace or type, then the *namespace-or-type-name* is ambiguous and a compile-time error occurs.
        - Otherwise, the *namespace-or-type-name* refers to the namespace named I in N.
      - Otherwise, if N contains an accessible type having name I and K type parameters, then:
        - If K is zero and the location where the *namespace-or-type-name* occurs is enclosed by a namespace declaration for N and the namespace declaration contains an *extern-alias-directive* or *using-alias-directive* that associates the name I with a namespace or type, then the *namespace-or-type-name* is ambiguous and a compile-time error occurs.
        - Otherwise, the *namespace-or-type-name* refers to the type constructed with the given type arguments.
      - Otherwise, if the location where the *namespace-or-type-name* occurs is enclosed by a namespace declaration for N:
        - If K is zero and the namespace declaration contains an *extern-alias-directive* or *using-alias-directive* that associates the name I with an imported namespace or type, then the *namespace-or-type-name* refers to that namespace or type.
        - Otherwise, if the namespaces imported by the *using-namespace-directives* of the namespace declaration contain exactly one type having name I and K type parameters, then the *namespace-or-type-name* refers to that type constructed with the given type arguments.
        - Otherwise, if the namespaces imported by the *using-namespace-directives* of the namespace declaration contain more than one type having name I and K type parameters, then the *namespace-or-type-name* is ambiguous and an error occurs.
        - Otherwise, the *namespace-or-type-name* is undefined and a compile-time error occurs.
      - Otherwise, the *namespace-or-type-name* is of the form N.I or of the form N.I<A₁, ..., Aₖ>. N is first resolved as a *namespace-or-type-name*. If the resolution of N is not successful, a compile-time error occurs. Otherwise, N.I or N.I<A₁, ..., Aₖ> is resolved as follows:
        - If K is zero and N refers to a namespace and N contains a nested namespace with name I, then the *namespace-or-type-name* refers to that nested namespace.
