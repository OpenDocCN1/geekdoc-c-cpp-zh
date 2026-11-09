
```csharp
return @delegate.GetDelegate();
        }
    }
```

Now, we can look at my `WeakEventHandler` class:

```csharp
// This class provides support for the non-generic EventHandler delegate
public sealed class WeakEventHandler : WeakDelegate<EventHandler> {
    public WeakEventHandler(EventHandler @delegate) : base(@delegate) { }

    /// <summary>Returns a reference to the non-generic EventHandler delegate</summary>
    public override EventHandler GetDelegate() { return Callback; }

    // This private method must match the desired delegate's signature
    private void Callback(Object sender, EventArgs e) {
        // If the target hasn't been GC'd invoke it
        var eh = base.GetRealDelegate();
        if (eh != null) eh(sender, e);
    }
}
```

Solving this weak delegate problem turned out to be much more challenging than I first expected it to be. The CLR and C# have a lot of limitations that I had to work around; this makes the code bigger and more complex than I would have liked. Here are some of the problems:

- I want my `WeakDelegate` class to have its `TDelegate` generic argument constrained to accept only delegate objects that are derived from `System.MulticastDelegate`. However, C# doesn't allow you to constrain a generic argument to `MulticastDelegate` or even `System.Delegate` (the base class of `MulticastDelegate`). Therefore, the best I can do is constrain `TDelegate` to `class` (that is, any reference type).
- I wanted to have a `WeakDelegate` object automatically remove itself from the delegate chain that it is a member of when it sees that its target delegate has been garbage collected. However, a delegate has no way to know what chain it is a member of.
- I also thought about passing an event (like the `Button`'s `Click` event) to `WeakDelegate`'s constructor. Then I could have code inside my `WeakDelegate` class that automatically removes the `WeakDelegate` object from the event, but there is no way to create a variable that refers to an event. Therefore, the user of a `WeakDelegate` class can optionally set the `RemoveDelegateCode` property to some delegate referring to code that knows how to remove the delegate from a delegate chain or an event; at least I can pass the `WeakDelegate` object's delegate to remove into this code.
- The CLR treats each delegate type as different types and so you can't cast a reference to one delegate type to another delegate type even if the delegate types have the same signature. For example, I'd like to cast a reference to an `EventHandler` delegate to an `EventHandler<EventArgs>` delegate since these delegate signatures are actually identical. But the CLR treats these as different types, and the cast is not allowed.

Microsoft's CLR team knows about this delegate limitation and is considering ways to allow delegates with the same signature to be equivalent in a future version of the CLR. Due to this limitation, a different class has to be defined for each delegate's type.

I already showed you the `WeakEventHandler` type that corresponds to the `EventHandler` delegate. I also have a `WeakEventHandler<TEventArgs>` type that corresponds to the `EventHandler<TEventArgs>` delegate type:

```csharp
// This WeakDelegate partial class provides support for the
// generic EventHandler<TEventArgs> delegate
public sealed class WeakEventHandler<TEventArgs> :
    WeakDelegate<EventHandler<TEventArgs>> where TEventArgs : EventArgs {

    public WeakEventHandler(EventHandler<TEventArgs> @delegate) : base(@delegate) { }

    /// <summary>
    /// Returns a reference to the generic
    /// EventHandler<TEventArgs> delegate
    /// </summary>
    public override EventHandler<TEventArgs> GetDelegate() { return Callback; }

    private void Callback(Object sender, TEventArgs e) {
        // If the target hasn't been GC'd invoke it
        var eh = base.GetRealDelegate();
        if (eh != null) eh(sender, e);
    }
}
```

If the CLR would treat delegate types that have the same signature as equivalent, I could use my `WeakEventHandler<TEventArgs>` type for non-generic `EventHandler` events, and I could delete my `WeakEventHandler` class entirely.

It would actually be pretty cool if the .NET Framework included a weak reference delegate mechanism, but no such thing exists today. However, it has been discussed by the CLR team at Microsoft, and it is likely that something like that will be part of a future version. If the CLR had first-class support for it, then they could easily work around all the limitations that I had to deal with, which would make the implementation easier to use and more efficient.

> **Important** When developers start learning about weak references, they immediately start thinking that they are useful in caching scenarios. For example, they think it would be cool to construct a bunch of objects that contain a lot of data and then to create weak references to these objects. When the program needs the data, the program checks the weak reference to see if the object that contains the data is still around, and if it is, the program just uses it; the program experiences high performance. However, if a garbage collection occurs, the objects that contain the data will be destroyed, and when the program has to re-create the data, the program experiences lower performance.

> The problem with this technique is the following: Garbage collections do not occur when memory is full or close to full. Instead, garbage collections occur whenever generation 0 is full, which occurs approximately after every 256 KB of memory is allocated. So objects are being tossed out of memory much more frequently than desired, and your application's performance suffers greatly.

Weak references can be used quite effectively in caching scenarios, but building a good cache algorithm that finds the right balance between memory consumption and speed is very complex. Basically, you want your cache to keep strong references to all of your objects and then, when you see that memory is getting tight, you start turning strong references into weak references. Currently, the CLR offers no mechanism to notify an application that memory is getting tight. But some people have had much success by periodically calling the Win32 `GlobalMemoryStatusEx` function and checking the returned `MEMORYSTATUSEX` structure's `dwMemoryLoad` member. If this member reports a value above 80, memory is getting tight, and you can start converting strong references to weak references based on whether you want a least-recently used algorithm, a most-frequently used algorithm, a time-based algorithm, or whatever.

Developers frequently want to associate a piece of data with another entity. For example, you can associate data with a thread or with an `AppDomain`. It is also possible to associate data with an individual object by using the `System.Runtime.CompilerServices.ConditionalWeakTable<TKey,TValue>` class, which looks like this:

```csharp
public sealed class ConditionalWeakTable<TKey, TValue>
    where TKey : class where TValue : class {
    public ConditionalWeakTable();
    public void    Add(TKey key, TValue value);
    public TValue  GetValue(TKey key, CreateValueCallback<TKey, TValue> createValueCallback);
    public Boolean TryGetValue(TKey key, out TValue value);
    public TValue  GetOrCreateValue(TKey key);
    public Boolean Remove(TKey key);

    public delegate TValue CreateValueCallback(TKey key);   // Nested delegate definition
}
```

If you want to associate some arbitrary data with one or more objects, you would first create an instance of this class. Then, call the `Add` method passing in a reference to some object for the `key` parameter and the data you want to associate with the object in the `value` parameter. If you attempt to add a reference to the same object more than once, the `Add` method throws an `ArgumentException`; to change the value associated with an object, you must remove the key and then add it back in with the new value. Note that this class is thread-safe so multiple threads can use it concurrently, although this means that the performance of the class is not stellar; you should test the performance of this class to see how well it works for your scenario. Also, there is no good reason why `TValue` is constrained to class (only reference types). In the future, the CLR team might remove the constraint on `TValue` so that you can associate value type instances with an object without having to box the value types.

Of course, a table object internally stores a `WeakReference` to the object passed in as the key; this ensures that the table doesn't forcibly keep the object alive. But what makes the `ConditionalWeakTable` class so special is that it guarantees that the value remains in memory as long as the object identified by the key is in memory. So this is more than a normal `WeakReference` because if it were, the value could be garbage collected even though the key object continued to live. The `ConditionalWeakTable` class could be used to implement the dependency property mechanism of Silverlight and Windows Presentation Foundation.
