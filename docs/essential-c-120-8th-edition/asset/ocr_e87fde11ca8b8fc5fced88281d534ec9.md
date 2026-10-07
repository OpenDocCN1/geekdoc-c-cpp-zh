# Why Synchronization? 1051

By locking the section of code accessing _Count (using either lock or Monitor), you make the Main() and Decrement() methods safe, meaning they can be safely called from multiple threads simultaneously.\3

The price of synchronization is a reduction in performance. Listing 22.4, for example, takes an order of magnitude longer to execute than 22.1 does, which demonstrates lock's relatively slow execution compared to the execution of incrementing and decrementing the count.

Even when lock is insignificant in comparison with the work it synchronizes, programmers should avoid indiscriminate synchronization so as to avoid the possibility of deadlocks and unnecessary synchronization on multiprocessor computers that could be executing code in parallel. The general best practice for object design is to synchronize mutable static state, but not any instance data. (There is no need to synchronize something that never changes.) Programmers who allow multiple threads to access a particular object must provide synchronization for the object. Any class that explicitly deals with threads is likely to want to manage threads safe to some extent.

# BEGINNER TOPIC

# Task Return with No await

In Listing 22.1, although Task.Run() => Decrement() returns a Task, the await operator is not used. The reason for this is that prior to C# 7.1, Main() didn't support the use of async. Given C# 7.1, however, the code can be refactored to the use of async/await pattern, as shown in Listing 22.5.

Listing 22.5: async Main() with C# 7.1

```
using System;
using System.Threading.Tasks;

public class Program
{
```

+   3. Prior to C# 4.0, the concept was the same but the compiler-itted code depended on the lockTaken-less Monitor.Enter() method, and the Monitor.Enter() called was emitted before the try block.