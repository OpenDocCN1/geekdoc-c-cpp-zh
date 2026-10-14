Click here to view code image

```
public class ProfilingComponent : IComponent
{
    public ProfilingComponent(IComponent decoratedComponent, IStopwatch stopwatch)
    {
        this.decoratedComponent = decoratedComponent;
        this.stopwatch = stopwatch;
    }

    public void Something()
    {
        stopwatch.Start();
        decoratedComponent.Something();
        var elapsedMilliseconds = stopwatch.Stop();
        Console.WriteLine("The method took {0} seconds to complete", elapsedMilliseconds
/
1000);
    }

    private readonly IComponent decoratedComponent;
    private readonly IStopwatch stopwatch;
}
```

Now that the ProfilingComponent class does not depend directly on the System.Diagnostics.Stopwatch class, you can vary the implementation of the IStopwatch class. A LoggingStopwatch decorator is created, as shown in Listing 5-29, to enhance any further IStopwatch implementations with logging facilities.

# LISTING 5-29 The LoggingStopwatch decorator is an IStopwatch implementation that logs and delegates.

Click here to view code image

```
public class LoggingStopwatch : IStopwatch
{
    public LoggingStopwatch(IStopwatch decoratedStopwatch)
    {
        this.decoratedStopwatch = decoratedStopwatch;
    }

    public void Start()
    {
        decoratedStopwatch.Start();
        Console.WriteLine("Stopwatch started...");
```