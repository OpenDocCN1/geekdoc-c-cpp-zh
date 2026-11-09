```
```csharp
// Example: Set default values for fields in a new version of this type
}

[OnDeserialized]
private void OnDeserialized(StreamingContext context) {
    // Example: Initialize transient state from fields
    sum = x + y;
}

[OnSerializing]
private void OnSerializing(StreamingContext context) {
    // Example: Modify any state before serializing
}

[OnSerialized]
private void OnSerialized(StreamingContext context) {
    // Example: Restore any state after serializing
}
```
```

Whenever you use any of these four attributes, the method you define must take a single **StreamingContext** parameter (discussed in the “Streaming Contexts” section later in this chapter) and return **void**. The name of the method can be anything you want it to be. Also, you should declare the method as **private** to prevent it from being called by normal code; the formatters run with enough security that they can call private methods.

> **Note** When you are serializing a set of objects, the formatter first calls all of the objects’ methods that are marked with the **OnSerializing** attribute. Next it serializes all of the objects’ fields, and finally it calls all of the objects’ methods marked with the **OnSerialized** attribute. Similarly, when you deserialize a set of objects, the formatter calls all of the objects’ methods that are marked with the **OnDeserializing** attribute, then it deserializes all of the object’s fields, and then it calls all of the objects’ methods marked with the **OnDeserialized** attribute.
> 
> Note also that during deserialization, when a formatter sees a type offering a method marked with the **OnDeserialized** attribute, the formatter adds this object’s reference to an internal list. After all the objects have been deserialized, the formatter traverses this list in reverse order and calls each object’s **OnDeserialized** method. When this method is called, all the serializable fields will be set correctly, and they may be accessed to perform any additional work that would be necessary to fully deserialize the object. Invoking these methods in reverse order is important because it allows inner objects to finish their deserialization before the outer objects that contain them finish their deserialization.
> 
> For example, imagine a collection object (like **HashTable** or **Dictionary**) that internally uses a hash table to maintain its sets of items. The collection object type would implement a method marked with the **OnDeserialized** attribute. Even though the collection object would start being deserialized first (before its items), its **OnDeserialized** method would be called last (after any of its items’ **OnDeserialized** methods). This allows the items to complete deserialization so that all their fields are initialized properly, allowing a good hash code value to be calculated. Then, the collection object creates its internal buckets and uses the items’ hash codes to place the items into the buckets. I show an example of how the **Dictionary** class uses this in the upcoming “Controlling the Serialized/Deserialized Data” section of this chapter.