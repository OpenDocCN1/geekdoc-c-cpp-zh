# Coding the Publish–Subscribe Pattern with Multicast Delegates 731

```
Heater heater = new(60);
Cooler cooler = new(80);
```

```
thermostat.OnTemperatureChange +=
heater.OnTemperatureChanged;
thermostat.OnTemperatureChange +=
cooler.OnTemperatureChanged;
```

```
Console.Write("Enter temperature: ");
string? temperature = Console.ReadLine();
if (!int.TryParse(temperature, out int currentTemperature))
{
    Console.WriteLine($"{{temperature}" is not a valid integer.");
    return;
}
thermostat.CurrentTemperature = currentTemperature;
```

The code in this listing has registered two subscribers (heater .OnTemperatureChanged and cooler.OnTemperatureChanged) to the OnTemperatureChange delegate by directly assigning them using the += operator.

By taking the value the user has entered as input, you can set the CurrentTemperature of thermostat. However, you have not yet written any code to publish the change temperature event to subscribers.

# Invoking a Delegate

Every time the CurrentTemperature property on the Thermostat class changes, you want to invoke the delegate to notify the subscribers (heater and cooler) of the change in temperature. To achieve this goal, you must modify the CurrentTemperature property to save the new value and publish a notification to each subscriber. The code modification appears in Listing 14.4.

Listing 14.4: Invoking a Delegate without Checking for null

```
public class Thermostat
{
    // ...
    public float CurrentTemperature
```