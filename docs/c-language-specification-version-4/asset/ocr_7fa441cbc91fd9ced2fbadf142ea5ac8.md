```
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

# 3.8 Namespace and type names

Several contexts in a C# program require a namespace-name or a type-name to be specified.

namespace-name:
    namespace-or-type-name

type-name:
    namespace-or-type-name

namespace-or-type-name:
    identifier type-argument-list_opt
    namespace-or-type-name . identifier type-argument-list_opt
    qualified-alias-member

A namespace-name is a namespace-or-type-name that refers to a namespace. Following resolution as described below, the namespace-or-type-name of a namespace-name must refer to a namespace, or otherwise a compile-time error occurs. No type arguments (§4.4.1) can be present in a namespace-name (only types can have type arguments).

A type-name is a namespace-or-type-name that refers to a type. Following resolution as described below, the namespace-or-type-name of a type-name must refer to a type, or otherwise a compile-time error occurs.

If the namespace-or-type-name is a qualified-alias-member its meaning is as described in §9.7. Otherwise, a namespace-or-type-name has one of four forms:

+   - I
+   - I<A₁, ..., Aₙ>
+   - N.I
+   - N.I<A₁, ..., Aₙ>

where I is a single identifier, N is a namespace-or-type-name and <A₁, ..., Aₙ> is an optional type-argument-list. When no type-argument-list is specified, consider K to be zero.

The meaning of a namespace-or-type-name is determined as follows:

+   - If the namespace-or-type-name is of the form I or of the form I<A₁, ..., Aₙ>:
+     - If K is zero and the namespace-or-type-name appears within a generic method declaration (§10.6) and if that declaration includes a type parameter (§10.1.3) with name I, then the namespace-or-type-name refers to that type parameter.
+     - Otherwise, if the namespace-or-type-name appears within a type declaration, then for each instance type T (§10.3.1), starting with the instance type of that type declaration and continuing with the instance type of each enclosing class or struct declaration (if any):