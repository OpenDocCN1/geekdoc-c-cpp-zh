```
```csharp
public class Stack : ICollection, IEnumerable, ICloneable
public class Hashtable : IDictionary, ICollection, IEnumerable,
    ISerializable, IDeserializationCallback, ICloneable
```
```

Notice that each of the collection classes implements ICloneable. The Array class is the only one in the collection that is an abstract class. The Hashtable class is the only one that implements the IDeserializationCallback interface. You are encouraged to explore the documentation for these classes and interfaces. By doing so, you can see some of the real power of object-oriented development. As you explore the documentation, you notice that it includes not only the members that must be implemented, but it also gives a description of the class and shows examples in multiple languages.

The documentation provides links to the classes so that you can drill down and uncover additional information.

![](bbox=[0.175, 0.364, 0.237, 0.413])

One of the most powerful features of the .NET Framework class library and Visual Studio is the extensive library of documentation available. In addition to syntax grammar, it includes tutorials and examples of feature use.

The Hashtable class implements Add( ) by adding an element with the specified key and value pair into a collection. The ArrayList class implements Add( ) by adding an object to the end of a collection. Can Add( ) mean something different based on what type of object it is being used with? That is the idea behind polymorphism—the topic of the next section.

# POLYMORPHISM

**Polymorphism** is the ability for classes to provide different implementations of methods that are called by the same name. You already understand and use polymorphism in your everyday life when you determine what situation or **object** is being used with a verb to determine the verb’s true behavior. For example, by itself the meaning of the verb “drive” is vague. Driving a car differs from driving a nail, driving a boat, or driving someone crazy. Only when you put “drive” in context do you know what behavior or activity is associated with it.

You have also experienced the use of polymorphism in your programs a number of times. One quick example is with the ToString( ) method. Remember that this method is defined as one of the four methods of the **Object class**. This means that for every **class** in .NET, both user-defined and Framework classes have a ToString( ) method. Based on what kind of **object** calls the ToString( ) method, it performs a different function. The end result is to convert some **object** to its **string** representation. Converting an integer to a **string** is a different activity than converting a single character to a **string**. You can think of it as having a number of different implementations, and the implementation is determined by the type of **object** that calls it. Example 11-24 shows two calls to the ToString( ) method, which were included in the PresentationGUI **class**.