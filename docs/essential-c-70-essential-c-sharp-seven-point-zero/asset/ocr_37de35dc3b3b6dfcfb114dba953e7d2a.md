One way to circumvent this restriction is to supply a factory interface that includes a method for instantiating the type. The factory implementing the interface takes responsibility for instantiating the entity rather than the EntityDictionary itself (see Listing 12.33).

# LISTING 12.33: Using a Factory Interface in Place of a Constructor Constraint

```
```csharp
public class EntityBase<TKey>
{
    public EntityBase(TKey key)
    {
        Key = key;
    }
    public TKey Key { get; set; }
}

public class EntityDictionary<TKey, TValue, TFactory> :
    Dictionary<TKey, TValue>
    where TKey : IComparable<TKey>, IFormattable
    where TValue : EntityBase<TKey>
    where TFactory : IEntityFactory<TKey, TValue>, new()
{
    ...
    public TValue New(TKey key)
    {
        TFactory factory = new TFactory();
        TValue newEntity = factory.CreateNew(key);
        Add(newEntity.Key, newEntity);
        return newEntity;
    }
    ...
}

public interface IEntityFactory<TKey, TValue>
{
    TValue CreateNew(TKey key);
}
```
```

A declaration such as this allows you to pass the new key to a TValue factory method that takes parameters, rather than forcing you to rely on the default constructor. It no longer uses the constructor constraint on TValue because TFactory is responsible for instantiating value. (One modification to the code in Listing 12.33 would be to cache a reference to the factory method—possibly leveraging Lazy<T> if multithreaded support was needed. This would enable you to reuse the factory method instead of reinstantiating it every time.)