Now the assignment of `CurrentTemperature` includes some special logic to notify subscribers of changes in `CurrentTemperature`. The call to notify all subscribers is simply the single C# statement, `OnTemperatureChange(value)`. This single statement publishes the temperature change to both the `cooler` and `heater` objects. Here, you see in practice that the ability to notify multiple subscribers using a single call is why delegates are more specifically known as multicast delegates, which are discussed further later in the chapter.

# Check for null

One important part of event publishing code is missing from Listing 14.4. If no subscriber has registered to receive the notification, `OnTemperatureChange` would be `null`, and executing the `OnTemperatureChange(value)` statement would throw a `NullReferenceException`. To avoid this scenario, it is necessary to check for `null` before firing the event. Listing 14.5 demonstrates how to do this using C# 6.0's null conditional operator before calling `Invoke()`.

# LISTING 14.5: Invoking a Delegate

```
```csharp
public class Thermostat
{
    ...
    public float CurrentTemperature
    {
        get { return _CurrentTemperature; }
        set
        {
            if (value != CurrentTemperature)
            {
                _CurrentTemperature = value;
                // If there are any subscribers,
                // notify them of changes in temperature
                // by invoking said subscribers
                OnTemperatureChange?.Invoke(value); // C# 6.0
            }
        }
    }
    private float _CurrentTemperature;
}
```
```

Notice the call to the `Invoke()` method that follows the null conditional. Although this method may be called using only a dot operator, there is little point, since that is the equivalent of calling the delegate directly