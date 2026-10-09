**LISTING 14.19: Custom add and remove Handlers**

```
```
public class Thermostat
{
    public class TemperatureArgs: System.EventArgs
    {
        ...
    }
```
```

```
```
// Define the event publisher
public event EventHandler<TemperatureArgs> OnTemperatureChange
{
    add
    {
        _OnTemperatureChange = (TemperatureChangeHandler)
            System.Delegate.Combine(value, _OnTemperatureChange);
    }
    remove
    {
        _OnTemperatureChange = (TemperatureChangeHandler)
            System.Delegate.Remove(_OnTemperatureChange, value);
    }
}
protected EventHandler<TemperatureArgs> _OnTemperatureChange;
```
```

```
```
public float CurrentTemperature
{
    ...
}
private float _CurrentTemperature;
```
```

In this case, the delegate that stores each subscriber, _OnTemperatureChange, was changed to protected. In addition, implementation of the add block switches around the delegate storage so that the last delegate added to the chain is the first delegate to receive a notification.

# SUMMARY

Now that we have described events, it is worth mentioning that, in general, method references are the only cases where it is advisable to work with a delegate variable outside the context of an event. In other words, given the additional encapsulation features of an event and the ability to customize the implementation when necessary, the best practice is always to use events for the publish-subscribe pattern.

2.0