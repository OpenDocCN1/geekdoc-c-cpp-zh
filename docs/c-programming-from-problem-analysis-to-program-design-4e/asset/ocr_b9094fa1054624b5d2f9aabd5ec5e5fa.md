is contracted as part of implementing ICloneable. The IList interface requires implementation details for Add(), Clear(), Remove(), Insert(), plus other methods. The ICollection interface has a method for CopyTo(). The IEnumerable interface has a method titled GetEnumerator() that returns an enumerator that can iterate through a collection.

The signatures for some of the collection classes are shown in Example 11–23.

# EXAMPLE 11.23

```
public abstract class Array : ICloneable, IList, ICollection,
                             IEnumerable
public class ArrayList : IList, ICollection, IEnumerable, ICloneable
public class Queue : ICollection, IEnumerable, ICloneable
public class Stack : ICollection, IEnumerable, ICloneable
public class Hashtable : IDictionary, ICollection, IEnumerable,
    ISerializable, IDeserializationCallback, ICloneable
```

Notice that each of the collection classes implements ICloneable. The Array class is the only one in the collection that is an abstract class. The Hashtable class is the only one that implements the IDeserializationCallback interface. You are encouraged to explore the documentation for these classes and interfaces. By doing so, you can see some of the real power of object-oriented development. As you explore the documentation, you will notice that it includes not only the members that must be implemented, but it also gives a description of the class and shows examples in multiple languages.

The documentation provides links to the classes so that you can drill down and uncover additional information.

> **NOTE**
> 
> One of the most powerful features of the .NET Framework class library and Visual Studio is the extensive library of documentation available. In addition to syntax grammar, it includes tutorials and examples of feature use.

The Hashtable class implements Add() by adding an element with the specified key and value pair into a collection. The ArrayList class implements Add() by adding an object to the end of a collection. Can Add() mean something different based on what type of object it is being used with? That is the idea behind polymorphism—the topic of the next section.

# Polymorphism

**Polymorphism** is the ability for classes to provide different implementations of methods that are called by the same name. You already understand and use polymorphism in your everyday life when you determine what situation an object is being used with a verb to