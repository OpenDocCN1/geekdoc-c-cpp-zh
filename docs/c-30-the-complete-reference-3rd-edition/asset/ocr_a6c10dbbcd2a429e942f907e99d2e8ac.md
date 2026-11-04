```
MyThread mt1 = new MyThread("Thread #1");
MyThread mt2 = new MyThread("Thread #2");
MyThread mt3 = new MyThread("Thread #3");

mt1.Thrd.Join();
mt2.Thrd.Join();
mt3.Thrd.Join();
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