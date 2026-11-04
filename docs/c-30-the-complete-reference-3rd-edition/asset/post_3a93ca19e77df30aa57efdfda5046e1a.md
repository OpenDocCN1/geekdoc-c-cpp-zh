
```
lock(lockOn) { // lock the entire method
    sum = 0; // reset sum

    for(int i=0; i < nums.Length; i++) {
        sum += nums[i];
        Console.WriteLine("Running total for " +
            Thread.CurrentThread.Name +
            " is " + sum);
        Thread.Sleep(10); // allow task-switch
    }
    return sum;
}
}
```

class MyThread {
    public Thread Thrd;
    int[] a;
    int answer;

    // Create one SumArray object for all instances of MyThread.
    static SumArray sa = new SumArray();

    // Construct a new thread.
    public MyThread(string name, int[] nums) {
        a = nums;
        Thrd = new Thread(this.Run);
        Thrd.Name = name;
        Thrd.Start(); // start the thread
    }

    // Begin execution of new thread.
    void Run() {
        Console.WriteLine(Thrd.Name + " starting.");

        answer = sa.SumIt(a);

        Console.WriteLine("Sum for " + Thrd.Name +
            " is " + answer);

        Console.WriteLine(Thrd.Name + " terminating.");
    }
}

class Sync {
    static void Main() {
        int[] a = {1, 2, 3, 4, 5};

        MyThread mt1 = new MyThread("Child #1", a);
        MyThread mt2 = new MyThread("Child #2", a);

        mt1.Thrd.Join();
        mt2.Thrd.Join();
    }
}

Here is sample output from the program. (The actual output you see may vary slightly.)

```
Child #1 starting.
Running total for Child #1 is 1
Child #2 starting.
Running total for Child #1 is 3
Running total for Child #1 is 6
Running total for Child #1 is 10
Running total for Child #1 is 15
Running total for Child #2 is 1
Sum for Child #1 is 15
Child #1 terminating.
Running total for Child #2 is 3
Running total for Child #2 is 6
Running total for Child #2 is 10
Running total for Child #2 is 15
Sum for Child #2 is 15
Child #2 terminating.
```

As the output shows, both threads compute the proper sum of 15.

Let's examine this program in detail. The program creates three classes. The first is SumArray. It defines the method SumIt(), which sums an integer array. The second class is MyThread, which uses a static object called sa that is of type SumArray. Thus, only one object of SumArray is shared by all objects of type MyThread. This object is used to obtain the sum of an integer array. Notice that SumArray stores the running total in a field called sum. Thus, if two threads use SumIt() concurrently, both will be attempting to use sum to hold the running total. Because this will cause errors, access to SumIt() must be synchronized.

Finally, the class Sync creates two threads and has them compute the sum of an integer array.

Inside SumIt(), the lock statement prevents simultaneous use of the method by different threads. Notice that lock uses lockOn as the object being synchronized. This is a private object that is used solely for synchronization. Sleep() is called to purposely allow a task-switch to occur, if one can—but it can't in this case. Because the code within SumIt() is locked, it can be used by only one thread at a time. Thus, when the second child thread begins execution, it does not enter SumIt() until after the first child thread is done with it. This ensures the correct result is produced.

To understand the effects of lock fully, try removing it from the body of SumIt(). After doing this, SumIt() is no longer synchronized, and any number of threads can use it concurrently on the same object. The problem with this is that the running total is stored in sum, which will be changed by each thread that calls SumIt(). Thus, when two threads call SumIt() at the same time on the same object, incorrect results are produced because sum reflects the summation of both threads, mixed together. For example, here is sample output from the program after lock has been removed from SumIt():

```
Child #1 starting.
Running total for Child #1 is 1
Child #2 starting.
Running total for Child #2 is 1
Running total for Child #1 is 3
Running total for Child #2 is 5
Running total for Child #1 is 8
Running total for Child #2 is 11
Running total for Child #1 is 15
Running total for Child #2 is 19
Running total for Child #1 is 24
Running total for Child #2 is 29
Sum for Child #1 is 29
Child #1 terminating.
Sum for Child #2 is 29
Child #2 terminating.
```

As the output shows, both child threads are using SumIt() at the same time on the same object, and the value of sum is corrupted.

The effects of lock are summarized here:

- For any given object, once a lock has been acquired, the object is locked and no other thread can acquire the lock.
- Other threads trying to acquire the lock on the same object will enter a wait state until the code is unlocked.
- When a thread leaves the locked block, the object is unlocked.

## An Alternative Approach

Although locking a method's code, as shown in the previous example, is an easy and effective means of achieving synchronization, it will not work in all cases. For example, you might want to synchronize access to a method of a class you did not create, which is itself not synchronized. This can occur if you want to use a class that was written by a third party and for which you do not have access to the source code. Thus, it is not possible for you to add a lock statement to the appropriate method within the class. How can access to an object of this class be synchronized? Fortunately, the solution to this problem is simple: Lock access to the object from code outside the object by specifying the object in a lock statement. For example, here is an alternative implementation of the preceding program. Notice that the code within SumIt() is no longer locked and no longer declares the lockOn object. Instead, calls to SumIt() are locked within MyThread.

```
// Another way to use lock to synchronize access to an object.

using System;
using System.Threading;

class SumArray {
    int sum;
    public int SumIt(int[] nums) {
        sum = 0; // reset sum

        for(int i=0; i < nums.Length; i++) {
            sum += nums[i];
            Console.WriteLine("Running total for " +
                Thread.CurrentThread.Name +
                " is " + sum);
            Thread.Sleep(10); // allow task-switch
        }
        return sum;
    }
}
class MyThread {
    public Thread Thrd;
    int[] a;
    int answer;

    /* Create one SumArray object for all
    instances of MyThread. */
    static SumArray sa = new SumArray();

    // Construct a new thread.
    public MyThread(string name, int[] nums) {
        a = nums;
        Thrd = new Thread(this.Run);
        Thrd.Name = name;
        Thrd.Start(); // start the thread
    }

    // Begin execution of new thread.
    void Run() {
        Console.WriteLine(Thrd.Name + " starting.");
        // Lock calls to SumIt().
        lock(sa) answer = sa.SumIt(a);
        Console.WriteLine("Sum for " + Thrd.Name +
            " is " + answer);
        Console.WriteLine(Thrd.Name + " terminating.");
    }
}
class Sync {
    static void Main() {
        int[] a = {1, 2, 3, 4, 5};
        MyThread mt1 = new MyThread("Child #1", a);
        MyThread mt2 = new MyThread("Child #2", a);
        mt1.Thrd.Join();
        mt2.Thrd.Join();
    }
}
```

Here, the call to sa.SumIt() is locked, rather than the code inside SumIt() itself. The code that accomplishes this is shown here:

```
// Lock calls to SumIt().
lock(sa) answer = sa.SumIt(a);
```

Because sa is a private object, it is safe to lock on. Using this approach, the program produces the same correct results as the original approach.

## The Monitor Class and lock

The C# keyword lock is really just shorthand for using the synchronization features defined by the Monitor class, which is defined in the System.Threading namespace. Monitor defines several methods that control or manage synchronization. For example, to obtain a lock on an object, call Enter(). To release a lock, call Exit(). These methods are shown here:

```
public static void Enter(object syncOb)
public static void Exit(object syncOb)
```

Here, syncOb is the object being synchronized. If the object is not available when Enter() is called, the calling thread will wait until it becomes available. You will seldom use Enter() or Exit(), however, because a lock block automatically provides the equivalent. For this reason, lock is the preferred method of obtaining a lock on an object when programming in C#.

One method in Monitor that you may find useful on occasion is TryEnter(). One of its forms is shown here:

```
public static bool TryEnter(object syncOb)
```

It returns true if the calling thread obtains a lock on syncOb and false if it doesn't. In no case does the calling thread wait. You could use this method to implement an alternative if the desired object is unavailable.

Monitor also defines these three methods: Wait(), Pulse(), and PulseAll(). They are described in the next section.

## Thread Communication Using Wait(), Pulse(), and PulseAll()

Consider the following situation. A thread called T is executing inside a lock block and needs access to a resource, called R, that is temporarily unavailable. What should T do? If T enters some form of polling loop that waits for R, then T ties up the object, blocking other threads' access to it. This is a less than optimal solution because it partially defeats the advantages of programming for a multithreaded environment. A better solution is to have T temporarily relinquish control of the object, allowing another thread to run. When R becomes available, T can be notified and resume execution. Such an approach relies upon some form of interthread communication in which one thread can notify another that it is blocked and be notified when it can resume execution. C# supports interthread communication with the Wait(), Pulse(), and PulseAll() methods.

The Wait(), Pulse(), and PulseAll() methods are defined by the Monitor class. These methods can be called only from within a locked block of code. Here is how they are used. When a thread is temporarily blocked from running, it calls Wait(). This causes the thread to go to sleep and the lock for that object to be released, allowing another thread to use the object. At a later point, the sleeping thread is awakened when some other thread enters the same lock and calls Pulse() or PulseAll(). A call to Pulse() resumes the first thread in the queue of threads waiting for the lock. A call to PulseAll() signals the release of the lock to all waiting threads.

Here are two commonly used forms of Wait():

```
public static bool Wait(object waitOb)
public static bool Wait(object waitOb, int milliseconds)
```

The first form waits until notified. The second form waits until notified or until the specified period of milliseconds has expired. For both, waitOb specifies the object upon which to wait.
