```
// The protected property allows derived types access to the collection.
protected EventSet { get { return m_eventSet; } }
```

```
#Region to support the Foo event (repeat this pattern for additional events)
// Define the members for the Foo event.
// 2a. Create a static, read-only object to identify this event.
// Each object has its own hash code for looking up this
// event's delegate linked list in the object's collection.
protected static readonly EventKey s_fooEventKey = new EventKey();
```

```
// 2b. Define the event's accessor methods that add/remove
// from the collection.
public event EventHandler<FooEventArgs> Foo {
    add m_eventSet.Add(s_fooEventKey, value);
    remove m_eventSet.Remove(s_fooEventKey, value);
}
```

```
// 2c. Define the protected, virtual On method for this event.
protected virtual void OnFoo(FooEventArgs e) {
    m_eventSet.Raise(s_fooEventKey, this);
}
```

```
// 2d. Define the method that translates input to this event.
public void SimulateFoo() { OnFoo(new FooEventArgs()); };
#endregion
```

Code that uses the TypeWithLotsOfEvents type can't tell whether the events have been implemented by the compiler or explicitly by the developer. They just register the events by normal syntax. Here is some code demonstrating this.

```
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