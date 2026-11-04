To be able to unhook our CountDown event handlers, we have to lift them into a local variable, as just shown:

```
```csharp
var countDown = new CountDown(5);

// Hook up event handlers
Action<uint> tickHandler = currentSecond => Console.WriteLine(currentSecond);
Action finishedHandler = () => {
    Console.Beep();

    // Finished has been called: we can unhook both Tick and Finished now.
    countDown.Tick -= tickHandler;
    countDown.Finished -= finishedHandler;
};

countDown.Tick += tickHandler;
countDown.Finished += finishedHandler;

countDown.Start();
```
```

The preceding code is almost right; it just doesn't compile yet. Conceptually, everything looks right, though: We create handler delegates of type Action first and hook them up using regular += syntax later. Inside the event handler for Finished, we can unhook those again based on our knowledge of the event protocol of CountDown.

The remaining issue (that prevents us from compiling the preceding code) is rather subtle. Take a closer look at the finishedHandler lambda expression. While we're defining it, we're using it inside its own body on the last line. In more technical terms, we're defining a recursive lambda expression, which is something the language doesn't permit in this syntactical form, as illustrated in Figure 18.14.

![](bbox=[0.091, 0.65, 0.642, 0.837])

# FIGURE 18.14 Recursive lambda expressions make the compiler unhappy.