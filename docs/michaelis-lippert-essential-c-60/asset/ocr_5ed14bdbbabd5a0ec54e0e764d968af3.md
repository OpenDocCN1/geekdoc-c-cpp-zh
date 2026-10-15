T will be available on the nested type as well. If the nested type includes its own type parameter named T, this will hide the type parameter within the containing type and any reference to T in the nested type will refer to the nested T type parameter. Fortunately, reuse of the same type parameter name within the nested type will cause a compiler warning to prevent accidental overlap (see Listing 11.18).

# LISTING 11.18: Nested Generic Types

```
class Container<T, U>
{
    // Nested classes inherit type parameters.
    // Reusing a type parameter name will cause
    // a warning.
    class Nested<U>
    {
        void Method(T param0, U param1)
        {
        }
    }
}
```

The containing type’s type parameters are accessible in the nested type the same way that members of the containing type are also accessible from the nested type. The rule is simply that a type parameter is available anywhere within the body of the type that declares it.

# Guidelines

> AVOID shadowing a type parameter of an outer type with an identically named type parameter of a nested type.

# Constraints

Generics support the ability to define constraints on type parameters. These constraints ensure that the types provided as type arguments conform to various rules. Take, for example, the BinaryTree<T> class shown in Listing 11.19.

# LISTING 11.19: Declaring a BinaryTree<T> Class with No Constraints

```
public class BinaryTree<T>
{
```