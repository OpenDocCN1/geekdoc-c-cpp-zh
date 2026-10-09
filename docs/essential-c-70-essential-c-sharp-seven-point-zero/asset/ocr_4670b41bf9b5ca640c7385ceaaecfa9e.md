TABLE 20.3: Execution Path with ManualResetEvent Synchronization

| Main() | DoWork() |
| :--- | :--- |
| `...` | |
| `Console.WriteLine(` | |
| `"Application started....");` | |
| `Task task = new Task(DoWork);` | |
| `Console.WriteLine(` | |
| `"Starting thread....");` | |
| `task.Start();` | |
| `DoWorkSignaledResetEvent.Wait();` | `Console.WriteLine(` |
| | `"DoWork() started....");` |
| | `DoWorkSignaledResetEvent.Set();` |
| `Console.WriteLine(` | `MainSignaledResetEvent.Wait();` |
| `"Thread executing...");` | |
| `MainSignaledResetEvent.Set();` | |
| `task.Wait();` | `Console.WriteLine(` |
| | `"DoWork() ending....");` |
| `Console.WriteLine(` | |
| `"Thread completed");` | |
| `Console.WriteLine(` | |
| `"Application exiting...");` | |

Calling a reset event's `Wait()` method (for a `ManualResetEvent`, it is called `WaitOne()`) blocks the calling thread until another thread signals and allows the blocked thread to continue. Instead of blocking indefinitely, `Wait()`/`WaitOne()` overrides include a parameter, either in milliseconds or as a `TimeSpan` object, for the maximum amount of time to block. When specifying a timeout period, the return from `WaitOne()` will be `false` if the timeout occurs before the reset event is signaled. `ManualResetEvent.Wait()` also includes a version that takes a cancellation token, allowing for cancellation requests as discussed in Chapter 19.

The difference between `ManualResetEventSlim` and `ManualResetEvent` is that the latter uses kernel synchronization by