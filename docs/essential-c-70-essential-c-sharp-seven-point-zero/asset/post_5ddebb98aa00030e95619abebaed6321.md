
// if using C# 2.0
thermostat.OnTemperatureChange +=
    (newTemperature) =>
    {
        throw new InvalidOperationException();
    };
thermostat.OnTemperatureChange +=
    cooler.OnTemperatureChanged;
Console.Write("Enter temperature: ");
temperature = Console.ReadLine();
thermostat.CurrentTemperature = int.Parse(temperature);
}

Figure 14.3 shows an updated sequence diagram. Even though cooler and heater subscribed to receive messages, the lambda expression exception terminates the chain and prevents the cooler object from receiving notification.

![](img/ef6a8a417630b222bfb3f3b949facff0_624_0.png)

## Figure 14.3: Delegate Invocation with Exception Sequence Diagram

To avoid this problem so that all subscribers receive notification, regardless of the behavior of earlier subscribers, you must manually enumerate through the list of subscribers and call them individually. Listing 14.10 shows the updates required in the CurrentTemperature property. The results appear in Output 14.2.

## Listing 14.10: Handling Exceptions from Subscribers

```csharp
public class Thermostat
{
    // Define the event publisher
    public Action<float> OnTemperatureChange;

    public float CurrentTemperature
    {
        get { return _CurrentTemperature; }
        set
        {
            if (value != CurrentTemperature)
            {
                _CurrentTemperature = value;
                Action<float> onTemperatureChange = OnTemperatureChange;
                if (onTemperatureChange != null)
                {
                    List<Exception> exceptionCollection =
                        new List<Exception>();
                    foreach (
                        Action<float> handler in
                        onTemperatureChange.GetInvocationList())
                    {
                        try
                        {
                            handler(value);
                        }
                        catch (Exception exception)
                        {
                            exceptionCollection.Add(exception);
                        }
                    }
                    if (exceptionCollection.Count > 0)
                    {
                        throw new AggregateException(
                            "There were exceptions thrown by "
                            + "OnTemperatureChange event subscribers.",
                            exceptionCollection);
                    }
                }
            }
        }
    }
    private float _CurrentTemperature;
}
```

## Output 14.2

```
Enter temperature: 45
Heater: On
Error in the application
Cooler: Off
```

This listing demonstrates that you can retrieve a list of subscribers from a delegate's `GetInvocationList()` method. Enumerating over each item in this list returns the individual subscribers. If you then place each invocation of a subscriber within a try/catch block, you can handle any error conditions before continuing with the enumeration loop. In this example, even though the delegate subscriber throws an exception, cooler still receives notification of the temperature change. After all notifications have been sent, Listing 14.10 reports any exceptions by throwing an `AggregateException`, which wraps a collection of exceptions that are accessible by the `InnerExceptions` property. In this way, all exceptions are still reported and, at the same time, all subscribers are notified.

Practically, no null conditional was used in this example, as a significant amount of code was dependent on a non-null delegate.

## Method Returns and Pass-by-Reference

There is another scenario in which it is useful to iterate over the delegate invocation list instead of simply activating a notification directly. This scenario relates to delegates that either do not return void or have ref or out parameters. In the thermostat example, the `OnTemperatureChange` delegate is of type `Action<float>`, which returns void and has no out or ref parameters. As a result, no data is returned to the publisher. This consideration is important, because an invocation of a delegate potentially triggers notification to multiple subscribers. If each of the subscribers returns a value, it is ambiguous as to which subscriber's return value would be used.

If you changed `OnTemperatureChange` to return an enumeration value, indicating whether the device was on because of the temperature change, the new delegate would be of type `Func<float, Status>`, where `Status` was an enum with elements On and Off. All subscriber methods would have to use the same method signature as the delegate, and therefore, each would be required to return a status value. Also, since `OnTemperatureChange` might potentially correspond to a chain of delegates, it is necessary to follow the same pattern that you used for error handling. In other words, you must iterate through each delegate invocation list, using the `GetInvocationList()` method, to retrieve each individual return value. Similarly, delegate types that use ref and out parameters need special consideration. However, although it is possible to use this approach in exceptional circumstances, the guideline is to avoid this scenario entirely by only returning void.

## Understanding Events

There are two key problems with the delegates as you have used them so far in this chapter. To overcome these issues, C# uses the keyword event. In this section, you will see why you would use events, and how they work.

### Why Events?

This chapter and the preceding one covered all you need to know about how delegates work. Unfortunately, weaknesses in the delegate structure may inadvertently allow the programmer to introduce a bug. These issues relate to encapsulation that neither the subscription nor the publication of events can sufficiently control.

### Encapsulating the Subscription

As demonstrated earlier, it is possible to assign one delegate to another using the assignment operator. Unfortunately, this capability introduces a common source for bugs. Consider Listing 14.11.

## Listing 14.11: Using the Assignment Operator = Rather Than +=

```csharp
class Program
{
    public static void Main()
    {
        Thermostat thermostat = new Thermostat();
        Heater heater = new Heater(60);
        Cooler cooler = new Cooler(80);
        string temperature;

        // Note: Use new Action (cooler.OnTemperatureChanged)
        // if C# 1.0
        thermostat.OnTemperatureChange =
            heater.OnTemperatureChanged;

        // Bug: Assignment operator overrides
        // previous assignment
        thermostat.OnTemperatureChange =
            cooler.OnTemperatureChanged;

        Console.Write("Enter temperature: ");
        temperature = Console.ReadLine();
        thermostat.CurrentTemperature = int.Parse(temperature);
    }
}
```

Listing 14.11 is almost identical to Listing 14.7, except that instead of using the += operator, you use a simple assignment operator. As a result, when code assigns `cooler.OnTemperatureChanged` to `OnTemperatureChange`, `heater.OnTemperatureChanged` is cleared out because an entirely new chain is assigned to replace the previous one. The potential for mistakenly using an assignment operator, when the += assignment is intended, is so high that it would be preferable if the assignment operator were not even supported for objects except within the containing class. The event keyword provides this additional encapsulation so that you cannot inadvertently cancel other subscribers.

### Encapsulating the Publication

The second important difference between delegates and events is that events ensure that only the containing class can trigger an event notification. Consider Listing 14.12.

## Listing 14.12: Firing the Event from Outside the Events Container

```csharp
class Program
{
    public static void Main()
    {
        Thermostat thermostat = new Thermostat();
        Heater heater = new Heater(60);
        Cooler cooler = new Cooler(80);
        string temperature;
        
        // Note: Use new Action (cooler.OnTemperatureChanged)
        // if C# 1.0
        thermostat.OnTemperatureChange +=
            heater.OnTemperatureChanged;
        thermostat.OnTemperatureChange +=
            cooler.OnTemperatureChanged;
        thermostat.OnTemperatureChange(42);
    }
}
```

In Listing 14.12, `Program` can invoke the `OnTemperatureChange` delegate even though the `CurrentTemperature` on `thermostat` did not change. `Program`, therefore, triggers a notification to all `thermostat` subscribers that the temperature changed, even though there was no change in the `thermostat` temperature. As before, the problem with the delegate
