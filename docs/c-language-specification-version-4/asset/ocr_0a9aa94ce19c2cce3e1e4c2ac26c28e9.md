+   - Otherwise, if N refers to a namespace and N contains an accessible type having name I and K type parameters, then the namespace-or-type-name refers to that type constructed with the given type arguments.
+   - Otherwise, if N refers to a (possibly constructed) class or struct type and N or any of its base classes contain a nested accessible type having name I and K type parameters, then the namespace-or-type-name refers to that type constructed with the given type arguments. If there is more than one such type, the type declared within the more derived type is selected. Note that if the meaning of N.I is being determined as part of resolving the base class specification of N then the direct base class of N is considered to be object (§10.1.4.1).
+   - Otherwise, N.I is an invalid namespace-or-type-name, and a compile-time error occurs.

A namespace-or-type-name is permitted to reference a static class (§10.1.1.3) only if

+   - The namespace-or-type-name is the T in a namespace-or-type-name of the form T.I, or
+   - The namespace-or-type-name is the T in a typeof-expression (§7.5.11) of the form typeof(T).

# 3.8.1 Fully qualified names

Every namespace and type has a fully qualified name, which uniquely identifies the namespace or type amongst all others. The fully qualified name of a namespace or type N is determined as follows:

+   - If N is a member of the global namespace, its fully qualified name is N.
+   - Otherwise, its fully qualified name is S.N, where S is the fully qualified name of the namespace or type in which N is declared.

In other words, the fully qualified name of N is the complete hierarchical path of identifiers that lead to N, starting from the global namespace. Because every member of a namespace or type must have a unique name, it follows that the fully qualified name of a namespace or type is always unique.

The example below shows several namespace and type declarations along with their associated fully qualified names.

```
```
class A {}          // A
namespace X         // X
{
    class B         // X.B
    {
        class C {}  // X.B.C
    }
    namespace Y     // X.Y
    {
        class D {}  // X.Y.D
    }
}
namespace X.Y       // X.Y
{
    class E {}      // X.Y.E
}
```
```

# 3.9 Automatic memory management

C# employs automatic memory management, which frees developers from manually allocating and freeing the memory occupied by objects. Automatic memory management policies are implemented by a garbage collector. The memory management life cycle of an object is as follows: