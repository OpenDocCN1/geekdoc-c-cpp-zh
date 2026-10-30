# LISTING 7-30 The primary IStopwatch implementation uses the Stopwatch class.

```
public class StopwatchAdapter : IStopwatch
{
    public StopwatchAdapter(Stopwatch stopwatch)
    {
        this.stopwatch = stopwatch;
    }

    public void Start()
    {
        stopwatch.Start();
    }

    public long Stop()
    {
        stopwatch.Stop();
        var elapsedMilliseconds = stopwatch.ElapsedMilliseconds;
        stopwatch.Reset();
        return elapsedMilliseconds;
    }

    private readonly Stopwatch stopwatch;
}
```

Note that you could have chosen to implement IStopwatch as a subclass of the System.Diagnostics.Stopwatch class and used the existing Start and Stop methods. However, the Start method acts to resume functionality when a stopwatch is stopped, but what you need to do is call Reset after you call Stop, and retrieve the ElapsedMilliseconds property value in between. This is another example of the Adapter pattern.

# Decorating properties and events

So far, you have learned how to decorate the methods of an interface, but what about properties and events? Both of these syntactic elements can also be decorated, as long as you do not use auto-properties or auto-events; you need to explicitly define both in order to decorate them properly.

Listing 7-31 shows the manual creation of a property, but rather than having a backing field, for both the getter and the setter this code delegates to the decorated instance of the interface.

# LISTING 7-31 Properties can also use the Decorator pattern, just like methods.

```
public class ComponentDecorator : IComponent
{
    public ComponentDecorator(IComponent decoratedComponent)
    {
        this.decoratedComponent = decoratedComponent;
    }
}
```