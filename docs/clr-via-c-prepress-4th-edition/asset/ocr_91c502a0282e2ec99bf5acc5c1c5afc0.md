```
    public Boolean TryGetTarget(out T target);
    }

```

This class is really just an object-oriented wrapper around a `GCHandle` instance: logically, its constructor calls `GCHandle`'s `Alloc`, its `TryGetTarget` method queries `GCHandle`'s `Target` property, its `SetTarget` method sets `GCHandle`'s `Target` property, and its `Finalize` method (not shown above, since it's protected) calls `GCHandle`'s `Free` method. In addition, no special permissions are required for code to use the `WeakReference<T>` class because the class supports only weak references; it doesn't support the behavior provided by `GCHandle` instances allocated with a `GCHandleType` of `Normal` or `Pinned`. The downside of the `WeakReference<T>` class is that an instance of it must be allocated on the heap. So the `WeakReference<T>` class is a heavier-weight object than a `GCHandle` instance.

**Important** When developers start learning about weak references, they immediately start thinking that they are useful in caching scenarios. For example, they think it would be cool to construct a bunch of objects that contain a lot of data and then to create weak references to these objects. When the program needs the data, the program checks the weak reference to see if the object that contains the data is still around, and if it is, the program just uses it; the program experiences high performance. However, if a garbage collection occurred, the objects that contained the data would be destroyed, and when the program has to re-create the data, the program experiences lower performance.

The problem with this technique is the following: Garbage collections do not occur only when memory is full or close to full. Instead, garbage collections occur whenever generation 0 is full. So objects are being tossed out of memory much more frequently than desired, and your application's performance suffers greatly.

Weak references can be used quite effectively in caching scenarios, but building a good cache algorithm that finds the right balance between memory consumption and speed is very complex. Basically, you want your cache to keep strong references to all of your objects and then, when you see that memory is getting tight, you start turning strong references into weak references. Currently, the CLR offers no mechanism to notify an application that memory is getting tight. But some people have had much success by periodically calling the Win32 `GlobalMemoryStatusEx` function and checking the returned `MEMORYSTATUSEX` structure's `dwMemoryLoad` member. If this member reports a value above 80, memory is getting tight, and you can start converting strong references to weak references based on whether you want a least-recently used algorithm, a most-frequently used algorithm, a time-base algorithm, or whatever.

Developers frequently want to associate a piece of data with another entity. For example, you can associate data with a thread or with an `AppDomain`. It is also possible to associate data with an individual object by using the `System.Runtime.CompilerServices.ConditionalWeakTable<TKey, TValue>` class, which looks like this:

```
    public sealed class ConditionalWeakTable<TKey, TValue>
        where TKey : class where TValue : class {
        public ConditionalWeakTable();
        public void    Add(TKey key, TValue value);
        public TValue GetValue(TKey key, CreateValueCallback<TKey, TValue> createValueCallback);
    }

```