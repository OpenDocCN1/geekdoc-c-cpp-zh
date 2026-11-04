```
```csharp
Console.WriteLine("Source is " + source);
Console.WriteLine();
}

class Y {
    public void Handler<T,V>(T source, V arg) where V : MyEventArgs {
        Console.WriteLine("Event " + arg.EventNum + " received by a Y object.");
        Console.WriteLine("Source is " + source);
        Console.WriteLine();
    }
}

class UseGenericEventDelegate {
    static void Main() {
        X ob1 = new X();
        Y ob2 = new Y();
        MyEvent evt = new MyEvent();
        // Add Handler() to the event list.
        evt.SomeEvent += ob1.Handler;
        evt.SomeEvent += ob2.Handler;
        // Fire the event.
        evt.OnSomeEvent();
        evt.OnSomeEvent();
    }
}
```
```

The output is show here:

```
```
Event 0 received by an X object.
Source is MyEvent

Event 0 received by a Y object.
Source is MyEvent

Event 1 received by an X object.
Source is MyEvent

Event 1 received by a Y object.
Source is MyEvent
```
```

# Generic Interfaces

In addition to generic classes and methods, you can also have generic interfaces. Generic interfaces are specified just like generic classes. Here is an example that reworks the ISeries interface developed in Chapter 12. (Recall that ISeries defines the interface to a class that generates a series of numbers.) The data type upon which it operates is now specified by a type parameter.