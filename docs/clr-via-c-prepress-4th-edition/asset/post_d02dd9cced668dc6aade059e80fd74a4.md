
removed from the event's list of delegates. If a match isn't found, no error occurs, and the list is unaltered.

By the way, C# requires your code to use the += and -= operators to add and remove delegates from the list. If you try to call the add or remove methods explicitly, the C# compiler produces the CS0571 "cannot explicitly call operator or accessor" error message.

### Explicitly Implementing an Event

The System.Windows.Forms.Control type defines about 70 events. If the Control type implemented the events by allowing the compiler to implicitly generate the add and remove accessor methods and delegate fields, every Control object would have 70 delegate fields in it just for the events! Since most programmers care about just a few events, an enormous amount of memory would be wasted for each object created from a Control-derived type. By the way, the ASP.NET System.Web.UI.Control and the Windows Presentation Foundation (WPF) System.Windows.UIElement type also offer many events that most programmers do not use.

In this section, I discuss how the C# compiler allows a class developer to explicitly implement an event, allowing the developer to control how the add and remove methods manipulate the callback delegates. I'm going to demonstrate how explicitly implementing an event can be used to efficiently implement a class that offers many events. However, there are certainly other scenarios where you might want to explicitly implement a type's event.

To efficiently store event delegates, each object that exposes events will maintain a collection (usually a dictionary) with some sort of event identifier as the key and a delegate list as the value. When a new object is constructed, this collection is empty. When interest in an event is registered, the event's identifier is looked up in the collection. If the event identifier is there, the new delegate is combined with the list of delegates for this event. If the event identifier isn't in the collection, the event identifier is added with the delegate.

When the object needs to raise an event, the event identifier is looked up in the collection. If the collection doesn't have an entry for the event identifier, nothing has registered interest in the event and no delegates need to be called back. If the event identifier is in the collection, the delegate list associated with the event identifier is invoked. Implementing this design pattern is the responsibility of the developer who is designing the type that defines the events; the developer using the type has no idea how the events are implemented internally.

Here is an example of how you could accomplish this pattern. First, I implemented an EventSet class that represents a collection of events and each event's delegate list as follows:

```csharp
using System;
using System.Collections.Generic;

// This class exists to provide a bit more type safety and
// code maintainability when using EventSet

public sealed class EventKey { }

public sealed class EventSet {
    // The private dictionary used to maintain EventKey -> Delegate mappings
    private readonly Dictionary<EventKey, Delegate> m_events =
        new Dictionary<EventKey, Delegate>();

    // Adds an EventKey -> Delegate mapping if it doesn't exist or
    // combines a delegate to an existing EventKey
    public void Add(EventKey eventKey, Delegate handler) {
        Monitor.Enter(m_events);
        Delegate d;
        m_events.TryGetValue(eventKey, out d);
        m_events[eventKey] = Delegate.Combine(d, handler);
        Monitor.Exit(m_events);
    }

    // Removes a delegate from an EventKey (if it exists) and
    // removes the EventKey -> Delegate mapping if the last delegate is removed
    public void Remove(EventKey eventKey, Delegate handler) {
        Monitor.Enter(m_events);
        // Call TryGetValue to ensure that an exception is not thrown if
        // attempting to remove a delegate from an EventKey not in the set
        Delegate d;
        if (m_events.TryGetValue(eventKey, out d)) {
            d = Delegate.Remove(d, handler);

            // If a delegate remains, set the new head else remove the EventKey
            if (d != null) m_events[eventKey] = d;
            else m_events.Remove(eventKey);
        }
        Monitor.Exit(m_events);
    }

    // Raises the event for the indicated EventKey
    public void Raise(EventKey eventKey, Object sender, EventArgs e) {
        // Don't throw an exception if the EventKey is not in the set
        Delegate d;
        Monitor.Enter(m_events);
        m_events.TryGetValue(eventKey, out d);
        Monitor.Exit(m_events);

        if (d != null) {
            // Because the dictionary can contain several different delegate types,
            // it is impossible to construct a type-safe call to the delegate at
            // compile time. So, I call the System.Delegate type's DynamicInvoke
            // method, passing it the callback method's parameters as an array of
            // objects. Internally, DynamicInvoke will check the type safety of the
            // parameters with the callback method being called and call the method.
            // If there is a type mismatch, then DynamicInvoke will throw an exception.
            d.DynamicInvoke(new Object[] { sender, e });
        }
    }
}
```

## 2020年度报告

本报告总结了公司2020年的主要业绩和发展情况。

- 收入增长20%
- 客户满意度提升15%
- 新拓展3个市场

| 指标 | 数值 |
| --- | --- |
| 收入 | $10M |
| 利润 | $2M |

![](img/3f2c86949cdef7e2f9e27c37c607b28e_262_0.png)

> 2020年是充满挑战与机遇的一年。

Code that uses the TypeWithLotsOfEvents type can't tell whether the events have been implemented implicitly by the compiler or explicitly by the developer. They just register the events using normal syntax. Here is some code demonstrating this:

```csharp
public sealed class Program {
    public static void Main() {
        TypeWithLotsOfEvents twle = new TypeWithLotsOfEvents();

        // Add a callback here
        twle.Foo += HandleFooEvent;

        // Prove that it worked
        twle.SimulateFoo();
    }

    private static void HandleFooEvent(object sender, FooEventArgs e) {
        Console.WriteLine("Handling Foo Event here...");
    }
}
```

## Chapter 12

## Generics

In this chapter:

- Generics in the Framework Class Library — 281
- Generics Infrastructure — 282
- Generic Interfaces — 289
- Generic Delegates — 290
- Delegate and Interface Contravariant and Covariant Generic Type Arguments — 291
- Generic Methods — 293
- Generics and Other Members — 296
- Verifiability and Constraints

Developers who are familiar with object-oriented programming know the benefits it offers. One of the big benefits that make developers extremely productive is code reuse, which is the ability to derive a class that inherits all of the capabilities of a base class. The derived class can simply override virtual methods or add some new methods to customize the behavior of the base class to meet the developer's needs. Generics is another mechanism offered by the common language runtime (CLR) and programming languages that provides one more form of code reuse: algorithm reuse.

Basically, one developer defines an algorithm such as sorting, searching, swapping, comparing, or converting. However, the developer defining the algorithm doesn't specify what data type(s) the algorithm operates on; the algorithm can be generically applied to objects of different types. Another developer can then use this existing algorithm as long as he or she indicates the specific data type(s) the algorithm should operate on, for example, a sorting algorithm that operates on Int32s, Strings, etc., or a comparing algorithm that operates on DateTimes, Versions, etc.

Most algorithms are encapsulated in a type, and the CLR allows the creation of generic reference types as well as generic value types, but it does not allow the creation of generic enumerated types. In addition, the CLR allows the creation of generic interfaces and generic delegates. Occasionally, a single method can encapsulate a useful algorithm, and therefore, the CLR allows the creation of generic methods that are defined in a reference type, value type, or interface.

Let's look at a quick example. The Framework Class Library (FCL) defines a generic list algorithm that knows how to manage a set of objects; the data type of these objects is not specified by the generic algorithm. Someone wanting to use the generic list algorithm can specify the exact data type to use with it later.

The FCL class that encapsulates the generic list algorithm is called List<T> (pronounced List of Tee), and this class is defined in the System.Collections.Generic namespace. Here is what this class definition looks like (the code is severely abbreviated):

```csharp
[Serializable]
public class List<T> : IList<T>, ICollection<T>, IEnumerable<T>,
    IList, ICollection, IEnumerable {

    public List();
    public void Add(T item);
    public Int32 BinarySearch(T item);
    public void Clear();
    public Boolean Contains(T item);
    public Int32 IndexOf(T item);
    public Boolean Remove(T item);
    public void Sort();
    public void Sort(IComparer<T> comparer);
    public void Sort(Comparison<T> comparison);
    public T[] ToArray();

    public Int32 Count { get; }
    public T this[Int32 index] { get; set; }
}
```

The programmer who defined the generic List class indicates that it works with an unspecified data type by placing the <T> immediately after the class name. When defining a generic type or method, any variables it specifies for types (such as T) are called type parameters. T is a variable name that can be used in source code anywhere a data type can be used. For example, in the List class definition, you see T being used for method parameters (the Add method accepts a parameter of type T) and return types (the ToArray method returns a single-dimension array of type T). Another example is the indexer method (called this in C#). The indexer has a get accessor method that returns a value of type T and a set accessor method that accepts a parameter of type T. Since the T variable can be used anywhere that a data type can be specified, it is also possible to use T when defining local variables inside a method or when defining fields inside a type.
