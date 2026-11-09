(WPF). It can also be used internally by dynamic languages to dynamically associate data with objects.

Here is some code that demonstrates the use of the **ConditionalWeakTable** class. It allows you to call the **GCWatch** extension method on any object passing in some **String** tag. Then it notifies you via the console window whenever that particular object gets garbage collected:

```
```csharp
internal static class ConditionalWeakTableDemo {
    public static void Main() {
        Object o = new Object().GCWatch("My Object created at " + DateTime.Now);
        GC.Collect();      // We will not see the GC notification here
        GC.KeepAlive(o);   // Make sure the object o refers to lives up to here
        o = null;          // The object that o refers to can die now

        GC.Collect();      // We'll see the GC notification here
    }
}

internal static class GCWatcher {
    // NOTE: Be careful with Strings due to interning and MarshalByRefObject proxy objects
    private readonly static ConditionalWeakTable<Object, NotifyWhenGCd<String>> s_cwt =
        new ConditionalWeakTable<Object, NotifyWhenGCd<String>>();

    private sealed class NotifyWhenGCd<T> {
        private readonly T m_value;

        internal NotifyWhenGCd(T value) { m_value = value; }
        public override string ToString() { return m_value.ToString(); }
        ~NotifyWhenGCd() { Console.WriteLine("GC'd: " + m_value); }
    }

    public static T GCWatch<T>(this T @object, String tag) where T : class {
        s_cwt.Add(@object, new NotifyWhenGCd<String>(tag));
        return @object;
    }
}
```
```

# # Resurrection

When we talked about finalization, you'll recall that when an object requiring finalization is considered dead, the garbage collector forces the object back to life so that its **Finalize** method can be called. Then, after its **Finalize** method is called, the object is permanently dead. To summarize: An object requiring finalization dies, lives, and then dies again. Bringing a dead object back to life is called *resurrection*.

The act of preparing to call an object's **Finalize** method is a form of resurrection. When the garbage collector places a reference to the object on the freachable queue, the object is now reachable from a root and has come back to life. This is required so that the code in the **Finalize** method can access the object's fields. Eventually, the object's **Finalize** method returns, no roots point to the object because it is removed from the freachable queue, and the object is dead forever after.