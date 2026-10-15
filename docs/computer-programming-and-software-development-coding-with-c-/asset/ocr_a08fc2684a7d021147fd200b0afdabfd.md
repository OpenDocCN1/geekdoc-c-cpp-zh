```
public class GenericRepository<T> where T : IEntity
{
    private readonly List<T> _items = new();

    public T GetById(int id)
    {
        //return _items.Single(item => item.Id == id);

        return default;
    }

    public void Add(T item)
    {
        item.Id = _items.Count + 1;
        _items.Add(item);
    }

    public void Remove(T item)
    {
```

Now you see it's again underlined in red, and now you can specify here the class constraint which says that T is a reference type, so it can actually be null. Also important to know is how the class constraint behaves when you have turned on nullable reference types like we have for our project. So when you go to the Solution Explorer, and when you here the project to open the csproj file, you can see here that we have enabled Nullable reference types.

```
<PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>
    <Nullable>enable</Nullable>
</PropertyGroup>

</Project>
```