An example with trains is shown here. Obviously, this simple example doesn't protect a shared resource for real (just an imaginary railway segment). True use of semaphores includes protecting a shared resource pool with an upper bound on the number of uses that are permitted simultaneously. Such an example is shown on MSDN.

```
var rnd = new Random();

var railwaySemaphore = new Semaphore(2, 2);
for (int i = 0; i < 10; i++)
{
    new Thread(() =>
    {
        // Time to leave the railway station.
        Thread.Sleep(rnd.Next(500, 8000));
        Console.WriteLine(Thread.CurrentThread.Name + " departing.");

        // Time to reach the semaphore next to the track.
        Thread.Sleep(rnd.Next(100, 5000));
        Console.WriteLine(Thread.CurrentThread.Name + " at signal.");

        // Waiting for the first signal.
        // The train is allowed to pass if no two trains are in the segment.
        railwaySemaphore.WaitOne();
        Console.WriteLine(Thread.CurrentThread.Name + " passed signal.");

        // Time to reach the end of the protected railway segment.
        Thread.Sleep(rnd.Next(2000, 4000));
        Console.WriteLine(Thread.CurrentThread.Name + " exited segment.");
        railwaySemaphore.Release();
    }) { Name = "Train " + i }.Start();
}
```

If the semaphore works correctly (it does), you shouldn't see more than two messages about a train passing the signal without a train exiting the segment first. It's left as an exercise for UI-savvy readers to implement a graphical visualization of the track, the signal, and the different trains driving over the railway.

Just like mutexes, semaphores are a built-in operating system primitives exposed to managed code. In the code shown here, we've been using a local semaphore without a name. However, constructor overloads exist, as well as a static OpenExisting method, to work with named semaphores. Such semaphore objects can be used across several processes to coordinate use of a shared resource pool, for instance.

Because of their impact on the scheduling of operating system threads (putting them in a waiting blocked state while acquiring the semaphore through WaitOne), you need to account for a certain overhead. To reduce this overhead in particular scenarios, a new type