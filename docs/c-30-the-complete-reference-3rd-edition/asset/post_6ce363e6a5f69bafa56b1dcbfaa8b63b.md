
```
Decrement Thread is waiting for the mutex.
In Increment Thread, SharedRes.Count is 1
In Increment Thread, SharedRes.Count is 2
In Increment Thread, SharedRes.Count is 3
In Increment Thread, SharedRes.Count is 4
In Increment Thread, SharedRes.Count is 5
Increment Thread releases the mutex.
Decrement Thread acquires the mutex.
In Decrement Thread, SharedRes.Count is 4
In Decrement Thread, SharedRes.Count is 3
In Decrement Thread, SharedRes.Count is 2
In Decrement Thread, SharedRes.Count is 1
In Decrement Thread, SharedRes.Count is 0
Decrement Thread releases the mutex.
```

As the output shows, access to SharedRes.Count is synchronized, with only one thread at a time being able to change its value.

To prove that the Mutex was needed to produce the preceding output, try commenting out the calls to WaitOne() and ReleaseMutex() in the preceding program. When you run the program, you will see the following sequence (the actual output you see may vary):

```
In Increment Thread, SharedRes.Count is 1
In Decrement Thread, SharedRes.Count is 0
In Increment Thread, SharedRes.Count is 1
In Decrement Thread, SharedRes.Count is 0
In Increment Thread, SharedRes.Count is 1
In Decrement Thread, SharedRes.Count is 0
In Increment Thread, SharedRes.Count is 1
In Decrement Thread, SharedRes.Count is 0
In Increment Thread, SharedRes.Count is 1
In Decrement Thread, SharedRes.Count is 0
In Increment Thread, SharedRes.Count is 1
```

As this output shows, without the mutex, increments and decrements to SharedRes.Count are interspersed rather than sequenced.

The mutex created by the previous example is known only to the process that creates it. However, it is possible to create a mutex that is known systemwide. To do so, you must create a named mutex, using one of these constructors:

```
public Mutex(bool owned, string name)
public Mutex(bool owned, string name, out bool whatHappened)
```

In both forms, the name of the mutex is passed in name. In the first form, if owned is true, then ownership of the mutex is requested. However, because a systemwide mutex might already be owned by another process, it is better to specify false for this parameter. In the second form, on return, whatHappened will be true if ownership was requested and acquired. It will be false if ownership was denied. (There is also a third form of the Mutex constructor that allows you to specify a MutexSecurity object, which controls access.) Using a named mutex enables you to manage interprocess synchronization.

One other point: It is legal for a thread that has acquired a mutex to make one or more additional calls to WaitOne() prior to calling ReleaseMutex(), and these additional calls will succeed. That is, redundant calls to WaitOne() will not block a thread that already owns the mutex. However, the number of calls to WaitOne() must be balanced by the same number of calls to ReleaseMutex() before the mutex is released.

## The Semaphore

A semaphore is similar to a mutex except that it can grant more than one thread access to a shared resource at the same time. Thus, the semaphore is useful when a collection of resources is being synchronized. A semaphore controls access to a shared resource through the use of a counter. If the counter is greater than zero, then access is allowed. If it is zero, access is denied. What the counter is counting are permits. Thus, to access the resource, a thread must be granted a permit from the semaphore.

In general, to use a semaphore, the thread that wants access to the shared resource tries to acquire a permit. If the semaphore's counter is greater than zero, the thread acquires a permit, which causes the semaphore's count to be decremented. Otherwise, the thread will block until a permit can be acquired. When the thread no longer needs access to the shared resource, it releases the permit, which causes the semaphore's count to be incremented. If there is another thread waiting for a permit, then that thread will acquire a permit at that time. The number of simultaneous accesses permitted is specified when the semaphore is created. If you create a semaphore that allows only one access, then a semaphore acts just like a mutex.

Semaphores are especially useful in situations in which a shared resource consists of a group or pool. For example, a collection of network connections, any of which can be used for communication, is a resource pool. A thread needing a network connection doesn't care which one it gets. In this case, a semaphore offers a convenient mechanism to manage access to the connections.

The semaphore is implemented by System.Threading.Semaphore. It has several constructors. The simplest form is shown here:

```csharp
public Semaphore(int initial, int max)
```

Here, initial specifies the initial value of the semaphore permit counter, which is the number of permits available. The maximum value of the counter is passed in max. Thus, max represents the maximum number of permits that can be granted by the semaphore. The value in initial specifies how many of these permits are initially available.

Using a semaphore is similar to using a mutex, described earlier. To acquire access, your code will call WaitOne() on the semaphore. This method is inherited by Semaphore from the WaitHandle class. WaitOne() waits until the semaphore on which it is called can be acquired. Thus, it blocks execution of the calling thread until the specified semaphore can grant permission.

When your code no longer needs ownership of the semaphore, it releases it by calling Release(), which is shown here:

```csharp
public int Release()
public int Release(int num)
```

The first form releases one permit. The second form releases the number of permits specified by num. Both return the permit count that existed prior to the release.

It is possible for a thread to call WaitOne() more than once before calling Release(). However, the number of calls to WaitOne() must be balanced by the same number of calls to Release() before the permit is released. Alternatively, you can call the Release(int) form, passing a number equal to the number of times that WaitOne() was called.

Here is an example that illustrates the semaphore. In the program, the class MyThread uses a semaphore to allow only two MyThread threads to be executed at any one time. Thus, the resource being shared is the CPU.

```csharp
// Use a Semaphore.
using System;
using System.Threading;

// This thread allows only two instances of itself
// to run at any one time.
class MyThread {
    public Thread Thrd;

    // This creates a semaphore that allows up to two
    // permits to be granted and that initially has
    // two permits available.
    static Semaphore sem = new Semaphore(2, 2);

    public MyThread(string name) {
        Thrd = new Thread(this.Run);
        Thrd.Name = name;
        Thrd.Start();
    }

    // Entry point of thread.
    void Run() {

        Console.WriteLine(Thrd.Name + " is waiting for a permit.");

        sem.WaitOne();

        Console.WriteLine(Thrd.Name + " acquires a permit.");

        for(char ch='A'; ch < 'D'; ch++) {
            Console.WriteLine(Thrd.Name + ": " + ch + " ");
            Thread.Sleep(500);
        }

        Console.WriteLine(Thrd.Name + " releases a permit.");

        // Release the semaphore.
        sem.Release();
    }
}

class SemaphoreDemo {
    static void Main() {

        // Construct three threads.
        MyThread mt1 = new MyThread("Thread #1");
        MyThread mt2 = new MyThread("Thread #2");
        MyThread mt3 = new MyThread("Thread #3");

        mt1.Thrd.Join();
        mt2.Thrd.Join();
        mt3.Thrd.Join();
    }
}
```

MyThread declares the semaphore sem, as shown here:

```
static Semaphore sem = new Semaphore(2, 2);
```

This creates a semaphore that can grant up to two permits and that initially has both permits available.

In MyThread.Run(), notice that execution cannot continue until a permit is granted by the semaphore, sem. If no permits are available, then execution of that thread suspends. When a permit does become available, execution resumes and the thread can run. In Main(), three MyThread threads are created. However, only the first two get to execute. The third must wait until one of the other threads terminates. The output, shown here, verifies this. (The actual output you may vary slightly.)

```
Thread #1 is waiting for a permit.
Thread #1 acquires a permit.
Thread #1 : A
Thread #2 is waiting for a permit.
Thread #2 acquires a permit.
Thread #2 : A
Thread #3 is waiting for a permit.
Thread #1 : B
Thread #2 : B
Thread #1 : C
Thread #2 : C
Thread #1 releases a permit.
Thread #3 acquires a permit.
Thread #3 : A
Thread #3 releases a permit.
Thread #3 : B
Thread #3 : C
Thread #3 releases a permit.
```

The semaphore created by the previous example is known only to the process that creates it. However, it is possible to create a semaphore that is known systemwide. To do so, you must create a named semaphore. To do this, use one of these constructors:

```
public Semaphore(int initial, int max, string name)
public Semaphore(int initial, int max, string name, out bool whatHappened)
```

In both forms, the name of the semaphore is passed in name. In the first form, if a semaphore by the specified name does not already exist, it is created using the values of initial and max. If it does already exist, then the values of initial and max are ignored. In the second form, on return, whatHappened will be true if the semaphore was created. In this case, the values of initial and max will be used to create the semaphore. If whatHappened is false, then the
