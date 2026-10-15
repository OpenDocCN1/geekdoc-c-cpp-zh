Because a class type constraint requires a particular class, using a struct constraint with a class type constraint would be contradictory. Therefore, you cannot combine struct and class constraints.

The struct constraint has one special characteristic: Nullable value types do not satisfy the constraint. Why? Nullable value types are implemented as the generic type `Nullable<T>`, which itself applies the struct constraint to T. If nullable value types satisfied that constraint, it would be possible to define the nonsense type `Nullable<Nullable<int>>`. A doubly nullable integer is confusing to the point of being meaningless. (As expected, the shorthand syntax `int??` is also disallowed.)

# Multiple Constraints

For any given type parameter, you may specify any number of interface type constraints, but no more than one class type constraint (just as a class may implement any number of interfaces but inherit from only one other class). Each new constraint is declared in a comma-delimited list following the generic type parameter and a colon. If there is more than one type parameter, each must be preceded by the where keyword. In Listing 11.25, the generic `EntityDictionary` class declares two type parameters: `TKey` and `TValue`. The `TKey` type parameter has two interface type constraints, and the `TValue` type parameter has one class type constraint.

```
public class EntityDictionary<TKey, TValue>
    : Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase
{
    ...
}
```

In this case, there are multiple constraints on `TKey` itself and an additional constraint on `TValue`. When specifying multiple constraints on one type parameter, an AND relationship is assumed. If a type C is supplied as the type argument for `TKey`, C must implement `IComparable<C>` and `IFormattable`, for example.

Notice there is no comma between each where clause.