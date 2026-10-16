
model that enables the creation of child tasks, also providing a way to cancel a complete hierarchy.

The cancellation framework offers a standard mechanism that can be used in the same manner with different classes to cancel a task early.

The next chapter gives information about an important concept on using tasks: synchronization.

## 22 Task Synchronization

### What’s In This Chapter?

- Threading issues
- The lock Keyword
- Synchronization with Monitor
- Mutex
- Semaphore and SemaphoreSlim
- ManualResetEvent, AutoResetEvent, and CountdownEvent
- Barrier
- Reader Writer Lock
- Timers

### Wrox.com Code Downloads for This Chapter

The wrox.com code downloads for this chapter are found at www.wrox.com/go/professionalcsharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

- ThreadingIssues
- SynchronizationSamples
- SemaphoreSample
- EventSample
- EventSampleWithCountdownEvent
- BarrierSample
- ReaderWriterLockSample
- WinAppTimer

### Overview

Chapter 21, “Tasks and Parallel Programming,” explains using the Task and Parallel classes to create multithreaded applications. This chapter covers synchronization between multiple processes, tasks, and threads.

It is best when you can avoid synchronization by not sharing data between threads. Of course, this is not always possible. If data sharing is necessary, you must use synchronization techniques so that only one task at a time accesses and changes the shared state. In case you don’t pay attention to synchronization, race conditions and deadlocks can occur. A big issue with these is that errors can occur from time to time.

```
using static System.Console;
```

You can start the sample application ThreadingIssues with command-line arguments to simulate either race conditions or deadlocks.

### Race Conditions

A race condition can occur if two or more threads access the same objects and access to the shared state is not synchronized. To demonstrate a race condition, the following example defines the class StateObject, with an int field and the method ChangeState. In the implementation of ChangeState, the state variable is verified to determine whether it contains 5; if it does, the value is incremented. Trace.Assert is the next statement, which immediately verifies that state now contains the value 6.

After incrementing by 1 a variable that contains the value 5, you might assume that the variable now has the value 6; but this is not necessarily the case. For example, if one thread has just completed the if (_state == 5) statement, it might be preempted, with the scheduler running another thread. The second thread now goes into the if body and, because the state still has the value 5, the state is incremented by 1 to 6. The first thread is then scheduled again, and in the next statement the state is incremented to 7. This is when the race condition occurs and the assert message is shown (code file ThreadingIssues/SampleTask.cs):

```
public class StateObject
{
    private int _state = 5;

    public void ChangeState(int loop)
    {
        if (_state == 5)
        {
            _state++;
            Trace.Assert(_state == 6,
                $"Race condition occurred after {loop} loops");
        }
        _state = 5;
    }
}
```

You can verify this by defining a method for a task. The method RaceCondition of the class SampleTask gets a StateObject as a parameter. Inside an endless while loop, the ChangeState method is invoked. The variable i is used just to show the loop number in the assert message:

```
public class SampleTask
{
    public void RaceCondition(object o)
    {
        Trace.Assert(o is StateObject, "o must be of type StateObject");
        StateObject state = o as StateObject;

        int i = 0;
        while (true)
        {
            state.ChangeState(i++);
        }
    }
}
```

In the Main method of the program, a new StateObject is created that is shared among all the tasks. Task objects are created by invoking the RaceCondition method with the lambda expression that is passed to the Run method of the Task. The main thread then waits for user input. However, there’s a good chance that the program will halt before reading user input, as a race condition will happen:

```
public void RaceConditions()
{
    var state = new StateObject();
    for (int i = 0; i < 2; i++)
    {
        Task.Run(() => new SampleTask().RaceCondition(state));
    }
}
```

When you start the program, you get race conditions. How long it takes until the first race condition happens depends on your system and whether you build the program as a release build or a debug build. With a release build, the problem happens more often because the code is optimized. If you have multiple CPUs in your system or dual-/quad-core CPUs, where multiple threads can run concurrently, the problem also occurs more often than with a single-core CPU. The problem occurs with a single-core CPU because thread scheduling is preemptive, but the problem doesn’t occur that often.

Figure 22.1 shows an assertion of the program in which the race condition occurred after 1121 loops. If you start the application multiple times, you always get different results.

![Figure 22.1](img/3d365b72b289213a91ade7eb366b8f35_786_0.png)

You can avoid the problem by locking the shared object. You do this inside the thread by locking the variable state, which is shared among the threads, with the lock statement, as shown in the following example. Only one thread can exist inside the lock block for the state object. Because this object is shared among all threads, a thread must wait at the lock if another thread has the lock for state. As soon as the lock is accepted, the thread owns the lock, and gives it up at the end of the lock block. If every thread changing the object referenced with the state variable is using a lock, the race condition no longer occurs:

```
public class SampleTask
{
    public void RaceCondition(object o)
    {
        Trace.Assert(o is StateObject, "o must be of type StateObject");
        StateObject state = o as StateObject;

        int i = 0;
        while (true)
        {
            lock (state) // no race condition with this lock
            {
                state.ChangeState(i++);
            }
        }
    }
}
```

> **NOTE** With the downloaded sample code, you need to uncomment the lock statements for solving the issues with race conditions.

Instead of performing the lock when using the shared object, you can make the shared object thread-safe. In the following code, the ChangeState method contains a lock statement. Because you cannot lock the state variable itself (only reference types can be used for a lock), the variable `_sync` of type object is defined and used with the lock statement. If a lock is done using the same synchronization object every time the value state is changed, race conditions no longer happen:

```
public class StateObject
{
    private int _state = 5;
    private object _sync = new object();

    public void ChangeState(int loop)
    {
        lock (_sync)
        {
            if (_state == 5)
            {
                _state++;
                Trace.Assert(_state == 6,
                    $"Race condition occurred after {loop} loops");
            }
            _state = 5;
        }
    }
}
```

### Deadlocks

Too much locking can get you in trouble as well. In a deadlock, at least two threads halt and wait for each other to release a lock. As both threads wait for each other, a deadlock occurs and the threads wait endlessly.

To demonstrate deadlocks, the following code instantiates two objects of type StateObject and passes them with the constructor of the SampleTask class. Two tasks are created: one task running the method Deadlock1 and the other task running the method Deadlock2 (code file ThreadingIssues/Program.cs):

```
var state1 = new StateObject();
var state2 = new StateObject();
new Task(new SampleTask(state1, state2).Deadlock1).Start();
new Task(new SampleTask(state1, state2).Deadlock2).Start();
```

The methods Deadlock1 and Deadlock2 now change the state of two objects: s1 and s2. That’s why two locks are generated. Deadlock1 first does a lock for s1 and next for s2. Deadlock2 first does a lock for s2 and
