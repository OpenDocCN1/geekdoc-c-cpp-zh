
```
object gate = new object();
lock (gate)
{
    // Do stuff...
}
```

## THE EVIL LOCK SNIPPET

Visual Studio comes with a code snippet for a "lock block." By default, this lock is taken on the this object, highlighted for substitution by some other object. You should really make this substitution because locking on this is considered evil:

```
// Don't do this at home!
lock (this)
    // Do work under the lock
```

Why? When you lock on an instance of your class that's shared with other code, someone else can take a lock on the object without you knowing about it. This can easily cause your program to become locked endlessly.

The core of this issue is sharing state—in this case this or the object itself—associated with an implementation detail (locking to make the code behave well), which should always be considered evil. Check out vssnippets.codeplex.com, a project of this book's reviewer, for some great code snippets to help you deal with concurrent programming (and more).

This is roughly turned into the following piece of code. Notice, however, that you shouldn't write this code by hand but should use the lock keyword instead. Over the years, the C# compiler has tweaked the code emitted for locks, taking care of tricky edge cases.

```
object gate = new object();
bool __lockTaken = false;
try
{
    Monitor.Enter(gate, ref __lockTaken);
    // Do stuff...
}
finally
{
    if (__lockTaken)
        Monitor.Exit(gate);
}
```

The overload passing a Boolean "lock taken" flag by reference was added in .NET 4 and is what the C# compiler emits code against. Ignore this flag for now, though. The basic idea of a monitor's Enter method is to block until no more (other) threads are inside the lock.

When the method returns, the code can proceed to run code that won't be influenced by other code using the same lock object. In summary, this means that the acquired lock is exclusive: Only one thread can be operating under the lock at any given point in time.

## BEWARE OF BOXING

Don't use a value for the object to lock on because this results in boxing. Each time you use the lock keyword with a value (even if it's the same), a different (heap-allocated) boxed object is created. Because the monitor deals with objects on the heap, different boxed objects result in different locks. So you would end up with different nonexclusive locks, voiding the protection you thought you created.

Use of the Boolean flag to determine whether the lock was taken was introduced in the latest version of the .NET Framework to protect against certain exceptional cases. The lock should only be released, by calling Monitor.Exit, if the lock was acquired. If an exception occurred while attempting to acquire the lock, we would end up in the finally block, and the check for the "lock taken" flag reveals the lock shouldn't be released. Such a situation can happen when Interrupt is called on the blocked thread, which causes a ThreadInterruptedException to be thrown from the Enter call.

More functionality is defined on the Monitor class through static methods. For more information, refer to the MSDN documentation.

## Mutexes

Mutual exclusion of code executing simultaneously is the essential idea to tame the concurrency monster. In fact, the concept of a mutex got its name from it. Semaphores are the generalization of mutexes and are discussed in the next section.

Using a mutex, we could make our running example thread safe as follows. This piece of code illustrates the two main operations invoked with a mutex.

```
static void Main()
{
    var mutex = new Mutex();
    int n = 0;

    var up = new Thread(() =>
    {
        for (int i = 0; i < 1000000; i++)
        {
            mutex.WaitOne();
            n++;
            mutex.ReleaseMutex();
        }
    });
up.Start();

for (int i = 0; i < 1000000; i++)
{
    mutex.WaitOne();
    n--;
    mutex.ReleaseMutex();
}

up.Join();
Console.WriteLine(n);
}
```

Again, the code will be guaranteed to print zero as a result. The basic idea is to use the WaitOne method to wait for the mutex to be released by another thread. When this call returns, we've grabbed the mutex and can run with it. When we're done, we release the mutex, allowing another thread to grab it. No two threads can have acquired the mutex at the same time. This technique is often used in real life, too. For example, if trains have to share the same track in opposite directions, a driver's protocol may be set up to avoid crashes. One such protocol is to require a driver to carry a stick before he or she is allowed to drive over the shared track. Figure 29.20 shows this in practice with train drivers carrying a flag (the mutex).

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1507_0.png)

FIGURE 29.20 Mutexes applied in railway traffic.

So why would we use mutexes instead of taking the lock-based approach? Although the concept of a monitor sits at the level of the common language runtime, mutexes are a lower-level operating system primitive. Different constructors and static methods on the Mutex class illustrate this fact. In particular, mutexes can be named and used from different processes. This allows coordination of resource access across a set of different components of a bigger system.

As an example, consider the following code fragment. Here, the Main method takes in a name of an event to wait on. The application then tries to grab the mutex by calling WaitOne, after which it blocks waiting for user input to release the mutex. Running two instances of the application will clearly show how both instances can be waiting for one another:

```
static void Main(string[] args)
{
    var createdNew = false;
    var mutex = new Mutex(/* start as owned */ false, args[0], out createdNew);
    Console.WriteLine("Mutex {0} - Created = {1}", args[0], createdNew);

    Console.Write("Waiting... ");
    mutex.WaitOne();
    Console.WriteLine("Acquired.", DateTime.Now);

    Console.Write("Press ENTER to release... ");
    Console.ReadLine();
    mutex.ReleaseMutex();
}
```

Figure 29.21 shows this example in practice, where one instance of the application is waiting for the other instance to release the shared mutex. All we had to do to obtain the mutex is create an instance of Mutex passing in the common mutex name. The output parameter createdNew reveals whether an existing mutex was found. Alternatively, the Mutex.OpenExisting method can be used.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1508_0.png)

FIGURE 29.21 Mutexes coordinating resource access across processes.

One caveat to point out is this: If you try to morph the lock-based counter solution into the form using mutexes, you see a significant performance difference that favors the use of locks. The difference can be as large as a 100x factor.

The reason for the weaker performance of mutexes is their very low-level nature by which a thread becomes blocked at the operating system scheduler level, causing the thread to transition into another state and causing context switches. Monitors, on the other hand, are a common language runtime facility that sits much higher on the stack and are not as costly.

On the flip side, mutexes are the way to go if you need cross-process synchronization, where the use of monitors falls short. To prove that mutexes are low-level primitives, you can use the SysInternals Process Explorer tool and look at a process's resources, as shown in Figure 29.22. Mutexes are known as “mutants” in the operating system, and therefore they appear as such in the tool.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1509_0.png)

FIGURE 29.22 Mutexes are an operating system-level facility, known as mutants.

## Semaphores

Semaphores are a generalization of mutexes. Maybe it's better to state the opposite: Mutexes are a special case of the semaphore primitive invented by the Dutch computer scientist Dijkstra. The name semaphore was inspired by synchronization mechanisms used in railways; they are the equivalent to roadside traffic lights.

Before getting into details about the Semaphore class and its properties, let's take a look at a railway semaphore. Figure 29.23 shows states a semaphore can be in, which are used to communicate actions to train drivers. I'm not an expert in railway design, but the basic idea is simple. One sign indicates the train has to stop, and another indicates it's safe to pass. An intermediate state sometimes exists, too, indicating another train is in the next segment, allowing the driver to proceed with caution. Nowadays, such signs have largely been replaced with traffic lights.

Dijkstra defined the concept of a semaphore in terms of two operations, P and V. The former stands for prolaag, a made-up Dutch word of probeer verlaag or “try to decrease.” V, on the other hand, stands for the existing Dutch word verhoog, which means “to increase.”
