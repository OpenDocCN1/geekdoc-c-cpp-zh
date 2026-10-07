base classes let you share implementation along with the member signatures, whereas interfaces allow you to share the member signatures without necessarily sharing the implementation.

Instead of sharing a common base class, each compression needs to implement a common interface. Interfaces define the contract that a class supports to interact with the other classes that expect the interface. If all the classes implemented the IFileCompression interface and its Compress() and Uncompress() methods, the code for calling the algorithm on any particular compression class would simply involve a conversion to the IFileCompression interface and a call to the members. The result is polymorphism because each compression class has the same method signature but individual implementations of that signature.

The IFileCompression interface shown in Listing 8.1 is an example of an interface implementation. By convention—a convention so strong it is universal—the interface name is PascalCase with a capital “I” prefix.

# Listing 8.1: Defining an Interface

```
interface IFileCompression
{
    void Compress(string targetFileName, string[] fileList);
    void Uncompress(
        string compressedFileName, string expandDirectory);
}
```

IFileCompression defines the methods that type must be used in the same manner as other compression-related classes. The power of interfaces is that they grant the ability to switch among implementations without modifying the calling code.

Prior to C# 8.0, one of the key characteristics of an interface was that it had no implementation and no data (fields). Method declarations in an interface always had a single semicolon in place of curly braces after the declaration. Properties, looking like automatically implemented properties, with no backing fields. In fact, fields (data) could not appear in an interface declaration either.

Many of these rules were relaxed in C# 8.0 for the purposes of allowing interfaces to have some level of restricted changes after publishing. However, until