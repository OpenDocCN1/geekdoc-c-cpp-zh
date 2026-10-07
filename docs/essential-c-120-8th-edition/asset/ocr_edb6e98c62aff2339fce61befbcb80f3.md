# Using the System.Threading.Interlocked Class

The mutual exclusion pattern described so far provides the minimum set of tools for handling synchronization within a process (application domain). However, synchronization with System.Threading.Monitor is a relatively expensive operation, and an alternative solution that the processor supports directly targets synchronization patterns.

Listing 22.6 sets _Data to a new value as long as the preceding value was null. As indicated by the method name, this pattern is the compare/exchange pattern. Instead of placing a lock around behaviorally equivalent compare and exchange code, the Interlocked.CompareExchange() provides a built-in method for a synchronous operation that does the same for a value (null) and updates the first parameter if the value is equal to the second parameter. Table 22.2 shows other synchronization methods supported by Interlocked.

Listing 22.6: Synchronization Using System.Threading.Interlocked

```
public class SynchronizationUsingInterlocked
{
    private static object? _Data;

    // Initialize data if not assigned
    public static void Initialize(object newValue)
    {
        // If _Data is null then set it to newValue
        Interlocked.CompareExchange(
            ref _Data, newValue, null);
    }
    
    // ...
}
```

# TABLE 22.2: Interlocked's Synchronization-Related Methods

| Method Signature | Description |
| public static T CompareExchange<T>(T location, T value, T comparand); | Checks location for the value in comparand. If the values are equal, it sets location to value and returns the original data stored in location. |