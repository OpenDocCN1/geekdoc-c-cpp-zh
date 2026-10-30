
```csharp
public string Property
{
    get
    {
        // We can do some mutation here after retrieving the value
        return decoratedComponent.Property;
    }
    set
    {
        // And/or here, before we set the value
        decoratedComponent.Property = value;
    }
}

private readonly IComponent decoratedComponent;
```

Listing 7-32 shows the manual creation of an event, but rather than having a backing field, for both the adder and remover this code delegates to the decorated instance of the interface.

## Listing 7-32 Events can also use the Decorator pattern, just like methods.

```csharp
public class ComponentDecorator : IComponent
{
    public ComponentDecorator(IComponent decoratedComponent)
    {
        this.decoratedComponent = decoratedComponent;
    }

    public event EventHandler Event
    {
        add
        {
            // We can do something here, when the event handler is registered
            decoratedComponent.Event += value;
        }
        remove
        {
            // And/or here, when the event handler is deregistered
            decoratedComponent.Event -= value;
        }
    }

    private readonly IComponent decoratedComponent;
}
```

## Conclusion

The single responsibility principle has a hugely positive impact on the adaptability of code. Compared to equivalent code that does not adhere to the principle, SRP-compliant code leads to a greater number of classes that are smaller and more directed in scope. Where there would otherwise have been a single class or suite of classes with interdependencies and a confusion of responsibility, the SRP introduces order and clarity.

The SRP is primarily achieved through abstracting code behind interfaces and delegating responsibility for unrelated functionality to whichever implementation happens to be behind the interface at run time. Some design patterns are excellent at supporting efforts to strictly regiment the SRP—in particular, the Adapter pattern and the Decorator pattern. The former enables much of your code to maintain first-party references to interfaces under your direct control, although in reality using a third-party library. The latter can be applied whenever some of a class’s functionality needs to be removed but it is too tightly coupled with the intent of the class to stand alone.

What this chapter did not cover is how all of these classes are orchestrated at run time. Passing interfaces into constructors was taken for granted in this chapter, but Chapter 12 describes a variety of ways in which this can be accomplished.

## The open/closed principle

**After completing this chapter, you will be able to**

- Understand different interpretations of the open/closed principle.
- Treat SOLID code as append-only.
- Compare and contrast different class extension-point mechanisms.
- Use protected variation as a guideline for extension points.

The oxymoronic nature of the open/closed principle causes some confusion. Its pithy name suggests code that is permissive but at the same time restrictive. The fact that there are several variations of the definition serves only to cloud matters further.

Picking one definition over another and using it alone would be remiss. Rather, this chapter compares each definition and its consequences to try to distill the principle down to its essence. The goal is a very useful guideline that will enable you to create code that is more adaptive to future changes.

## Introduction to the open/closed principle

There are two definitions of the open/closed principle that must be examined, the original coining from the 1980s and a more contemporary definition. The latter seeks to elaborate on the former by giving it more context and clarifying the principle's scope.

## The Meyer definition

Bertrand Mayer, in his 1988 book, *Object-Oriented Software Construction* (Prentice Hall), defined the open/closed principle (OCP) as follows:

> *Software entities should be open for extension, but closed for modification.*

The Meyer definition is the most commonly cited definition of the principle, but there is a second: the Martin definition.

- 2. The source code is *modified* so that the unit test passes. The bug-fix exception to the OCP becomes necessary at this juncture because, without it, you would not be able to modify any existing code. Editing the system under test allows you to transition the failing test from red to green—from failure to success. When you ensure that no other tests are failing as a side effect, the bug is fixed.

## Client awareness

A more permissive exception to the “closed for modification” rule is that any change to existing code is allowed as long as it does not also require a change to any client of that code. This places an emphasis on how coupled the software modules are, at all levels of granularity: between classes and classes, assemblies and assemblies, and subsystems and subsystems.

If a change in one class forces a change in another, the two are said to be *tightly* coupled. Conversely, if a class can change in isolation without forcing other classes to change, the participating classes are *loosely* coupled. At all times and at all levels, loose coupling is preferable. Maintaining loose coupling limits the impact that the OCP has if you allow modifications to existing code that do not force further changes to clients.

## Extension points

Now that the “closed for modification” rule of the OCP is clarified, the “open for extension” rule can be considered. Classes that honor the OCP should be open to extension by containing defined extension points where future functionality can hook into the existing code and provide new behaviors.

Some options for different kinds of extension points are detailed in this section, with their pros and cons explored. These examples continue the TradeProcessor example of the previous chapters, this time from the point of view of the client interacting with the class.

## Code without extension points

First, what does code look like when it has no extension points? Figure 8-1 shows what happens when a class that has no extension points needs new functionality.

![](img/f852e0a12c174e64d91a8e1a05146eab_277_0.png)

**FIGURE 8-1** When there are no extension points, clients are forced to change.

The TradeProcessorClient depends directly on the TradeProcessor class. A new requirement is handed to you, resulting in necessary changes to the TradeProcessor class. Without modifying the original class, you create a new version (TradeProcessorVersion2) that contains the new functionality as specified in your new requirement. Because the client directly depends on the TradeProcessor class, and because of the lack of extension points in the TradeProcessor class, you need to place the new functionality inside a new class. The side effect of this change is that the TradeProcessorClient must be edited so that it depends on the new version of the class. It seems like it would just be easier to allow you to edit the existing TradeProcessor, doesn’t it?

If you allow changes to existing code where they have no client impact, you might not have to create an entirely new version of the TradeProcessor. If the ProcessTrades method signature were to change, this would not simply be an implementation change for the class, it would also be an interface change. All interface changes force client changes because clients are tightly coupled to the interfaces of their dependencies.

## Virtual methods

An alternative implementation for the TradeProcessor class contains an extension point: the ProcessTrades method is virtual. Figure 8-2 shows how the three classes are now arranged.

![](img/f852e0a12c174e64d91a8e1a05146eab_278_0.png)

**FIGURE 8-2** The client depends on the TradeProcessor class, which can be extended via inheritance.

Any class that marks one of its members as virtual is open to extension. This type of extension is via implementation inheritance. When your requirement for a new feature in the TradeProcessor class arrives, you can subclass the existing TradeProcessor and—without modifying its source code—alter the ProcessTrades method.

The TradeProcessorClient does not need to change in this case, because you can use polymorphism to supply the client with the new version of the TradeProcessor and have it call the subclass’s implementation of the ProcessTrades method.
