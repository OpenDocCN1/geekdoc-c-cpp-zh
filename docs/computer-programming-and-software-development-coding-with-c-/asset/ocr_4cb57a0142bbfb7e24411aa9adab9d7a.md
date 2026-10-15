```
{
    public class GenericRepository<T> where T:EntityBase
    {
        private readonly List<T> _items = new();

        public T GetById(int id)
        {
            return _items.Single(item => item. == id);
        }

        public void Add(T item)
        {
            _items.Add(item);
        }
    }
```

You use a colon, and you can say T must be of type EntityBase. When I scroll up in this file, you can see I have here already a using directive for the entity's namespace, so EntityBase is found. Now in the code, it's clear that T is of type EntityBase, so when I write here a dot, you see now we get here this Id property because this one is defined in the EntityBase class. So I can use it here, and now we have this GetById method implemented in this generic class.

```
public class GenericRepository<T> where T:EntityBase
{
    private readonly List<T> _items = new();

    public T GetById(int id)
    {
        return _items.Single(item => item. == id);
    }

    public void Add(T item)
    {
        _items.Add(item);
    }

    public void Remove(T item)
    {
        _items.Remove(item);
    }
```