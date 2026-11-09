If multiple threads call **GetSingleton** simultaneously, then this version might create two (or more) **Singleton** objects. However, the call to **Interlocked.CompareExchange** ensures that only one of the references is ever published into the **s_value** field. Any object not rooted by this field will be garbage collected later on. Since, in most applications, it is unlikely that multiple threads will call **GetSingleton** at the same time, it is unlikely that more than one **Singleton** object will ever be created.

Now it might upset you that multiple **Singleton** objects could be created, but there are many benefits to this code. First, it is very fast. Second, it never blocks a thread; if a thread pool thread is blocked on a **Monitor** or any other kernel-mode thread synchronization construct, then the thread pool creates another thread to keep the CPUs saturated with work. So now, another megabyte or more of memory is allocated and initialized and all the DLLs get a thread attach notification. With **CompareExchange**, this can never happen. Of course, you can use this technique only when the constructor has no side effects.

The FCL offers two types that encapsulate the patterns described in this section. The generic **System.Lazy** class looks like this (some methods are not shown):

```
public class Lazy<T> {
    public Lazy(Func<T> valueFactory, LazyThreadSafetyMode mode);
    public Boolean IsValueCreated { get; }
    public T Value { get; }
}
```

This code demonstrates how it works:

```
public static void Main() {
    // Create a lazy-initialization wrapper around getting the DateTime
    Lazy<String> s = new Lazy<String>(
        () => DateTime.Now.ToLongTimeString(),
        LazyThreadSafetyMode.PublicationOnly);

    Console.WriteLine(s.IsValueCreated);      // Returns false since Value not queried yet
    Console.WriteLine(s.Value);               // The delegate is invoked now
    Console.WriteLine(s.IsValueCreated);      // Returns true since Value was queried
    Thread.Sleep(10000);                      // Wait 10 seconds and display the time again
    Console.WriteLine(s.Value);               // The delegate is NOT invoked now; same result
}
```

When I run this, I get the following output:

```
False
2:40:42 PM
True
2:40:42 PM    ← Notice that the time did not change 10 seconds later
```

The code above constructed an instance of the **Lazy** class and passed one of the **LazyThreadSafetyMode** flags into it. Here is what these flags look like and what they mean: