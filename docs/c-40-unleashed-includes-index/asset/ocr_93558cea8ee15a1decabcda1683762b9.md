# Yielding to Others

When a thread has run out of juice, it can voluntarily yield its turn for code execution to others. This is most likely the closest you can get to native thread control from the .NET Framework, because this function corresponds closely to an equivalent Win32 API with the same purpose.

As you can guess, the method to realize a yield is called Yield. Like most methods for threading, it's a static method that applies to the current thread. In other words, you can yield your own turn to execute code but not some other thread's:

```
// Have done some work, but can take a nap now...
Thread.Yield();
// At some point, we'll be scheduled again and end up here...
```

When a yield operation occurs, another thread that's ready to execute will be picked by the operating system scheduler to run. It should be emphasized that yielding is an act that's carried out explicitly by a thread.

Threads can be switched out in favor of others for multiple reasons that are beyond the direct control of the thread. For example, a thread can become blocked waiting for I/O to complete, or a thread's quantum can be expired. Context switches as a result of such situations are under the control of the OS scheduler directly (although one can argue that issuing an I/O operation is more or less "asking" to be scheduled away in case of the occurrence of blocking).

# COOPERATIVE SCHEDULING

Yielding is a weak form of cooperative scheduling. Today's common operating systems employ preemptive scheduling to switch out a thread if the thread's quantum expires. The operating system scheduler plays the role of a big brother that's watching everything that happens on the system and always has the power, by piggybacking on clock interrupts, to switch between threads.

Prior to preemptive scheduling, applications had to be well behaved to yield execution time to one another in an explicit manner. It goes without saying that relying on the kindness of others is not evident. More often than not, a single program could run away and monopolize the system for itself. That said, some systems still employ cooperative scheduling for good reasons. One example is the SQL Server OS, where the user mode scheduler relies on the cooperation of various parts of the system to avoid blocking and expensive context switching.

Thread.Yield could be argued to be a weak form of cooperative scheduling in that a thread can decide not to use its full quantum, which gets enforced by the OS's preemptive scheduler. Although a thread can yield, it doesn't pose any problem if it doesn't because the preemptive scheduler is there to pause a thread if it has run for long enough.