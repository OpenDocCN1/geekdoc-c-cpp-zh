Notice that I had to add the new keyword to the definition of the previous Message method (see Item 33). MyClass.Message() is not virtual. Derived classes cannot provide an overridden version of Message. The MyDerived class creates a new Message method, but that method does not override MyClass.Message. It hides it. Furthermore, MyClass.Message is still available through the IMsg reference:

```
```csharp
MyDerivedClass d = new MyDerivedClass();
d.Message(); // prints "MyDerivedClass".
IMsg m = d as IMsg;
m.Message(); // prints "MyClass"
```
```

Interface methods are not virtual. When you implement an interface, you are declaring a concrete implementation of a particular contract in that type.

But you often want to create interfaces, implement them in base classes, and modify the behavior in derived classes. You can. You've got two options. If you do not have access to the base class, you can reimplement the interface in the derived class:

```
```csharp
public class MyDerivedClass : MyClass
{
    public new void Message()
    {
        Console.WriteLine("MyDerivedClass");
    }
}
```
```

The addition of the IMsg keyword changes the behavior of your derived class so that IMsg.Message() now uses the derived class version:

```
```csharp
MyDerivedClass d = new MyDerivedClass();
d.Message(); // prints "MyDerivedClass".
IMsg m = d as IMsg;
m.Message(); // prints " MyDerivedClass "
```
```

You still need the new keyword on the MyDerivedClass.Message() method. That's your clue that there are still problems (see Item 33). The base class version is still accessible through a reference to the base class:

```
```csharp
MyDerivedClass d = new MyDerivedClass();
d.Message(); // prints "MyDerivedClass".
```
```