
## SRP and the Decorator pattern

The Decorator pattern is excellent for ensuring that each class has a single responsibility. Classes can often do too many things without an obvious way of splitting the responsibilities into other classes. The responsibilities seem too closely linked.

The Decorator pattern’s basic premise is that each decorator class fulfills the contract of a type and also accepts one or more of those types as constructor parameters. This is beneficial because functionality can be added to an existing class that implements a certain interface, and the decorator also acts—unbeknownst to clients—as an implementation of the required interface. [Figure 5-4](#figure-5-4) shows a UML diagram of the Decorator design pattern.

![](img/65c1bad7a6b3cffae8cbb79664f0708b_208_0.png)

**FIGURE 5-4** A UML diagram showing an implementation of the Decorator pattern.

A simple example of the pattern is shown in [Listing 5-13](#listing-5-13), which does not pertain to a specific use of the pattern but provides a canonical example.

**LISTING 5-13** A template example of the decorator pattern.

[Click here to view code image](#code-image)

```csharp
public interface IComponent
{
    void Something();
}
// . . .
public class ConcreteComponent : IComponent
{
    public void Something()
    {
    }
}
// ...
public class DecoratorComponent : IComponent
{
    public DecoratorComponent(IComponent decoratedComponent)
    {
        this.decoratedComponent = decoratedComponent;
    }

    public void Something()
    {
        SomethingElse();
        decoratedComponent.Something();
    }

    private void SomethingElse()
    {

    }

    private readonly IComponent decoratedComponent;
}
// ...
class Program
{
    static IComponent component;

    static void Main(string[] args)
    {
        component = new DecoratorComponent(new ConcreteComponent());
        component.Something();
    }
}
```

Because a client accepts the interface shown in the listing as a method parameter, you can provide either the original, undecorated type to that client or you can provide the decorated version. Note that the client will be oblivious: it will not have to change depending on which version it is being provided.

## The Composite pattern

The Composite pattern is a specialization of the Decorator pattern and is one of the more common uses of that pattern. A UML diagram describing the Composite pattern’s collaborators is shown in [Figure 5-5](#figure-5-5).

**FIGURE 5-5** The Composite pattern closely resembles the Decorator pattern.

The Composite pattern’s purpose is to allow you to treat many instances of an interface as if they were just one instance. Therefore, clients can accept just one instance of an interface, but they can be implicitly provided with many instances, without requiring the client to change. Listing 5-14 shows a composite decorator in practice.

**LISTING 5-14** The composite implementation of an interface.

Click here to view code image

```
public interface IComponent
{
    void Something();
}
//...
public class Leaf : IComponent
{
    public void Something()
    {
    }
}
//...
public class CompositeComponent : IComponent
{
    public CompositeComponent()
    {
        children = new List<IComponent>();
    }

    public void AddComponent(IComponent component)
    {
        children.Add(component);
    }

    public void RemoveComponent(IComponent component)
    {
        children.Remove(component);
    }

    public void Something()
    {
        foreach(var child in children)
        {
            child.Something();
        }
    }

    private ICollection<IComponent> children;
}
//...
class Program
{
    static void Main(string[] args)
    {
        var composite = new CompositeComponent();
        composite.AddComponent(new Leaf());
        composite.AddComponent(new Leaf());
        composite.AddComponent(new Leaf());

        component = composite;
        component.Something();
    }

    static IComponent component;
}
```

In the CompositeComponent class, there are methods for adding and removing other instances of the IComponent. These methods do not form part of the interface and are for clients of the CompositeComponent class, directly. Whichever factory method or class is tasked with creating instances of the CompositeComponent class will also have to create the decorated instances and pass them into the Add method; otherwise, the clients of the IComponent would have to change in order to cope with compositions.

Whenever the Something method is called by the IComponent clients, the list of composed instances is enumerated, and their respective Something is called. This is how you reroute the call to a single instance of IComponent—of type CompositeComponent—to many other types.

Each instance that you supply to the CompositeComponent class must implement the IComponent interface—and this is enforced by the compiler due to C#’s strong typing—but the instances need not all be of the same concrete type. Because of the advantages of polymorphism, you can treat all implementations of an interface as instances of that interface. In the example shown in Listing 5-15, the CompositeComponent instances provided are of different types, further enhancing this pattern’s utility.

**LISTING 5-15** Instances provided to the composite can be of different types.

Click here to view code image

```
public class SecondTypeOfLeaf : IComponent
{
    public void Something()
    {
    }
}
//...
public class AThirdLeafType : IComponent
{
    public void Something()
    {
    }
}
//...
public void AlternativeComposite()
{
    var composite = new CompositeComponent();
    composite.AddComponent(new Leaf());
    composite.AddComponent(new SecondTypeOfLeaf());
    composite.AddComponent(new AThirdLeafType());

    component = composite;
    composite.Something();
```

Taking this pattern to its logical conclusion, you can even pass in one or more instances of the CompositeComponent interface to the Add method, forming a chain of composite instances in a hierarchical tree structure.

## Where should the composite live?

Chapter 2 introduced the Entourage anti-pattern, which states that implementations should not live in the same assemblies as their interfaces. However, there is an exception to that rule: implementations whose dependencies are a subset of their interface’s dependencies.

Depending on how the composite is implemented, it is likely that no further dependencies will be introduced. If this is true, the assembly in which the interface resides could also include the composite implementation.

In Chapter 2, classes were shown to be modeled as object graphs. That theme continues here, to further demonstrate how the Composite pattern works. In Figure 5-6, the nodes of the graph represent object instances, and the edges represent method calls.

![](img/65c1bad7a6b3cffae8cbb79664f0708b_214_0.png)

**FIGURE 5-6** The object graph notation helps to visualize the runtime structure of the program.

## Predicate decorators

The predicate decorator is a useful construct for hiding the conditional execution of code from clients. Listing 5-16 shows an example.

**LISTING 5-16** This client will only execute the Something method on even days of the month.

Click here to view code image

```
public class DateTester
{
    public bool TodayIsAnEvenDayOfTheMonth
{
    get
    {
        return DateTime.Now.Day % 2 == 0;
    }
}
}
//...
class PredicatedDecoratorExample
{
    public PredicatedDecoratorExample(IComponent component)
    {
        this.component = component;
    }

    public void Run()
    {
        DateTester dateTester = new DateTester();
        if (dateTester.TodayIsAnEvenDayOfTheMonth)
        {
            component.Something();
        }
    }

    private readonly IComponent component;
}
```

The presence of the DateTester class in this example is a dependency that does not belong in this class. The initial temptation is to alter the code toward that of Listing 5-17. However, that is only a partial solution.

**LISTING 5-17** An improvement is to require the dependency to be passed into the class.

Click here to view code image

```
class PredicatedDecoratorExample
{
    public PredicatedDecoratorExample(IComponent component)
    {
        this.component = component;
    }

    public void Run(DateTester dateTester)
    {
        if (dateTester.TodayIsAnEvenDayOfTheMonth)
```
