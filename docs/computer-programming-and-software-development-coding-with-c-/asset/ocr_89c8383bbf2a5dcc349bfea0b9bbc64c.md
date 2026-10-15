Explicit implementation changes things a bit. When we provide an explicit implementation, that implementation belongs to the interface rather than the class, this means that we can only access the explicitly implemented member by using the interface type. If we try to use the class type, we will get an error. Another difference is that explicitly implemented members have no access modifiers. If we try to mark an explicit implementation as public or private, we will get a compiler error. Here is an example of an explicitly implemented interface member.

```
public interface ISaveable {
    void Save();
}

public class Catalog : ISaveable
{
    void ISaveable.Save()
    {
        Console.Write("Saved");
    }
}
```

We have the same ISaveable interface that we saw earlier, but the implementation in the Catalog class is different. The main difference is that the implementation uses the interface name. So here we have ISaveable.Save, this indicates that the implementation belongs to the ISaveable interface rather than the Catalog class. Also, this method does not have an access modifier. If we try to mark this as public or