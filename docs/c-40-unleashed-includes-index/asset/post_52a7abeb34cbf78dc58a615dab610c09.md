
## Yielding to Others

When a thread has run out of juice, it can voluntarily yield its turn for code execution to others. This is most likely the closest you can get to native thread control from the .NET Framework, because this function corresponds closely to an equivalent Win32 API with the same purpose.

As you can guess, the method to realize a yield is called Yield. Like most methods for threading, it's a static method that applies to the current thread. In other words, you can yield your own turn to execute code but not some other thread's:

```
// Have done some work, but can take a nap now...
Thread.Yield();
// At some point, we'll be scheduled again and end up here...
```

When a yield operation occurs, another thread that's ready to execute will be picked by the operating system scheduler to run. It should be emphasized that yielding is an act that's carried out explicitly by a thread.

Threads can be switched out in favor of others for multiple reasons that are beyond the direct control of the thread. For example, a thread can become blocked waiting for I/O to complete, or a thread's quantum can be expired. Context switches as a result of such situations are under the control of the OS scheduler directly (although one can argue that issuing an I/O operation is more or less "asking" to be scheduled away in case of the occurrence of blocking).

### COOPERATIVE SCHEDULING

Yielding is a weak form of cooperative scheduling. Today's common operating systems employ preemptive scheduling to switch out a thread if the thread's quantum expires. The operating system scheduler plays the role of a big brother that's watching everything that happens on the system and always has the power, by piggybacking on clock interrupts, to switch between threads.

Prior to preemptive scheduling, applications had to be well behaved to yield execution time to one another in an explicit manner. It goes without saying that relying on the kindness of others is not evident. More often than not, a single program could run away and monopolize the system for itself. That said, some systems still employ cooperative scheduling for good reasons. One example is the SQL Server OS, where the user mode scheduler relies on the cooperation of various parts of the system to avoid blocking and expensive context switching.

Thread.Yield could be argued to be a weak form of cooperative scheduling in that a thread can decide not to use its full quantum, which gets enforced by the OS's preemptive scheduler. Although a thread can yield, it doesn't pose any problem if it doesn't because the preemptive scheduler is there to pause a thread if it has run for long enough.

## Interrupting a Blocked Thread

Another life cycle method available for the control of threads is Interrupt, which is an instance method. It can be used to interrupt a thread that's in a so-called WaitSleepJoin state. This state is characterized by being blocked because of a wait due to the use of the lock keyword (or the underlying Monitor class), a thread sleep, or the use of the Join method discussed before.

When calling Interrupt on a thread that's currently in any of the aforementioned states, a ThreadInterruptedException will occur in the target thread. As usual, if the exception goes unhandled, the target thread will die. Working with this interrupt mechanism therefore requires threads to be prepared to be interrupted, which can work well in a controlled environment.

As with the Abort method, the occurrence of an exception in a target thread at some unexpected point of execution is quite unnatural. Personally, I use Interrupt rarely. If its goal is to wake up threads from a blocked state to shut down an application in its entirety, gentler techniques are often available. Although we haven't talked about (synchronization) events yet, you should have no trouble understanding that waking up a thread that's waiting for an event can be accomplished by signaling that event. However, a signal typically indicates a resource being available for use, which won't be the case if the event is signaled simply to unblock the thread:

```
sharedFile.WaitOne(); // See later for a discussion of WaitOne.
// When some thread sets the sharedFile event, we'll execute this code.
```

A similar example could be given using the lock keyword. Possible ways to discover why the event was signaled include a check for some “stopping” flag (that's set before signaling the event in case of setting the event to unblock the thread) or the use of multiple events and the WaitAny construct (discussed in the section, “Synchronization Primitives”). In short, Interrupt has its use (although rather seldom).

## Managed Thread Characteristics

Being layered on top of native threads, managed threads are in some sense richer than just native threads. For example, the state a managed thread can be in introduces a number of managed code-specific states, such as WaitSleepJoin discussed in the previous section. Besides those differences, a whole lot of properties on Thread reveal a lot of useful information about threads. Some of those thread settings can also be set to control their behavior.

## Background Versus Foreground

A first useful property of managed threads is whether they are foreground threads or background threads. The difference between both concepts is minimal. The only altered behavior of a background thread is that it won't keep the process from being terminated after all foreground threads have quit. In other words, a foreground thread can keep a process alive until it exits, whereas a background thread can't. For example, consider the following fragment of code where two threads are running, one of which has been configured as a background thread. The other thread uses the default setting for IsBackground, which is set to false:

```
static void Main()
{
    var t1 = new Thread(() =>
    {
        for (int i = 0; i < 10; i++)
        {
            Console.WriteLine("Background says {0}", i);
            Thread.Sleep(500);
        }
    }) { IsBackground = true };

    var t2 = new Thread(() =>
    {
        for (int i = 0; i < 10; i++)
        {
            Console.WriteLine("Foreground says {0}", i);
            Thread.Sleep(100);
        }
    });

    t1.Start();
    t2.Start();
}
```

This code prints all the messages from the foreground thread, which is keeping the process alive. However, when the foreground thread completes in about 1 second, the background thread won’t have a chance to execute further because the sole thread that kept the process alive has exited.

Notice there are three threads in this example: the two that have been created using our code, and one for the main thread. Can you infer whether the main thread is foreground or background? Observe how the Main method can finish without taking down the process. Why is that? Because some foreground thread keeps the process alive.

What happens if the main thread is still going but all other threads in the program have finished? Clearly, you don’t want your program’s main thread to be terminated abruptly because some of your other threads have finished their duties. In other words, the main thread needs to keep the process alive as well, having a chance to reach its end. That’s exactly what it means to be a foreground thread:

```
static void Main(string[] args)
{
    // Prints false
    Console.WriteLine(Thread.CurrentThread.IsBackground);
}
```

Typically, background threads are used to monitor the state of some component or other process. Such activities don't need to keep the program alive and are typically just meant to support the rest of the program. Marking such threads as background is a good practice.

You learn later, in the “Thread Pools” section, that thread pool threads are background threads. Similarly, advanced scenarios where native code creates threads will also cause them to be marked as background threads right from the start. Concerning exception behavior, no difference exists between background and foreground threads: Unhandled exceptions in either of them terminate the entire process. We cover exceptions in the “Dealing with Exceptions” section.

## Giving Threads a Name

Debugging applications with a lot of threads can be a painful undertaking, especially if a lot of those threads are doing similar activities (for instance, processing user requests coming in from the network). Giving threads a friendly name definitely helps you see the forest for the trees. For this purpose, the string-valued Name property can be used:

```
var monitor1 = new Thread(() =>
{
    while (true)
    {
        Console.WriteLine("Monitor 1 heartbeat");
        // Do something more useful every second...
        Thread.Sleep(1000);
    }
}) { IsBackground = true, Name = "Monitoring thread 1" };

// ...
monitor1.Start();

// Prevent the main thread from exiting for the sample...
Console.ReadLine();
```

The preceding example shows how to tag the monitoring thread with a friendly name. This name shows up in the Threads window in Visual Studio, as shown in Figure 29.7. The additional threads that show up in this display are due to the use of the Visual Studio hosting process for debugging. Feel free to compare the outcome with and without the hosting process enabled. To disable the hosting process, see the project properties Debug tab.

Also notice how the code window marks where a thread currently is by using a gray background. In this particular snapshot of the process execution, one of the monitoring threads is in the Thread.Sleep call, as indicated in gray.

To make threads more explicit in the debugger, you can right-click anywhere in the Threads window and enable the Show Threads in Source option. Figure 29.8 shows threads being identified in the source by a threads icon in the margin.
