
be blocked anyway.

Many of the CLR's thread synchronization constructs are really just object-oriented class wrappers around Win32 thread synchronization constructs. After all, CLR threads are Windows threads, which means that Windows schedules and controls the synchronization of threads. Windows thread synchronization constructs have been around since 1992, and a ton of material has been written about them.67 Therefore, I give them only cursory treatment in this chapter.

## User-Mode Constructs

The CLR guarantees that reads and writes to variables of the following data types are atomic: **Boolean, Char, (S)Byte, (U)Int16, (U)Int32, (U)IntPtr, Single**, and **reference types**. This means that all bytes within that variable are read from or written to all at once. So, for example, if you have the following class:

```csharp
internal static class SomeType {
    public static Int32 x = 0;
}
```

then, if some thread executes this line of code:

```csharp
SomeType.x = 0x01234567;
```

the x variable will change from 0x00000000 to 0x01234567 all at once (atomically). Another thread cannot possibly see the value in an intermediate state. For example, it is impossible for some other read to query SomeType.x and get a value of 0x01230000. Suppose that the x field in the SomeType class above is an Int64. If a thread executes this line of code:

```csharp
SomeType.x = 0x0123456789abcdef;
```

it is possible that another thread could query x and get a value of 0x0123456700000000 or 0x0000000089abcdef, since the read and write operations are not atomic. This is called a torn read.

While atomic access to a variable guarantees that the read or write happens all at once, it does not guarantee when the read or write will happen due to compiler and CPU optimizations. The primitive user-mode constructs discussed in this section are used to enforce the timing of these atomic read and write operations. In addition, these constructs can also force atomic and timed access to variables of additional data types: **(U)Int64** and **Double**.

There are two kinds of primitive user-mode thread synchronization constructs:

- Volatile constructs, which perform an atomic read or write operation on a variable containing a simple data type at a specific time
- Interlocked constructs, which perform an atomic read and write operation on a variable containing a simple data type at a specific time

All the volatile and interlocked constructs require you to pass a reference (memory address) to a variable containing a simple data type.

### Volatile Constructs

Back in the early days of computing, software was written using assembly language. Assembly language is very tedious, because programmers must explicitly state everything—use this CPU register for this, branch to that, call indirect through this other thing, and so on. To simplify programming, higher-level languages were introduced. These higher-level languages introduced common useful constructs, like if/else, switch/case, various loops, local variables, arguments, virtual method calls, operator overloads, and much more. Ultimately, these language compilers must convert the high-level constructs down to the low-level constructs so that the computer can actually do what you want it to do.

In other words, the C# compiler translates your C# constructs into Intermediate Language (IL), which is then converted by the just-in-time (JIT) compiler into native CPU instructions, which must then be processed by the CPU itself. In addition, the C# compiler, the JIT compiler, and even the CPU itself can optimize your code. For example, the following ridiculous method can ultimately be compiled into nothing:

```csharp
private static void OptimizedAway() {
    // Constant expression is computed at compile time resulting in zero
    Int32 value = (1 * 100) - (50 * 2);

    // If value is 0, the loop never executes
    for (Int32 x = 0; x < value; x++)
    {
        // There is no need to compile the code in the loop since it can never execute
        Console.WriteLine("Jeff");
    }
}
```

In this code, the compiler can see that value will always be 0; therefore, the loop will never execute and consequently, there is no need to compile the code inside the loop. This method could be compiled down to nothing. In fact, when JITing a method that calls OptimizedAway, the JITter will try to inline the OptimizedAway method’s code. Since there is no code, the JITter will even remove the code that tries to call OptimizedAway. We love this feature of compilers. As developers, we get to write the code in the way that makes the most sense to us. The code should be easy to write, read, and maintain. Then compilers translate our intentions into machine-understandable code. We want our compilers to do the best job possible for us.

When the C# compiler, JIT compiler, and CPU optimize our code, they guarantee us that the intention of the code is preserved. That is, from a single-threaded perspective, the method does what we want it to do, although it may not do it exactly the way we described in our source code. However, the intention might not be preserved from a multithreaded perspective. Here is an example where the optimizations make the program not work as expected:

```csharp
internal static class StrangeBehavior {
  // As you'll see later, mark this field as volatile to fix the problem
  private static Boolean s_stopWorker = false;

  public static void Main() {
    Console.WriteLine("Main: letting worker run for 5 seconds");
    Thread t = new Thread(Worker);
    t.Start();
    Thread.Sleep(5000);
    s_stopWorker = true;
    Console.WriteLine("Main: waiting for worker to stop");
    t.Join();
  }

  private static void Worker(Object o) {
    Int32 x = 0;
    while (!s_stopWorker) x++;
    Console.WriteLine("Worker: stopped when x={0}", x);
  }
}
```

In this code, the Main method creates a new thread that executes the Worker method. This Worker method counts as high as it can before being told to stop. The Main method allows the Worker thread to run for 5 seconds before telling it to stop by setting the static Boolean field to true. At this point, the Worker thread should display what it counted up to, and then the thread will terminate. The Main thread waits for the Worker thread to terminate by calling Join, and then the Main thread returns, causing the whole process to terminate.

Looks simple enough, right? Well, the program has a potential problem due to all the optimizations that could happen to it. You see, when the Worker method is compiled, the compiler sees that s_stopWorker is either true or false, and it also sees that this value never changes inside the Worker method itself. So the compiler could produce code that checks s_stopWorker first. If s_stopWorker is true, then "Worker: stopped when x=0" will be displayed. If s_stopWorker is false, then the compiler produces code that enters an infinite loop that increments x forever. You see, the optimizations cause the loop to run very fast because checking s_stopWorker only occurs once before the loop; it does not get checked with each iteration of the loop.

If you actually want to see this in action, put this code in a .cs file and compile the code using C#'s /platform:x86 and /optimize+ switches. Then run the resulting EXE file, and you'll see that the program runs forever. Note that you have to compile for x86 ensuring that the x86 JIT compiler is used at runtime. The x86 JIT compiler is more mature than the x64 JIT compiler, so it performs more aggressive optimizations. The x64 JIT compiler does not perform this particular optimization, and therefore the program runs to completion. This highlights another interesting point about all of this. Whether your program behaves as expected depends on a lot of factors, such as which compiler

67 In fact, my own book, *Windows via C/C++*, 5th Edition (Microsoft Press, 2007), has several chapters devoted to this subject.
