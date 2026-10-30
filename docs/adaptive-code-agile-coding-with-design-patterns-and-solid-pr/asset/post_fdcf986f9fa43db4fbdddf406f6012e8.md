
The Class Adapter pattern makes use of inheritance for the adapter—a subclass of the target class needs to be adapted to fit the expected interface of clients. Listing 4-18 shows how this works in practice.

## LISTING 4-18 The Class Adapter pattern uses implementation inheritance.

```
public class Adaptee
{
    public void MethodB()
    {
    }
}
// . . .
public class Adapter : Adaptee
{
    public void MethodA()
    {
        MethodB();
    }
}
// . . .
class Program
{
    static Adapter dependency = new Adapter();
    static void Main(string[] args)
    {
        dependency.MethodA();
    }
}
```

This is the less common of the two types of Adapter pattern, mostly because developers are told to favor composition over inheritance. This is because inheritance, which is whitebox reuse, makes the subclass dependent on the implementation of a class, rather than merely on its interface. Composition, which is blackbox reuse, limits the dependency to the interface, so that the implementation can vary without adversely affecting clients.

> Tip The terms whitebox reuse and blackbox reuse refer to an ability to see into the implementation or have the implementation hidden from inspection, respectively.

## The Object Adapter pattern

The Object Adapter pattern uses composition to delegate from the methods of the interface to those of a contained, encapsulated object. Figure 4-6 shows the collaborating classes and interfaces used in the Object Adapter pattern.

![](img/f852e0a12c174e64d91a8e1a05146eab_158_0.png)

FIGURE 4-6 The UML class diagram for the Object Adapter pattern.

## LISTING 4-19 The adaptor accepts the target class as a constructor parameter and delegates to it.

```
public interface IExpectedInterface
{
    void MethodA();
}
// . . .
public class Adapter : IExpectedInterface
{
    public Adapter(TargetClass target)
    {
        this.target = target;
    }

    public void MethodA()
    {
        target.MethodB();
    }

    private TargetClass target;
}
//
public class TargetClass
{
    public void MethodB()
    {
    }
}
```

```
// . . .
class Program
{
    static IExpectedInterface dependency = new Adapter(new TargetClass());
    static void Main(string[] args)
    {
        dependency.MethodA();
    }
}
```

This is the more common form of the Adapter pattern. The main method uses an IExpectedInterface but, rather than provide a "real" implementation of this interface, an adapter to a different class—TargetClass—is applied. This adapter fulfills the requirements of an IExpectedInterface—a MethodA method—but it delegates this call to TargetClass, rather than doing anything directly itself.

## The Strategy pattern

The Strategy pattern allows you to change the desired behavior of a class based on one or more supplied "strategies." Figure 4-7 shows the UML class diagram for the Strategy pattern.

![](img/f852e0a12c174e64d91a8e1a05146eab_159_0.png)

FIGURE 4-7 The UML class diagram of the Strategy pattern.

The Strategy pattern is used whenever a class needs to exhibit variant behavior depending on the state of an object. If this behavior can change at run time depending on the current state of the class, the Strategy pattern is a perfect fit for encapsulating this variant behavior. Listing 4-20 shows how to create the Strategy pattern and use it in a class.

```
public interface IStrategy
{
    void Execute();
}
// ...
public class ConcreteStrategyA : IStrategy
{
    public void Execute()
    {
        Console.WriteLine("ConcreteStrategyA.Execute()");
    }
}
// ...
public class ConcreteStrategyB : IStrategy
{
    public void Execute()
    {
        Console.WriteLine("ConcreteStrategyB.Execute()");
    }
}
// ...
public class Context
{
    public Context()
    {
        currentStrategy = strategyA;
    }

    public void DoSomething()
    {
        currentStrategy.Execute();

        // swap strategy with each call
        currentStrategy = (currentStrategy == strategyA) ? strategyB : strategyA;
    }

    private readonly IStrategy strategyA = new ConcreteStrategyA();
    private readonly IStrategy strategyB = new ConcreteStrategyB();

    private IStrategy currentStrategy;
}
```

With every call that is made to Context.DoSomething(), the method first delegates to the current strategy and then swaps between strategy A and strategy B. The next call delegates to the newly selected strategy before again swapping back to the original strategy.

The way the strategies are selected is an implementation detail—it does not alter the net effect of the pattern: that the behavior of the class is hidden behind an interface whose implementations are used to perform the real work.

## Further versatility

The utility of interfaces is not limited to design patterns. There are some other, more-specialized uses of interfaces that are worth investigation. Though these features are not generally applicable, there are situations in which they are the right tool for the job.

Just as with design patterns, their overuse can be detrimental to the readability and maintainability of code. It is a difficult balancing act to find the correct number of collaborating patterns and techniques to solve a problem concisely, so exercise caution when using interfaces in the following ways.

## Duck-typing

C# is a statically typed language, whereas duck-typing is more commonly found in dynamically typed languages. Duck-typing uses the “duck test”:

> When I see a bird that walks like a duck and swims like a duck and quacks like a duck, I call that bird a duck.
> 
> —James Whitcomb Riley

Applied to types in a programming language, the duck test suggests that, as long as an object exhibits the behavior of a certain interface, it should be treated as that interface. Unfortunately, this is not true by default in C#. Observe the example in Listing 4-21.

## LISTING 4-21 Although the object Swan fulfills all of the methods of an IDuck, it is, in fact, not an IDuck.

```
public interface IDuck
{
    void Walk();
    void Swim();
    void Quack();
}
// . . .
public class Swan
{
    public void Walk()
    {
        Console.WriteLine("The swan is walking.");
    }
    public void Swim()
    {
```

```
```csharp
Console.WriteLine("The swan can swim like a duck.");
}

public void Quack()
{
    Console.WriteLine("The swan is quacking.");
}
}
// . . .
class Program
{
    static void Main(string[] args)
    {
        var swan = new Swan();

        var swanAsDuck = swan as IDuck;

        if(swan is IDuck || swanAsDuck != null)
        {
            swanAsDuck.Walk();
            swanAsDuck.Swim();
            swanAsDuck.Quack();
        }
    }
}
```
```

The is predicate and the as cast return false and null, respectively. The Common Language Runtime (CLR) does not consider a Swan as being an IDuck, even though it contains the same methods as the interface. A type must *implement* the interface via interface inheritance.

There are a couple of tricks that you can employ to enable the Swan class to be usable as an instance of the IDuck interface without having to implement it. Either you take advantage of the dynamic typing extensions in newer versions of the CLR, or you make use of a third-party library called *Impromptu Interface*.

## Using the Dynamic Language Runtime

As of version 4, the .NET Framework was no longer strictly statically typed. With the introduction of the dynamic keyword, and some supporting types, you can avoid the CLR’s static typing and switch to the dynamic typing of the Dynamic Language Runtime (DLR). An example of dynamic typing in C# is shown in Listing 4-22.

**LISTING 4-22**  The DLR can be used for duck-typing.

```
```csharp
class Program
{
    static void Main(string[] args)
    {
        var swan = new Swan();
```
```

```
DoDuckLikeThings(swan);

Console.ReadKey();
}

static void DoDuckLikeThings(dynamic duckish)
{
    if (duckish != null)
    {
        duckish.Walk();
        duckish.Swim();
        duckish.Quack();
    }
}
```

Notice, however, that the method parameter is of type dynamic. Not only do you need to target the .NET Framework 4, dynamic typing needs to be designed into clients specifically. On both counts, this is sometimes infeasible. You can’t, for example, simply start creating all methods to take dynamic parameters everywhere, or you would be better off using a dynamically typed .NET Framework language, such as IronPython².

## Using Impromptu Interface

Impromptu Interface is a .NET Framework library that can be installed via NuGet. After it is installed, you can use the ActLike<Ts>() method to pass in your Swan and receive an IDuck instance that delegates to your instance. Listing 4-23 shows how this works.

## LISTING 4-23 Impromptu Interface allows duck-typing in C#.

```
class Program
{
    static void Main(string[] args)
    {
        var swan = new Swan();

        var swanAsDuck = Impromptu.ActLike<IDuck>(swan);

        if (swanAsDuck != null)
        {
            swanAsDuck.Walk();
            swanAsDuck.Swim();
            swanAsDuck.Quack();
        }

        Console.ReadKey();
    }
}
```
