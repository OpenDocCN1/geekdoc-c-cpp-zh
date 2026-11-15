call to Event() because the signature of the event firing is unknown with the data types System.Delegate and System.MulticastDelegate. The same restriction occurs for any enum type.

# Constructor Constraints Are Allowed Only for Default Constructors

Listing 11.26 includes a constructor constraint that forces TValue to support a default constructor. There is no constraint to force TValue to support a constructor other than the default. For example, it is not possible to make EntityBase key protected and only set it in a TV alue constructor that takes a TKey parameter using constraints alone. Listing 11.32 demonstrates the invalid code.

# LISTING 11.32: Constructor Constraints Can Be Specified Only for Default Constructors

```
public TValue New(TKey key)
{
    // Error: 'TValue': Cannot provide arguments
    // when creating an instance of a variable type.
    TValue newEntity = null;
    // newEntity = new TValue(key);
    Add(newEntity.Key, newEntity);
    return newEntity;
}
```

One way to circumvent this restriction is to supply a factory interface that includes a method for instantiating the type. The factory implementing the interface takes responsibility for instantiating the entity rather than the EntityDictionary itself (see Listing 11.33).

# Listing 11.33: Using a Factory Interface in Place of a Constructor Constraint

```
public class EntityBase<TKey>
{
    public EntityBase(TKey key)
    {
        Key = key;
    }

    public TKey Key
    {
        get { return _key; }
        set { _key = value; }
    }

    private TKey _key;
}

public class EntityDictionary<TKey, TValue, TFactory> :
    Dictionary<TKey, TValue>
    where TKey : IComparable<T>, IFormattable
```