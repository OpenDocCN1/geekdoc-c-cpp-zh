used for multicast delegates with no target methods is to avoid heap allocations for every empty event. There’s another side to this, as well: the field required for an event’s multicast delegate object. For example, in 99.99% of cases, developers only handle the Click event of a button control. For Windows Form’s Button, that’s 1 out of 68 events on the control, which would lead to 67 null references that are a pure waste of memory. Manual implementation of our own add and remove accessors comes to the rescue here.

Before going any further, note that this manual implementation of add and remove accessors is something you’ll rarely have to do unless you plan on designing systems with a very large number of events where memory footprint becomes very significant. To get an idea of the scale of frameworks we’re talking about here, notice that the two concrete implementations of such an idea I am aware of are Windows Forms and Windows Presentation Foundation (WPF).

So let’s give it a try and design a little efficient event management system. Instead of keeping storage fields for each multicast delegate, we’re going to store an object’s event handlers in a dictionary. Each available event gets represented by a unique key. The value associated with that key determines the event handler, while the absence of an entry in the dictionary indicates no handlers are present for that event. Let’s keep things a bit abstract for the sake of discussion and assume we have a class like this:

```
```csharp
class Bar {
    public event Action A1, A2, A3, A4, A5, A6, A7, A8;
}
```
```

Each instance of Bar has eight compiler-generated storage fields for Action delegates to keep the handlers for A1 through A8 in. When no event handlers are attached, that’s eight wasted references. For 10 instances of Bar, that adds up to a total of 80.

With a dictionary, we get the following picture:

```
```csharp
class Bar {
    static readonly object s_keyA1 = new object();
    // ...
    static readonly object s_keyA8 = new object();

    private Dictionary<object, Delegate> _handlers = /* TODO */;

    public event Action A1 {
        add { /* TODO */ }
        remove { /* TODO */ }
    }
    // ...
    public event Action A8 {
        add { /* TODO */ }
        remove { /* TODO */ }
    }
}
```
```