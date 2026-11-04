
## MESSAGE PUMPS TO THE RESCUE

This problem doesn't really exist in UI applications based on Windows Forms or Windows Presentation Foundation (WPF) because those have a *message pump* that keeps the main thread occupied until an exit message is posted to the message queue. Such an exit message arrives when the program's main window is closed or programmatic calls are made.

In our example, the Console.ReadLine call effectively blocks the main thread, waiting for the user to press Enter to terminate the program. There are cleaner ways to deal with this problem, though, and again the IAsyncResult objects returned by BeginInvoke provide the key to success.

One of the properties on IAsyncResult is called AsyncWaitHandle and returns a so-called *wait handle* that provides a way to wait for the background work to complete. For the Main method to use those, we'll return the wait handle from the method:

```csharp
static WaitHandle CalculateFib(uint n) {
    ...
    var asyncRes = fibN.BeginInvoke(asyncResult => {
        ...
        uint result = fibN.EndInvoke(asyncResult);
        ...
    }, null);
    ...
    return asyncRes.AsyncWaitHandle;
}
```

Back in Main, we receive all of those WaitHandle objects, which we can collect in an array. Based on this, we can express our desire to block until all the background work is done, as follows:

```csharp
static void Main() {
    const int N = 20;

    var waitHandles = new WaitHandle[N];
    for (uint n = 1; n <= N; n++) {
        waitHandles[n - 1] = CalculateFib(n);
    }

    WaitHandle.WaitAll(waitHandles);
}
```

WaitHandle.WaitAll basically tells the CLR to block until all the background threads associated with the wait handles have finished.

### NOTE

To be really honest, the preceding code isn't completely right just yet. Even though WaitAll will block and prevent the main thread from finishing until all asynchronous invocations complete, this doesn't take into account that the callback procedures (in our case, responsible for printing the result to the console) can take some time to complete. Therefore, it's still possible for the main thread to terminate before all callbacks have completed their jobs.

We won't go into detail about how to fix this defect right now but defer discussion about more thread synchronization primitives and techniques until Chapter 29. Nevertheless, this proves that parallel computation isn't a simple thing to get right under all circumstances. Rest assured, APIs have improved significantly over the years as parallel, asynchronous, and reactive computing has become more and more important.

Refer to Figure 17.24 for a moment and observe some apparent oddities in the output. One thing you'll notice is that Fib(5) returned before Fib(4). Out-of-order arrival is common when doing background processing because the runtime's and operating system's thread-scheduling mechanisms are involved. An even more extreme case is visible with Fib(7)'s completion message arriving after Fib(12)'s. Often, different background tasks have very different performance profiles (for example, because of latency experienced when making network calls and such).

For all of those reasons, you can't expect in-order arrival of asynchronous calls. Even more, every time you run the program you'll see different patterns due to differences in the "dynamics" of the system at the point the program runs. (Other threads in the OS may be competing with your application's threads.)

So what if we want to keep things in order somehow and print some progress to the screen while a number is being computed, as we promised near the beginning of this section? Using IAsyncResult's IsCompleted property, we can also poll for the completion of an asynchronous call:

```csharp
static void CalculateFib(uint n) {
    Func<uint> fibN = () => Fibonacci(n);

    var asyncResult = fibN.BeginInvoke(_ => { }, null);
    while (!asyncResult.IsCompleted) {
        Console.Write(".");
        Thread.Sleep(500);
    }
    Console.WriteLine();

    uint result = fibN.EndInvoke(asyncResult);
    Console.WriteLine($"Fib({0}) = {1}", n, result);
}
```

This code deserves a detailed explanation. We already know how we created the fibN delegate, so let's skip that part. The first important difference is about the absence of a meaningful callback function specified to BeginInvoke. Here we're passing a funky-looking lambda expression:

```
_ => { }
```

Recall that the expected argument is an AsyncCallback delegate, which takes in one of those IAsyncResult objects and returns void. Because we don't want to use a callback procedure (we're going to poll for completion status later), we don't care about the argument passed in to that lambda expression. It turns out a plain underscore character is a valid identifier in C#, so it's a handy, compact way to express this: "I have a lambda expression parameter here, but I don't care about it." And obviously, to create a delegate that doesn't do anything, we specify an empty body, hence the use of { }.

### NOTE

Quite frankly, this _ => { } trick is not required for the preceding code because BeginInvoke also accepts a null reference for its AsyncCallback argument. However, I thought it was the ideal time and place to reveal this little trick that comes in handy from time to time: _ is a valid C# identifier, and its use for a "don't care" variable name can prove useful in such situations.

Nevertheless, now that you know _ is a proper identifier, you shouldn't go off and start writing code like this:

```
(_, __, ___) => (_ + __) * ___;
```

No matter how aesthetically pleasing this may be to the trained (ASCII-art-savvy) eye, it's just asking for nonmaintainable and unreadable code! Also keep in mind that this is nothing but a trick and not a proper language feature of its own (because you can't have multiple "don't care" arguments with the same "_" name): To the compiler, it's just another variable name that may clash with other variables already in scope.

After starting the asynchronous call, we start polling for its completion status by checking the IsCompleted property periodically in a while loop. Notice we sleep inside the loop body for half a second (an interval that can be adjusted depending on the expected performance profile of the call being polled for) before checking again. This avoids busy waiting, which is a bad practice that drives your CPU to full utilization with no benefit other than heating the chip. Every time we fail to see a completed status, we print an additional dot to the screen. This signals to the user we're still alive but waiting for the operation to complete.

Figure 17.25 shows the result of restructuring our code with the polled-based waiting and printing of "status dots."

![](img/a16f85e62ce9bdc527f4b09dbfe26092_852_0.png)

FIGURE 17.25 Asynchronous computation with status polling and reporting.

Notice that categorization of blocking versus nonblocking depends on your point of view when looking at the code. First, from CalculateFib's point of view, the call to the fibN delegate is no longer blocking due to the use of BeginInvoke. However, when looking at the CalculateFib method from Main's point of view, that one is still blocking because it doesn't return before the result of the calculation is printed to the screen (by means of the polling loop inside).

## EXERCISE FOR THE READER

Figure 17.25 does not completely correspond to the code shown before because it still reports the measured time for the calculation. Extending the sample code by enabling it to report timing information accurately is left as an exercise for you.

Notice this is not as easy as it might seem at first: Because we're sleeping 500 milliseconds at a time when polling for completion status, the naive approach of wrapping the loop in a Stopwatch would always report multiples of 500 milliseconds (approximately).

One little tip: Use the BeginInvoke callback procedure to stop the Stopwatch as soon as the asynchronous call finishes.

## DON'T BLOCK THE MESSAGE LOOP

In reality, we would likely perform more useful work while we're waiting for an asynchronous operation to complete. If the result of the operation is not essential to continue all further processing in the system, we can start doing other work in parallel. But even if we really depend on the value to come back before we can do more meaningful work, asynchronous computing is beneficial because we can keep the user informed about the application not being fatally hung. I bet readers have seen the scenery illustrated in Figure 17.26 far too often.
