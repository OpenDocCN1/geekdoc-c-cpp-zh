we want it to do, although it may not do it exactly the way we described in our source code. However, the intention might not be preserved from a multithreaded perspective. Here is an example where the optimizations make the program not work as expected:

```
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
```

In this code, the Main method creates a new thread that executes the Worker method. This Worker method counts as high as it can before being told to stop. The Main method allows the Worker thread to run for 5 seconds before telling it to stop by setting the static Boolean field to true. At this point, the Worker thread should display what it counted up to, and then the thread will terminate. The Main thread waits for the Worker thread to terminate by calling Join, and then the Main thread returns, causing the whole process to terminate.

Looks simple enough, right? Well, the program has a potential problem due to all the optimizations that could happen to it. You see, when the Worker method is compiled, the compiler sees that s_stopWorker is either true or false, and it also sees that this value never changes inside the Worker method itself. So the compiler could produce code that checks s_stopWorker first. If s_stopWorker is true, then "Worker: stopped when x=0" will be displayed. If s_stopWorker is false, then the compiler produces code that enters an infinite loop that increments x forever. You see, the optimizations cause the loop to run very fast because checking s_stopWorker only occurs once before the loop; it does not get checked with each iteration of the loop.

If you actually want to see this in action, put this code in a .cs file and compile the code using C#'s /platform:x86 and /optimize+ switches. Then run the resulting EXE file, and you'll see that the program runs forever. Note that you have to compile for x86 ensuring that the x86 JIT compiler is used at runtime. The x86 JIT compiler is more mature than the x64 JIT compiler, so it performs more aggressive optimizations. The x64 JIT compiler does not perform this particular optimization, and therefore the program runs to completion. This highlights another interesting point about all of this. Whether your program behaves as expected depends on a lot of factors, such as which compiler