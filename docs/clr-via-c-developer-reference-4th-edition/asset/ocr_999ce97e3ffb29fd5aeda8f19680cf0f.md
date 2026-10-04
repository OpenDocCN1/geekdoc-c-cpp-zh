Using C# fixed statement more efficient that allocating a pinned GC pool. What happens is that the C# compiler emits a special "pinned" flag on the bytes local variable. During a garbage collection, the GC examines the contents of this root, and if the root is not null, it knows not to move the object referred to by variable during the compaction phase. The C# compiler emits IL to initialize an IL instruction to set the bytes local variable back to null at the address of the object of a fixed block, the compiler emits IL until the end of the fixed block that the variable doesn't refer to any object, allowing the object to move when the next garbage collection occurs.

Now, let's talk about the next two flags, Weak and WeakTrackResurrection. These flags can be used in scenarios when interoperating with native code, but they can also be used in scenarios that use only managed code. The Weak flag lets you know when an object has been determined to garbage the object's memory is not guaranteed to be reclaimed. The WeakTrackResurrection flag lets you know when an object's memory has been reclaimed. Of the two, the Weak flag is much more commonly used than the WeakTrackResurrection flag. I've never seen such the WeakTrackResurrection flag in a real application.

Let's say Object-A periodically calls a method on Object-B. However, the fact that Object-A has a reference to Object-B forbids Object-B from being garbage, and in some scenarios, this may not be desired; we want Object-A to call Object-B's method if Object-B is still alive in the managed heap. To accomplish this scenario, GCHandleAlloc passing the reference to Object-B and the Weak flag. Object-A would now just have the returned GCHandle instance instead of the Object-B.

At this point, Object-B can be garbage collected if no roots are keeping it. When Object-A wants to call Object-B's method, it would query GCHandle's read-only Target property. If this property returns a non-null value, then Object-B is still alive. Object-A would then cast the returned to Object-B's type and call the method. If the Target property returns null, then Object-B has been collected (but not finalized) and Object-A would not attempt to call the method. At this point, Object-A's code would probably call GCHandle.Free to relinquish the GCHandle instance.

Because working with the GCHandle type can be a bit cumbersome because it requires elevated to keep or pin an object in memory, the System namespace includes a WeakReference<T> class to help you.

```
public sealed class WeakReference<T> : ISerializable where T : class {
    public WeakReference(T target);
    public WeakReference(T target, bool trackResurrection);
    public void SetTarget(T target);
    public bool GetTarget(out T target)\}
```

This class is really just an object-oriented wrapper around a GCHandle instance: logically, its constructor calls GCHandle.Alloc, its GetTarget method queries GCHandle's Target property, its SetTarget method sets GCHandle's Target property, and its Finalize method protects it. In addition, no special options are required to use the WeakReference<T> class because the class supports only weak