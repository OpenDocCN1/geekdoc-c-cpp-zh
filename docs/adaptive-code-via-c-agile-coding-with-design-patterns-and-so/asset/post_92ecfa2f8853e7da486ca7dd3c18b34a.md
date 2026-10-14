
![](img/65c1bad7a6b3cffae8cbb79664f0708b_110_0.png)

**FIGURE 2-25** Domain models should only be used for handling commands.

Querying data often needs to be fast and is allowed to provide few guarantees of transactional consistency: phantom reads or nonrepeatable reads can be an acceptable trade-off for increased responsiveness. Command processing, though, is often required to have transactional consistency, hence the differing layers in place to handle commands and queries. Sometimes, the data access layers can also differ between commands and queries. A fully ACID-compliant (ACID stands for atomic, consistent, isolated, durable) database might be needed for commands, whereas simple document storage might suffice for queries. The document storage would be updated asynchronously by events published from the command layer, giving eventual consistency to the query reads.

## Conclusion

This chapter has shown how the organization of dependencies presents a significant problem when creating software applications. The long-term health, adaptability, and possibly the viability of a project relies on sound management of dependencies. A mess of spaghetti-like interdependencies will occur if developers create classes that reference each other without careful consideration, which can seriously affect a team’s ability to deliver business value in a consistent, predictable fashion.

Dependencies must be managed at all levels, from individual classes and methods interacting with each other, through assembly references, to the high-level architecture of components. Developers must be constantly vigilant that spurious dependencies do not leak outside of their method, class, assembly, or layer.

In some ways, this chapter underpins a lot of the content of the rest of this book. The content provides a solid foundation for maintainable, adaptive code that is reinforced with each chapter. If your assemblies are a spaghetti of references, and your layers do not hide their infrastructural dependencies, your code will become harder to test, amend, and understand, no matter what other patterns or practices you attempt to follow.

## Chapter 3. Interfaces and design patterns

## After completing this chapter, you will be able to

- Define interfaces and identify the primary ways in which they differ from classes.
- Apply design patterns, such as the Adapter and Strategy patterns, to interfaces.
- Understand an interface’s versatility through duck-typing, mixins, and fluent interfaces.
- Identify the limitations of interfaces and implement workarounds.
- Spot common anti-patterns and abuses of interfaces.

The interface is a powerful construct in Microsoft .NET Framework development. Although the interface keyword is very simple, what it represents is a very powerful paradigm. When used correctly, interfaces provide your code with the extension points that make it extremely adaptive. However, some uses of interfaces are not so good; yet they remain in common use.

This chapter provides a reminder of the differences between classes and interfaces and describes how best to use the two together both to protect client code from implementation changes and to facilitate polymorphism.

It also covers the versatility of interfaces and how they are a ubiquitous tool in modern software solutions. This encompasses some powerful design patterns that, when applied correctly (in conjunction with other patterns in this book), yield code that is incredibly flexible and able to adapt to the changing requirements that Agile projects embrace.

Interfaces alone are, however, no panacea. A judicious sprinkling of interfaces can certainly help a project, but the interfaces must be applied in the correct manner. This chapter explores some of the common abuses of interfaces.

## What is an interface?

An interface defines the behavior that a class has, but not how this behavior is implemented.

Interfaces stand as separate constructs from classes, but they require a class to provide the working code to fulfill the interface.

Interfaces are defined by their syntax—that is, the language-construct side of the interface: the interface keyword and everything that this implies and entails. But they are also defined by their features: the concepts that they represent and enable.

## Syntax

Interfaces are defined by using the interface keyword. They can contain properties, methods, and events, just as classes can. However, no element of an interface can be given an access modifier: the implementing class must implement an interface as public. Listing 3-1 shows the declaration of an interface, along with a possible implementation.

## LISTING 3-1 Declaring and implementing an interface

Click here to view code image

```csharp
public interface ISimpleInterface
{
    void ThisMethodRequiresImplementation();

    string ThisStringPropertyNeedsImplementingToo
    {
        get;
        set;
    }

    int ThisIntegerPropertyOnlyNeedsAGetter
    {
        get;
    }

    public event EventHandler<EventArgs> InterfacesCanContainEventsToo;
}
//...
public class SimpleInterfaceImplementation : ISimpleInterface
{

    public void ThisMethodRequiresImplementation()
    {

    }

    public string ThisStringPropertyNeedsImplementingToo
    {
        get;
        set;
    }

    public int ThisIntegerPropertyOnlyNeedsAGetter
    {
        get
        {
            return this.encapsulatedInteger;
        }
        set
        {
            this.encapsulatedInteger = value;
        }
    }

    event EventHandler<EventArgs> InterfacesCanContainEventsToo = delegate {};
```

```csharp
private int encapsulatedInteger;
}
```

The .NET Framework does not support the concept of multiple inheritance of classes, but it does support multiple interface implementation for a single class.

There is no limit imposed on the number of interfaces that a class can implement; the number of interfaces that really make sense on one class is more of a practical concern. Listing 3-2 extends the prior example to implement a second interface on the implementing class.

## LISTING 3-2 Multiple interfaces can be implemented by a single class

Click here to view code image

```csharp
public interface IInterfaceOne
{
    void MethodOne();
}
//...
public interface IInterfaceTwo
{
    void MethodTwo();
}
//...
public class ImplementingMultipleInterfaces : IInterfaceOne, IInterfaceTwo
{
    public void MethodOne()
    {
    }

    public void MethodTwo()
    {
    }
}
```

Though there can be multiple interfaces implemented on a single class, a single interface can similarly be implemented multiple times by different classes.

## Multiple inheritance

Some languages support the concept of inheriting from multiple base classes. C++, in particular, allows this construct. However, .NET Framework languages do not permit it, and the compiler will generate a warning if a class attempts to inherit from two or more classes, as Figure 3-1 shows.

![](img/65c1bad7a6b3cffae8cbb79664f0708b_115_0.png)

**FIGURE 3-1** Multiple inheritance is prevented by the compiler.

## Diamond inheritance problem

One reason that multiple inheritance is disallowed is because of the diamond inheritance problem. This problem occurs when two or more classes are inherited by the same class. If each of those base classes contains identical methods, which one should be used? Figure 3-2 shows a Unified Modeling Language (UML) diagram of the problem.

![](img/65c1bad7a6b3cffae8cbb79664f0708b_115_1.png)

**FIGURE 3-2** A UML diagram showing the diamond inheritance problem.

In this case, which version of `RootMethod()` should class `AttemptedMultipleInheritance` inherit—the one that `BaseClassOne` inherited from `RootClass`, or the one that `BaseClassTwo` inherited from `RootClass`? Because of this ambiguity, the .NET Framework does not allow multiple inheritance of classes.

## Explicit implementation

Interfaces can also be implemented *explicitly*. Explicit interface implementation differs from implicit interface implementation, which is what was shown in the previous examples. Listing 3-3 shows the same example class from before, but this time it implements its interface explicitly.

## LISTING 3-3 Implementing an interface explicitly

Click here to view code image

```csharp
public class ExplicitInterfaceImplementation : ISimpleInterface
{
    public ExplicitInterfaceImplementation()
    {
        this.encapsulatedInteger = 4;
    }

    void ISimpleInterface.ThisMethodRequiresImplementation()
    {
        encapsulatedEvent(this, EventArgs.Empty);
    }

    string ISimpleInterface.ThisStringPropertyNeedsImplementingToo
    {
        get;
        set;
    }

    int ISimpleInterface.ThisIntegerPropertyOnlyNeedsAGetter
    {
        get
        {
            return encapsulatedInteger;
        }
    }

    event EventHandler<EventArgs> ISimpleInterface.InterfacesCanContainEventsToo
    {
        add { encapsulatedEvent += value; }
        remove { encapsulatedEvent -= value; }
    }

    private int encapsulatedInteger;
    private event EventHandler<EventArgs> encapsulatedEvent;
}
```
