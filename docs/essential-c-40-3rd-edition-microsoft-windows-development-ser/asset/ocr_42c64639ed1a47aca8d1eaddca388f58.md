If you tried to create a BinaryTree<T> variable using System.Text.StringBuilder as the type parameter, you would receive a compiler error because StringBuilder does not implement IComparable<T>. The error is similar to the one shown in Output 11.3.

# Output 11.3:

```
error CS0309: The type 'System.Text.StringBuilder' must be convertible
to 'System.IComparable<T>' in order to use it as parameter 'T' in the
generic type or method 'BinaryTree<T>'
```

To specify an interface for the constraint you declare an interface constraint. This constraint even circumvents the need to cast in order to call an explicit interface member implementation.

# Base Class Constraints

Sometimes you might want to limit the constructed type to a particular class derivation. You do this using a base class constraint, as shown in Listing 11.23.

# LISTING 11.23: Declaring a Base Class Constraint

```
public class EntityDictionary<TKey, TValue>
    : System.Collections.Generic.Dictionary<TKey, TValue>
    where TValue : EntityBase
{
        ...
}
```

In contrast to System.Collections.Generic.Dictionary<TKey, TValue>
on its own, EntityDictionary<TKey, TValue> requires that all TValue
types derive from the EntityBase class. By requiring the derivation, it is
possible to always perform a cast operation within the generic implementation,
because the constraint will ensure that all type parameters derive
from the base and, therefore, that all TValue type parameters used with
EntityDictionary can be implicitly converted to the base.

The syntax for the base class constraint is the same as that for the interface constraint, except that base class constraints must appear first when multiple constraints are specified. However, unlike interface constraints,