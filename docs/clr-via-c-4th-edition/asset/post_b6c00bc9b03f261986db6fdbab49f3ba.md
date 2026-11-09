
references; it doesn't support the behavior provided by GCHandle instances allocated with a GCHandleType of Normal or Pinned. The downside of the WeakReference<T> class is that an instance of it must be allocated on the heap. So the WeakReference<T> class is a heavier-weight object than a GCHandle instance.

> **Important** When developers start learning about weak references, they immediately start thinking that they are useful in caching scenarios. For example, they think it would be cool to construct a bunch of objects that contain a lot of data and then to create weak references to these objects. When the program needs the data, the program checks the weak reference to see if the object that contains the data is still around, and if it is, the program just uses it; the program experiences high performance. However, if a garbage collection occurred, the objects that contained the data would be destroyed, and when the program has to re-create the data, the program experiences lower performance.
>
> The problem with this technique is the following: garbage collections do not only occur when memory is full or close to full. Instead, garbage collections occur whenever generation 0 is full. So objects are being tossed out of memory much more frequently than desired, and your application's performance suffers greatly.
>
> Weak references can be used quite effectively in caching scenarios, but building a good cache algorithm that finds the right balance between memory consumption and speed is very complex. Basically, you want your cache to keep strong references to all of your objects and then, when you see that memory is getting tight, you start turning strong references into weak references. Currently, the CLR offers no mechanism to notify an application that memory is getting tight. But some people have had much success by periodically calling the Win32 GlobalMemoryStatusEx function and checking the returned MEMORYSTATUSEX structure's dwMemoryLoad member. If this member reports a value above 80, memory is getting tight, and you can start converting strong references to weak references based on whether you want a least-recently used algorithm, a most-frequently used algorithm, a time-based algorithm, or whatever.

Developers frequently want to associate a piece of data with another entity. For example, you can associate data with a thread or with an AppDomain. It is also possible to associate data with an individual object by using the System.Runtime.CompilerServices.ConditionalWeakTable<TKey,TValue> class, which looks like this.

```csharp
public sealed class ConditionalWeakTable<TKey, TValue>
   where TKey : class
   where TValue : class {
   public ConditionalWeakTable();
   public void Add(TKey key, TValue value);
   public TValue GetValue(TKey key, CreateValueCallback<TKey, TValue> createValueCallback);
   public Boolean TryGetValue(TKey key, out TValue value);
   public TValue GetOrCreateValue(TKey key);
   public Boolean Remove(TKey key);

   public delegate TValue CreateValueCallback(TKey key);   // Nested delegate definition
}
```

If you want to associate some arbitrary data with one or more objects, you would first create an instance of this class. Then, call the Add method, passing in a reference to some object for the key parameter and the data you want to associate with the object in the value parameter. If you attempt to add a reference to the same object more than once, the Add method throws an ArgumentException; to change the value associated with an object, you must remove the key and then add it back in with the new value. Note that this class is thread-safe so multiple threads can use it concurrently, although this means that the performance of the class is not stellar; you should test the performance of this class to see how well it works for your scenario.

Of course, a table object internally stores a WeakReference to the object passed in as the key; this ensures that the table doesn't forcibly keep the object alive. But what makes the ConditionalWeakTable class so special is that it guarantees that the value remains in memory as long as the object identified by the key is in memory. So this is more than a normal WeakReference because if it were, the value could be garbage collected even though the key object continued to live. The ConditionalWeakTable class could be used to implement the dependency property mechanism used by XAML. It can also be used internally by dynamic languages to dynamically associate data with objects.

Here is some code that demonstrates the use of the ConditionalWeakTable class. It allows you to call the GCWatch extension method on any object passing in some String tag. Then it notifies you via the console window whenever that particular object gets garbage collected.

```csharp
internal static class ConditionalWeakTableDemo {
   public static void Main() {
      Object o = new Object().GCWatch("My Object created at " + DateTime.Now);
      GC.Collect();      // We will not see the GC notification here
      GC.KeepAlive(o);   // Make sure the object o refers to lives up to here
      o = null;          // The object that o refers to can die now

      GC.Collect();      // We'll see the GC notification sometime after this line
      Console.ReadLine();
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

## CLR Hosting and AppDomains

**In this chapter:**

- CLR Hosting ........................................ 554
- AppDomains ........................................ 556
- AppDomain Unloading ............................... 570
- AppDomain Monitoring .............................. 571
- AppDomain First-Chance Exception Notifications .... 573
- How Hosts Use AppDomains .......................... 574
- Advanced Host Control ............................. 576

In this chapter, I'll discuss two main topics that really show off the incredible value provided by the Microsoft .NET Framework: *hosting* and *AppDomains*. Hosting allows any application to use the features of the common language runtime (CLR). In particular, this allows existing applications to be at least partially written with managed code. Furthermore, hosting allows applications the ability to offer customization and extensibility via programming.

Allowing extensibility means that third-party code will be running inside your process. In Windows, loading a third party's DLLs into a process has been fraught with peril. The DLL could easily have code in it that could compromise the application's data structures and code. The DLL could also try to use the security context of the application to gain access to resources that it should not have access to. The CLR's AppDomain feature solves all of these problems. AppDomains allow third-party untrusted code to run in an existing process, and the CLR guarantees that the data structures, code, and security context won't be exploited or compromised.

Programmers typically use hosting and AppDomains along with assembly loading and reflection. Using these four technologies together makes the CLR an incredibly rich and powerful platform. In this chapter, I'll focus on hosting and AppDomains. In the next chapter, I'll focus on assembly loading and reflection. When you learn and understand all of these technologies, you'll see how your investment in the .NET Framework today will certainly pay off down the line.
