```
public interface ISaveable {
    void Save();
    // void Save(string message) REMOVED
}
```

```
public class InventoryItem
{
    ISaveable saver = new SQLSaver();
    saver.Save("Added inventory"); *** ERROR ***
}
```

If we add a second Save method to the interface, then our Catalog class breaks. It does not have the second method and so no longer satisfies the interface. Our code is broken, and we get a compiler error. Removing members from an interface breaks the clients. Let's say that we have an ISaveable interface with two Save methods. We also have a client that calls one of those methods through the interface. If we remove that method from the interface, then the client is Broken. It is trying to call a method that no longer exists on the interface. We really need to keep in mind that an interface is a contract. Once it is in use by implementers and clients, we really should not change the terms of the contract. With that said, there are a couple of ways that we can add members to an interface. One way that we can add members to an interface is with default implementation. This lets us add a member to an interface along with implementation code. Since the implementation is part of the