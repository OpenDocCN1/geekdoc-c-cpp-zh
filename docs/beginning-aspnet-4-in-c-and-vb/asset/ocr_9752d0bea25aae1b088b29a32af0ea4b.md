Because the interface IResourceReader is derived from IEnumerable and IDisposable, the methods GetEnumerator(), which returns an IEnumerator interface, and Dispose() must be implemented, too:

```
IEnumerator IEnumerable.GetEnumerator()
{
    return this.GetEnumerator();
}

void IDisposable.Dispose()
{
}
}
```

# Creating a DatabaseResourceSet

The class DatabaseResourceSet can use nearly all implementations of the base class ResourceSet. You just need a different constructor that initializes the base class with your own resource reader, DatabaseResourceReader. The constructor of ResourceSet allows passing an object by implementing IResourceReader; this requirement is fulfilled by DatabaseResourceReader:

```
public class DatabaseResourceSet : ResourceSet
{
    internal DatabaseResourceSet(string connectionString, CultureInfo culture)
        : base(new DatabaseResourceReader(connectionString, culture))
    {
    }

    public override Type GetDefaultReader()
    {
        return typeof(DatabaseResourceReader);
    }
}
```

code snippet DatabaseResourceReader/DatabaseResourceSet.cs

# Creating a DatabaseResourceManager

The third class you have to create is the custom resource manager. DatabaseResourceManager is derived from the class ResourceManager, and you only have to implement a new constructor and override the method InternalGetResourceSet().

In the constructor, create a new Dictionary<string, DatabaseResourceSet> to store all queried resource sets and set it into the field ResourceSets defined by the base class:

```
public class DatabaseResourceManager : ResourceManager
{
    private string connectionString;
    private Dictionary<string, DatabaseResourceSet> resourceSets;
    public DatabaseResourceManager(string connectionString)
    {
        this.connectionString = connectionString;
        resourceSets = new Dictionary<string, DatabaseResourceSet>();
    }
}
```

code snippet DatabaseResourceReader/DatabaseResourceManager.cs

The methods of the ResourceManager class that you can use to access resources (such as GetString() and GetObject()) invoke the method InternalGetResourceSet() to access a resource set where the appropriate values can be returned.