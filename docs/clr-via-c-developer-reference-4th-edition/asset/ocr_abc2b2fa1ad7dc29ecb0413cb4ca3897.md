The preceding code constructed an instance of the Lazy and passed one of the Lazy-ThreadSafety flags into it. Here is what these flags look like and what they mean.

```
public enum LazyThreadSafetyMode {
    None,
    ExecutionAndPublication PublicationOnly,
    // No-thread-safety support at all (good for GUI apps)
    // Uses the double-check locking technique
    // Uses the Interlocked.CompareExchange technique
```

In some memory-constrained scenarios, you might not even want to create an instance of the Lazy class. Instead, you can call static methods of the System.Threading.LazyInitializer. The class looks like this.

```
public static class LazyInitializer {
    // These two methods use Interlocked.CompareExchange:
    public static T EnsureInitialized<T>(ref T target) where T : class;
    public static T EnsureInitialized<T>(ref T target, Func<T> valueFactory) where T : class;

    // These two methods use synclock to Monitor's Enter and Exit internally
    public static T EnsureInitialized<T>(ref T target, Boolean initialized, ref object synclock);
    public static T EnsureInitialized<T>(ref T target, Boolean initialized, ref object synclock, Func<T> valueFactory);
```

Also, being able to explicitly specify a synchronization object to the EnsureInitialized-synclock parameter allows multiple initialization functions and fields to be protected by the same lock.

Here is an example using this class.

```
public static void Main() {
    String name = null;
    // Because name is null, the delegate runs and initializes name
    LazyInitializer.EnsureInitialized(ref name, () => "Jeffrey");
    Console.WriteLine(name); // Displays "Jeffrey"

    // Because name is not null, the delegate does not run; name doesn't change
    LazyInitializer.EnsureInitialized(ref name, () => "Richter");
    Console.WriteLine(name); // Also displays "Jeffrey"
```

# The Condition Variable Pattern

Let's say that a thread waits to execute some code when a complex condition is true. One option would be to let the thread spin continuously, wasting CPU time, and it is also not possible to atomically test multiple variables that are making up the complex condition. Fortunately, there is a pattern that allows threads to efficiently synchronize their operations based on a complex condition.