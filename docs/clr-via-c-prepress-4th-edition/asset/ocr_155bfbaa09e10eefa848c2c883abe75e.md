Here is an example using a method from this class:

```
```csharp
public static void Main() {
   String name = null;
   // Since name is null, the delegate runs and initializes name
   LazyInitializer.EnsureInitialized(ref name, () => "Jeffrey");
   Console.WriteLine(name);   // Displays "Jeffrey"

   // Since name is not null, the delegate does not run; name doesn’t change
   LazyInitializer.EnsureInitialized(ref name, () => "Richter");
   Console.WriteLine(name);   // Also displays "Jeffrey"
}
```
```

# # The Condition Variable Pattern

Let’s say that a thread wants to execute some code when a complex condition is true. One option would be to let the thread spin continuously, repeatedly testing the condition. But this wastes CPU time, and it is also not possible to automatically test multiple variables that are making up the complex condition. Fortunately, there is a pattern that allows threads to efficiently synchronize their operations based on a complex condition. This pattern is called the condition variable pattern, and we use it via the following methods defined inside the Monitor class:

```
```csharp
public static class Monitor {
   public static Boolean Wait(Object obj);
   public static Boolean Wait(Object obj, Int32 millisecondsTimeout);

   public static void Pulse(Object obj);
   public static void PulseAll(Object obj);
}
```
```

Here is what the pattern looks like:

```
```csharp
internal sealed class ConditionVariablePattern {
   private readonly Object m_lock = new Object();
   private Boolean m_condition = false;

   public void Thread1() {
      Monitor.Enter(m_lock);        // Acquire a mutual-exclusive lock

      // While under the lock, test the complex condition "atomically"
      while (!m_condition) {
         // If condition is not met, wait for another thread to change the condition
         Monitor.Wait(m_lock);       // Temporarily release lock so other threads can get it
      }

      // The condition was met, process the data...

      Monitor.Exit(m_lock);          // Permanently release lock
   }

   public void Thread2() {
```
```