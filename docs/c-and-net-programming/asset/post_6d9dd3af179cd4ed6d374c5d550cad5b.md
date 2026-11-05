
## Example

```csharp
//Illustration of thread Abort operation
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;

namespace MultiThread
{
    class AbortOp
    {
        static void Main(string[] args)
        {
            Thread th = new Thread(Show);

            if (th.IsAlive)
            {
                th.Start();
                th.Abort(); //Show method is immediately stopped as thread aborts
            }
            for (int cnt = 1; cnt <= 10; cnt++)
            {
                Console.WriteLine("India");
            }
        }

        private static void Show()
        {
            for (int cnt = 1; cnt <= 5; cnt++)
            {
                Console.WriteLine("Welcome To");
            }
        }
    }
}
```

## Output

```text
India
India
India
India
India
India
India
India
India
India
```

## 3. Suspend a Thread

The **Suspend method** of the Thread class suspends a thread.

The thread is suspended until the Resume method is called.

Syntax

```csharp
if (thread.ThreadState == ThreadState.Running)
{
    thread.Suspend();
}
```

## 4. Resume a suspended Thread

The **Resume method** is called to resume a suspended thread.

If the thread is not suspended, the Resume method will have no effect.

Syntax

```csharp
if (thread.ThreadState == ThreadState.Suspended) {
    thread.Resume();
}
```

## 5. Make the thread a background thread

The threads running in background remain running even the main thread finishes. To end all threads when main thread dies, IsBackground property is set to true.

Syntax

```csharp
// make the thread background
thrd.IsBackground = true;
```

## 6. Thread Priority

**Concept**

- Priority is certain values (usually integer type) attached with the thread so as to indicate its importance from running point of view. That is priority tells that which thread is to be given a chance to execute first over other simultaneously running threads.

**Explanation**

- The Thread class's ThreadPriority property is used to set the thread's priority. The thread priority can have **Normal, AboveNormal, BelowNormal, Highest**, and **Lowest** values.

In C#, System.Threading.ThreadPriority is an enumeration that defines the priority states of a thread that in turn determines how much processor time a thread gets to execute.

- **High priority** threads always get more processor time than their counterparts. If there is more than one thread at a high priority then the operating system cycles through the threads giving each high priority thread some amount of processor time. Lower priority threads do not get to execute as long as a higher priority thread is available.
- When there are no more threads of higher priority, the operating system then selects the next lower priority threads for execution. If at any point it encounters a higher priority thread, then the lower priority threads are preempted (taken away from CPU) and higher priority thread is executed.
- Any new thread, when created, is assigned a **Normal priority**. If required, the thread priority value can be changed to any of the values shown below. There are **5 priorities** defined in the Priority property of the Thread class.
  - Highest
  - AboveNormal
  - Normal
  - BelowNormal
  - Lowest
- Syntax

```csharp
thread.Priority = ThreadPriority.Lowest;

//Example

//Illustration of thread creation without setting any priority

/* PrioritiesDemo1 program do not define any priority, which executes the method Show()
   first and then Main method gets a chance to execute. */

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;

namespace MultiThread
{
    class PrioritiesDemo1
    {
        static void Main(string[] args)
        {
            Thread th = new Thread(Show);
            th.Start();
            for (int cnt = 1; cnt <= 10; cnt++)
            {
                Console.WriteLine("India");
            }
        }

        private static void Show()
        {
            for (int cnt = 1; cnt <= 5; cnt++)
            {
                Console.WriteLine("Welcome to");
            }
        }
    }
}
```

## Output

```text
Welcome to
Welcome to
Welcome to
Welcome to
Welcome to
India
India
India
India
India
India
India
India
India
India
```

## Example

```csharp
//illustration of thread Using With Lowest Priority
/* PrioritiesDemo2 program defines the priority. New thread has low priority therefore
method Show() of this thread gets chance after high priority Main thread. Main method
executes first. */
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;

namespace MultiThread
{
    class PrioritiesDemo2
    {
        static void Main(string[] args)
        {
            Thread th = new Thread(Show);
            th.Priority = ThreadPriority.Lowest;
            th.Start();
            for (int cnt = 1; cnt <= 10; cnt++)
            {
                Console.WriteLine("India");
            }
        }

        private static void Show()
        {
            for (int cnt = 0; cnt < 5; cnt++)
            {
                Console.WriteLine("Welcome To");
            }
        }
    }
}
```

## Output

```text
India
India
India
India
India
India
India
India
India
India
Welcome To
Welcome To
Welcome To
Welcome To
Welcome To
```

## 15.5 Applications and Benefits of Threads

- Mutually exclusive tasks of the single process, such as gathering user input and background processing can be managed with the use of threads.
- Threads can be used as a convenient way to structure a program that performs several similar or identical tasks concurrently.
- Major advantage of using the threads is that multiple activities can be carried out simultaneously.
- Another advantage is that thread can be used to achieve faster computations by doing two different computations in two threads instead of serially one after the other.

## 15.6 Thread Communication

### 15.6.1 Synchronization

**Concept**

- Synchronization means coordinating the actions of threads for a fixed expected predictable outcome in terms of time and manipulations.

**Explanation**

- Synchronization is particularly important when threads access the same data.
- Synchronization processing can be divided into following four categories.

- **1. Synchronization using blocking the methods** — In this synchronization technique, rest of the threads wait for another thread to finish or wait for a period of time to elapse. Sleep, Join, and EndInvoke are simple blocking methods used for blocking.
- **2. Synchronization using Locking concept** — In this, exclusive access to a resource is enforced, such as a field or section of code, ensuring that only one thread can enter at a time. Locking is the primary thread-safety mechanism that allows threads to access common data without interfering with each other. The locking constructs are lock and Mutex and a variation of mutex called Semaphore.
- **3. Synchronization using Signals** — By sending signals, a thread can be paused until receiving a notification from another, avoiding the need for inefficient polling. There are two signaling mechanisms, event wait and Monitor's Wait/Pulse methods.
- **4. Synchronization using Nonblocking** — By this method, access to a common field is protected by calling upon processor primitives. The Interlocked class and the volatile keyword are the two constructs for achieving nonblocking methodology.

### 15.6.2 Blocking

**Concept**

- A thread is said to be blocked when its execution is paused for some reason, such as when waiting for another to end via Join or EndInvoke.

**Explanation**

- A blocked thread consumes almost no processor time.
- The CLR and operating system know about blocked threads, and provide appropriate support to keep them in a non-working state, waking them up when their blocking conditions are satisfied.

### 15.6.3 Locking

**Concept**

- Exclusive locking is used to ensure that only one thread can enter particular sections of code at a time. The .NET Framework provides two exclusive locking constructs namely lock and Mutex.

**Explanation**

- Only one thread can lock the synchronizing object (in this case, locker) at a time, and any contending threads are blocked until the lock is released. If more than one thread contends the lock, they are queued on a "ready queue" and granted the lock on a first-come, first-served basis. Exclusive locks are sometimes said to enforce serialized access to whatever's protected by the lock, because one thread's access cannot overlap with that of another thread.
- A thread blocked while awaiting a contended lock has a **ThreadState** of **WaitSleepJoin**.
- Locking should be done before accessing any field comprising writable shared state.

### 15.6.4 Mutex

A Mutex is like a C# lock, but it can work across multiple processes. In other words, Mutex can be computer-wide as well as application-wide.
