that is when we need to implement multiple interfaces that have conflicting method signatures. Here is an example of two interfaces that have different return types and the same method name.

```
public interface ISaveable {
    void Save();
}

public interface IDbSaver {
    string Save();
}
```

We can overload methods in C# by specifying different parameters, but we are not allowed to overload them by specifying different return types. This means that if we want to implement both of these interfaces, we need to explicitly implement one of the methods so that the compiler will know which method we want to use. Here is a Catalog class that explicitly implements one of the interfaces.

```
public class Catalog : ISaveable, IDbSaver
{
    public void Save()      // Catalog & ISaveable
    {
        Console.Write("Saved from ISaveable interface");
    }
    string IDbSaver.Save()  // IDbSaver (explicit)
    {
        return "Saved from IDbSaver interface";
    }
}
```

In this case, the Save method is available to both catalog and the ISaveable interface. The IDbSaver.Save method is only available to IDbSaver. We could also implement it the other way where ISaveable is explicit and a standard Save method is available to Catalog and