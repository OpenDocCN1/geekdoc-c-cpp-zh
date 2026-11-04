needs to be defined as Func<string>, a method returning a string. This method is invoked only once for each thread that is used to do the iterations.

The second delegate parameter defines the delegate for the body. In the example, the parameter is of type Func<int, ParallelLoopState, string, string>. The first parameter is the loop iteration; the second parameter, ParallelLoopState, allows for stopping the loop, as you saw earlier. With the third parameter, the body method receives the value that is returned from the init method. The body method also needs to return a value of the type that was defined with the generic For parameter.

The last parameter of the For() method specifies a delegate, Action<TLocal>; in the example, a string is received. This method again is called only once for each thread; this is a thread exit method.

```
Parallel.For<string>(0, 20,
() =>
{
    // invoked once for each thread
    Console.WriteLine("init thread {0}, task {1}",
        Thread.CurrentThread.ManagedThreadId, Task.CurrentId);
    return String.Format("t {0}",
        Thread.CurrentThread.ManagedThreadId);
},
(i, pls, str1) =>
{
    // invoked for each member
    Console.WriteLine("body i {0} str1 {1} thread {2} task {3}", i,
        Thread.CurrentThread.ManagedThreadId,
        Task.CurrentId);
    Thread.Sleep(10);
    return String.Format("i {0}", i);
},
(str1) =>
{
    // final action on each thread
    Console.WriteLine("finally {0}", str1);
});
```

The result of one time running this program is shown here:

```
init thread 1, task 1
body i 0 str1 t1 thread 1 task 1
body i 1 str1 i 0 thread 1 task 1
init thread 3, task 2
body i 10 str1 t3 thread 3 task 2
init thread 4, task 3
body i 3 str1 t4 thread 4 task 3
body i 2 str1 i 1 thread 1 task 1
body i 11 str1 i 10 thread 3 task 2
body i 4 str1 i 3 thread 4 task 3
body i 6 str1 i 2 thread 1 task 1
body i 12 str1 i 11 thread 3 task 2
body i 5 str1 i 4 thread 4 task 3
body i 7 str1 i 6 thread 1 task 1
body i 13 str1 i 12 thread 3 task 2
```