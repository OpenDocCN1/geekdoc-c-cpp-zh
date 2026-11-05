# Chapter 162: Garbage Collector in .Net

# Section 162.1: Weak References

In .NET, the GC allocates objects when there are no references left to them. Therefore, while an object can still be reached from code (there is a strong reference to it), the GC will not allocate this object. This can become a problem if there are a lot of large objects.

A weak reference is a reference, that allows the GC to collect the object while still allowing to access the object. A weak reference is valid only during the indeterminate amount of time until the object is collected when no strong references exist. When you use a weak reference, the application can still obtain a strong reference to the object, which prevents it from being collected. So weak references can be useful for holding on to large objects that are expensive to initialize, but should be available for garbage collection if they are not actively in use.

Simple usage:

```
WeakReference reference = new WeakReference(new object(), false);

GC.Collect();

object target = reference.Target;
if (target != null)
    DoSomething(target);
```

So weak references could be used to maintain, for example, a cache of objects. However, it is important to remember that there is always the risk that the garbage collector will get to the object before a strong reference is reestablished.

Weak references are also handy for avoiding memory leaks. A typical use case is with events.

Suppose we have some handler to an event on a source:

```
Source.Event += new EventHandler(Handler)
```

This code registers an event handler and creates a strong reference from the event source to the listening object. If the source object has a longer lifetime than the listener, and the listener doesn't need the event anymore when there are no other references to it, using normal .NET events causes a memory leak: the source object holds listener objects in memory that should be garbage collected.

In this case, it may be a good idea is to use the Weak Event Pattern.

Something like:

```
public static class WeakEventManager
{
    public static void SetHandler<S, TArgs>(
        Action<EventHandler<TArgs>> add,
        Action<EventHandler<TArgs>> remove,
        S subscriber,
        Action<S, TArgs> action)
        where TArgs : EventArgs
        where S : class
    {
        var subscrWeakRef = new WeakReference(subscriber);
        EventHandler<TArgs> handler = null;
```