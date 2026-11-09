
wastes a lot of CPU time, which would be better spent performing other work or even just letting the CPU go idle to conserve power.

This brings us to the primitive kernel-mode constructs. The kernel-mode constructs are provided by the Windows operating system itself. As such, they require that your application's threads call functions implemented in the operating system kernel. Having threads transition from user mode to kernel mode and back incurs a big performance hit, which is why kernel-mode constructs should be avoided.² However, they do have a positive feature—when a thread uses a kernel-mode construct to acquire a resource that another thread has, Windows blocks the thread so that it is no longer wasting CPU time. Then, when the resource becomes available, Windows resumes the thread, allowing it to access the resource.

A thread waiting on a construct might block forever if the thread currently holding the construct never releases it. If the construct is a user-mode construct, the thread is running on a CPU forever, and we call this a *livelock*. If the construct is a kernel-mode construct, the thread is blocked forever, and we call this a *deadlock*. Both of these are bad, but of the two, a *deadlock* is always preferable to a *livelock*, because a *livelock* wastes both CPU time and memory (the thread's stack, etc.), whereas a *deadlock* wastes only memory.³

In an ideal world, we'd like to have constructs that take the best of both worlds. That is, we'd like a construct that is fast and non-blocking (like the user-mode constructs) when there is no contention. But when there is contention for the construct, we'd like it to be blocked by the operating system kernel. Constructs that work like this do exist; I call them *hybrid constructs*, and I will discuss them in Chapter 30. It is very common for applications to use the *hybrid constructs*, because in most applications, it is rare for two or more threads to attempt to access the same data at the same time. A *hybrid construct* keeps your application running fast most of the time, and occasionally it runs slowly to block the thread. The slowness usually doesn't matter at this point, because your thread is going to be blocked anyway.

Many of the CLR's *thread synchronization constructs* are really just object-oriented class wrappers around Win32 thread synchronization constructs. After all, CLR threads are Windows threads, which means that Windows schedules and controls the synchronization of threads. Windows thread synchronization constructs have been around since 1992, and a ton of material has been written about them.⁴ Therefore, I give them only cursory treatment in this chapter.

² I'll show a program that measures the performance later in this chapter, at the end of the “Event Constructs” section.

³ I say that the memory allocated for the thread is wasted because the memory is not being used in a productive manner if the thread is not making forward progress.

⁴ In fact, Christophe Nasarre's and my book, Windows via C/C++, Fifth Edition (Microsoft Press, 2007), has several chapters devoted to this subject.

## User-Mode Constructs

The CLR guarantees that reads and writes to variables of the following data types are atomic: Boolean, Char, (S)Byte, (U)Int16, (U)Int32, (U)IntPtr, Single, and reference types. This means that all bytes within that variable are read from or written to all at once. So, for example, if you have the following class:

```csharp
internal static class SomeType {
    public static Int32 x = 0;
}
```

and if a thread executes this line of code:

```csharp
SomeType.x = 0x01234567;
```

then the x variable will change from 0x00000000 to 0x01234567 all at once (atomically). Another thread cannot possibly see the value in an intermediate state. For example, it is impossible for some other thread to query SomeType.x and get a value of 0x01230000. Suppose that the x field in the preceding SomeType class is an Int64. If a thread executes this line of code:

```csharp
SomeType.x = 0x0123456789abcdef;
```

it is possible that another thread could query x and get a value of 0x0123456700000000 or 0x0000000089abcdef, because the read and write operations are not atomic. This is called a torn read.

Although atomic access to a variable guarantees that the read or write happens all at once, it does not guarantee when the read or write will happen due to compiler and CPU optimizations. The primitive user-mode constructs discussed in this section are used to enforce the timing of these atomic read and write operations. In addition, these constructs can also force atomic and timed access to variables of additional data types: (U)Int64 and Double.

There are two kinds of primitive user-mode thread synchronization constructs:

- Volatile constructs, which perform an atomic read or write operation on a variable containing a simple data type at a specific time
- Interlocked constructs, which perform an atomic read and write operation on a variable containing a simple data type at a specific time

All the volatile and interlocked constructs require you to pass a reference (memory address) to a variable containing a simple data type.

### Volatile Constructs

Back in the early days of computing, software was written using assembly language. Assembly language is very tedious, because programmers must explicitly state everything—use this CPU register for this, branch to that, call indirect through this other thing, and so on. To simplify programming,

```csharp
private static void Worker(Object o) {
    Int32 x = 0;
    while (!s_stopWorker) x++;
    Console.WriteLine("Worker: stopped when x={0}", x);
}
```

In this code, the Main method creates a new thread that executes the Worker method. This Worker method counts as high as it can before being told to stop. The Main method allows the Worker thread to run for five seconds before telling it to stop by setting the static Boolean field to true. At this point, the Worker thread should display what it counted up to, and then the thread will terminate. The Main thread waits for the Worker thread to terminate by calling Join, and then the Main thread returns, causing the whole process to terminate.

Looks simple enough, right? Well, the program has a potential problem due to all the optimizations that could happen to it. You see, when the Worker method is compiled, the compiler sees that s_stopWorker is either true or false, and it also sees that this value never changes inside the Worker method itself. So the compiler could produce code that checks s_stopWorker first. If s_stopWorker is true, then Worker: stopped when x=0 will be displayed. If s_stopWorker is false, then the compiler produces code that enters an infinite loop that increments x forever. You see, the optimizations cause the loop to run very fast because checking s_stopWorker only occurs once before the loop; it does not get checked with each iteration of the loop.

If you actually want to see this in action, put this code in a .cs file and compile the code by using C#'s /platform:x86 and /optimize+ switches. Then run the resulting EXE file, and you'll see that the program runs forever. Note that you have to compile for x86, ensuring that the x86 JIT compiler is used at run time. The x86 JIT compiler is more mature than the x64 JIT compiler, so it performs more aggressive optimizations. The x64 JIT compiler does not perform this particular optimization, and therefore the program runs to completion. This highlights another interesting point about all of this. Whether your program behaves as expected depends on a lot of factors, such as which compiler version and compiler switches are used, which JIT compiler is used, and which CPU your code is running on. In addition, to see the preceding program run forever, you must not run the program under a debugger because the debugger causes the JIT compiler to produce unoptimized code that is easier to step through.

Let's look at another example, which has two threads that are both accessing two fields.

```csharp
internal sealed class ThreadsSharingData {
    private Int32 m_flag = 0;
    private Int32 m_value = 0;

    // This method is executed by one thread
    public void Thread1() {
        // Note: These could execute in reverse order
        m_value = 5;
        m_flag = 1;
    }

    // This method is executed by another thread
    public void Thread2() {
    }
}
```
