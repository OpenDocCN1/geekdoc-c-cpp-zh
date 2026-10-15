class, it has a Key property, and this Key property is of type string because that's the type that is passed directly to the base class.

```
public class GenericRepository<T,TKey>
{
    public TKey? Key { get; set; }

    protected readonly List<T> _items = new();

    public void Add(T item)
    {
        _items.Add(item);
    }

    public void Remove(T item)
    {
        _items.Remove(item);
    }

    public void Save()
    {
        foreach (var item in _items)
```

Now, let me change this back to just the GenericRepository, and let's go back to the GenericRepository C# file. Here, I just cut the Remove method, and we don't need actually a subclass. So let's delete this subclass. It was just here to explain you a few bits about inheritance. Now, in the GenericRepository class, let's paste here the Remove method. Also, in this class, let's remove the Key property, and let's remove also the second type parameter, TKey. We just need the T parameter. Now, as we don't have a subclass, we can make this items field again private. Now we have this GenericRepository