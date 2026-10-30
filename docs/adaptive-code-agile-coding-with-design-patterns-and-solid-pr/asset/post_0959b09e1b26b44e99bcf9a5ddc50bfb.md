
implementations of an interface as instances of that interface. In the example shown in Listing 7-15, the CompositeComponent instances provided are of different types, further enhancing this pattern's utility.

# LISTING 7-15 Instances provided to the composite can be of different types.

```
public class SecondTypeOfLeaf : IComponent
{
    public void Something()
    {
    }
}
// . . .
public class AThirdLeafType : IComponent
{
    public void Something()
    {
    }
}
// . . .
public void AlternativeComposite()
{
    var composite = new CompositeComponent();
    composite.AddComponent(new Leaf());
    composite.AddComponent(new SecondTypeOfLeaf());
    composite.AddComponent(new AThirdLeafType());

    component = composite;
    composite.Something();
}
```

Taking this pattern to its logical conclusion, you can even pass in one or more instances of the CompositeComponent interface to the Add method, forming a chain of composite instances in a hierarchical tree structure.

In Chapter 3, “Dependencies and layering,” classes were modeled as object graphs. That theme continues here, to further demonstrate how the Composite pattern works. In Figure 7-6, the nodes of the graph represent object instances, and the edges represent method calls.

![](img/f852e0a12c174e64d91a8e1a05146eab_261_0.png)

FIGURE 7-6 The object graph notation helps to visualize the runtime structure of the program.

# Predicate decorators

The predicate decorator is a useful construct for hiding the conditional execution of code from clients.

Listing 7-16 shows an example.

LISTING 7-16 This client will execute only the Something method on even days of the month.

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
```

```
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

The presence of the DateTester class in this example is a dependency that does not belong in this class. The initial temptation is to alter the code toward that of Listing 7-17. However, that is only a partial solution.

# LISTING 7-17 An improvement is to require the dependency to be passed into the class.

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
    {
      component.Something();
    }
  }

  private readonly IComponent component;
}
```

You now require a parameter of the Run method, breaking the client’s public interface and burdening its clients with providing an implementation of the DateTester class. By using the Decorator pattern, you are able to keep the client’s interface the same, yet retain the conditional-execution functionality. Listing 7-18 proves that this is not too good to be true.

# LISTING 7-18 The predicate decoration contains the dependency, and the client is much cleaner.

```
public class PredicatedComponent : IComponent
{
    public PredicatedComponent(IComponent decoratedComponent, DateTester dateTester)
    {
        this.decoratedComponent = decoratedComponent;
        this.dateTester = dateTester;
    }

    public void Something()
    {
        if(dateTester.TodayIsAnEvenDayOfTheMonth)
        {
            decoratedComponent.Something();
        }
    }

    private readonly IComponent decoratedComponent;
    private readonly DateTester dateTester;
}
// . . .
class PredicatedDecoratorExample
{
    public PredicatedDecoratorExample(IComponent component)
    {
        this.component = component;
    }

    public void Run()
    {
        component.Something();
    }

    private readonly IComponent component;
}
```

Note that this listing has added conditional branching to the code without modifying either the client code or the original implementing class. Also, this example has accepted the DateTester class as a dependency, but you could take this one step further by defining your own predicate interface for handling this scenario generically. After a few changes, the code looks like Listing 7-19.

# LISTING 7-19 Defining a dedicated IPredicate interface makes the solution more general.

```
public interface IPredicate
{
    bool Test();
}
// . . .
public class PredicatedComponent : IComponent
```

```
```csharp
{
    public PredicatedComponent(IComponent decoratedComponent, IPredicate predicate)
    {
        this.decoratedComponent = decoratedComponent;
        this.predicate = predicate;
    }

    public void Something()
    {
        if (predicate.Test())
        {
            decoratedComponent.Something();
        }
    }

    private readonly IComponent decoratedComponent;
    private readonly IPredicate predicate;
}
// . . .
public class TodayIsAnEvenDayOfTheMonthPredicate : IPredicate
{
    public TodayIsAnEvenDayOfTheMonthPredicate(DateTester dateTester)
    {
        this.dateTester = dateTester;
    }

    public bool Test()
    {
        return dateTester.TodayIsAnEvenDayOfTheMonth;
    }

    private readonly DateTester dateTester;
}
```
```

The TodayIsAnEvenDayOfTheMonthPredicate class converts the original dependent class, DateTester, to that of an IPredicate. This is an example of the Adapter pattern that was discussed earlier, in the “Refactoring for abstraction” section, and in Chapter 4, “Interfaces and design patterns.”

> **Note** The .NET Framework, as of version 2.0, contains a Predicate<T> delegate, which models a predicate that accepts a single, generic parameter as a context. I did not choose the Predicate<T> delegate for this example for two reasons: First, no context needs to be provided, because the original conditional test accepted no arguments. However, I could have used a Func<bool> delegate to model a context-free predicate, which brings me to the second reason: *delegates are not as versatile as interfaces*. By modeling an IPredicate, I will be able to decorate that interface just the same as any other in the future. In other words, I have defined another extension point that is infinitely decoratable.

## 1.1 从自然数到有理数

我们已经学过自然数、整数、分数等数的概念，并会用它们表示现实生活中的一些数量。

为了满足生活、生产与数学自身进一步发展的需要，数的概念在不断地扩展。例如，在小学里我们学过分数，就是由于测量和等分整体时，结果常常不是整数，于是引进了分数。

在七年级上册，我们学习了有理数，并且知道整数和分数统称为有理数。那么，有理数够用了吗？下面我们来看一个例子。

如图1-1，将一个边长为1的正方形，沿两组对边分别剪开，得到四个大小相同的小正方形，每个小正方形的面积为多少？

![](img/f852e0a12c174e64d91a8e1a05146eab_265_0.png)

设每个小正方形的面积为x，则x²=1/4，所以x=1/2。

如果设每个小正方形的边长为a，则a²=1/4，所以a=1/2。

如果设每个小正方形的对角线长为b，则b²=1/2，所以b=√2/2。

在上面的问题中，我们遇到了√2/2这样的数，它不是有理数，那么它是什么数呢？

事实上，在解决许多实际问题时，我们会遇到一些不是有理数的数。例如，圆的周长与直径的比值π，也是一个不是有理数的数。

为了满足生活、生产与数学自身进一步发展的需要，数的概念再一次扩展，我们将在本章学习一种新的数——无理数，并将有理数扩充到实数。

# Lazy decorators

The lazy decorator allows clients to be provided with a reference to an interface that will not be instantiated until its first use. Typically, and erroneously, clients are made aware of the presence of a lazy instance because a Lazy<T> is passed to them, as in Listing 7-21.

LISTING 7-21 This client has been given a Lazy<T>.

```
public class ComponentClient
{
    public ComponentClient(Lazy<IComponent> component)
    {
        this.component = component;
    }

    public void Run()
    {
        component.Value.Something();
    }

    private readonly Lazy<IComponent> component;
}
```

This client has no option but to accept that all instances of IComponent that it is provided with will be lazy. However, if you return to a more standard use of the interface, you can create a lazy decorator that prevents the client from knowing that it is dealing with a Lazy<T>, and allows some ComponentClient objects to accept IComponent instances that are not lazy. Listing 7-22 shows this decorator.

LISTING 7-22 LazyComponent implements a lazily instantiated IComponent, but ComponentClient is unaware of this.

```
public class LazyComponent : IComponent
{
    public LazyComponent(Lazy<IComponent> lazyComponent)
    {
        this.lazyComponent = lazyComponent;
    }

    public void Something()
    {
        lazyComponent.Value.Something();
    }

    private readonly Lazy<IComponent> lazyComponent;
}
// ...
public class ComponentClient
{
```
