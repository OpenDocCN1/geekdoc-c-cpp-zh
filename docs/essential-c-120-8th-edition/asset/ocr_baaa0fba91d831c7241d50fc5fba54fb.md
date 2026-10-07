# Constraints 651

method on a value typed as a generic type parameter, the compiler checks whether the method matches any method on any of the interfaces declared as constraints.

If you tried to create a BinaryTree<T> variable using System.Text.StringBuilder as the type parameter, you would receive a compiler error because StringBuilder does not implement IComparable<StringBuilder>. The error is similar to the one shown in Output 12.3.

# Output 12.3

```
error CS0311: The type 'System.Text.StringBuilder' cannot be used as type
parameter 'T' in the generic type or method 'BinaryTree<T>'. There is no implicit reference conversion from 'System.Text.StringBuilder' to 'System.IComparable<System.Text.StringBuilder>'.
```

To specify an interface for the constraint, you declare an interface constraint. This constraint even circumvents the need to call an explicit interface member implementation.

# Type Parameter Constraints

Sometimes you might want to constrain a type argument to be convertible to a particular type. You do do this using a type parameter constraint, as shown in Listing 12.23.

Listing 12.23: Declaring a Class Type Constraint

```
public class EntityDictionary<TKey, TValue>
    : System.Collections.Generic.Dictionary<TKey, TValue>
    where TKey : notnull
    where TValue : EntityBase
{
    // ...
}
```

In Listing 12.23, EntityDictionary<TKey, TValue> requires that all type arguments provided for the type parameter TValue be implicitly convertible to the EntityBase class. By requiring the conversion, it becomes possible to use the members of EntityBase on values of type TValue within the generic