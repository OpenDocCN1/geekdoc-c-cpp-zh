```
while (true)
{
    state.ChangeState(i++);
}
}
```

In the Main method of the program, a new StateObject is created that is shared among all the tasks. Task objects are created by invoking the RaceCondition method with the lambda expression that is passed to the Run method of the Task. The main thread then waits for user input. However, there’s a good chance that the program will halt before reading user input, as a race condition will happen:

```
public void RaceConditions()
{
    var state = new StateObject();
    for (int i = 0; i < 2; i++)
    {
        Task.Run(() => new SampleTask().RaceCondition(state));
    }
}
```

When you start the program, you get race conditions. How long it takes until the first race condition happens depends on your system and whether you build the program as a release build or a debug build. With a release build, the problem happens more often because the code is optimized. If you have multiple CPUs in your system or dual-/quad-core CPUs, where multiple threads can run concurrently, the problem also occurs more often than with a single-core CPU. The problem occurs with a single-core CPU because thread scheduling is preemptive, but the problem doesn’t occur that often.

Figure 22.1 shows an assertion of the program in which the race condition occurred after 1121 loops. If you start the application multiple times, you always get different results.