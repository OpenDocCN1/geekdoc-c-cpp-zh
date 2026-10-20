includes properties and fields. All you need to ensure the proper result is to utilize the proper visibility, as explained in the earlier chapter.

Another thing you need to remember is that inheritance need not take place from one class to another. It is possible to have an entire hierarchy of classes that inherit from one another. Keeping in tune with the earlier examples, it is possible to create a Kitten class that inherits from the Cat class and that, in turn, will be inheriting from the Animal class.

However, there is one thing that you cannot perform in C#, and that is multiple inheritances. In other words, you cannot make a class inherit from multiple classes simultaneously. C# does not support this feature.

# Understanding the Concept of Base Class and Derived Class

It is possible for a class to be derived from more than a single class. As a result, it is possible to inherit the functions and data from multiple base classes.

Given below is the syntax used to create derived classes in C#.

```
```csharp
<access-specifier> class <base_class>

{

...
```
```