Important Some extensible applications use Assembly.LoadFrom to load an assembly and then construct objects from types defined in the loaded assembly. These objects can be serialized without any trouble. However, when deserializing this stream, the formatter attempts to load the assembly by calling Assembly's Load method instead of calling LoadFrom. In most cases, the CLR will not be able to locate the assembly file, causing a SerializationException to be thrown. This catches many developers by surprise—because the objects serialized, the developers expect that the objects will deserialize correctly as well.

If your application serializes objects whose types are defined in an assembly that uses Assembly.LoadFrom, I recommend that you implement a method whose signature matches the System.ResolveEventHandler delegate and register this method with System.AppDomain.AssemblyResolve event just before calling a Deserialize method. Now, whenever the formatter fails to load an assembly, the CLR calls your ResolveEventHandler method. This method is passed the identity of the assembly that failed to load. The method can extract the file name from the assembly's identity and use it to construct the path where the application knows the assembly file can be found. Then, the method can call Assembly.LoadFrom to load the assembly and returning the Assembly reference back from the ResolveEventHandler method.

This section covers the basics of how to serialize and deserialize object graphs. In the remaining sections, we'll look at what you must do in order to define your serializable types, we'll also look at various mechanisms that allow you to have greater control over serialization and deserialization.

# Making a Type Serializable

When a type is designed, the developer must make the conscious decision as to whether or not to allow instances of the type to be serializable. By default, types are not serializable. For example, the following code does not perform as expected.

```
internal struct Point { public Int32 x, y; }

private static void OptInSerialization() {
    Point pt = new Point { x = 1, y = 2 };
    using (var stream = new MemoryStream()) {
        new BinaryFormatter().Serialize(stream, pt); // throws SerializationException
}
```