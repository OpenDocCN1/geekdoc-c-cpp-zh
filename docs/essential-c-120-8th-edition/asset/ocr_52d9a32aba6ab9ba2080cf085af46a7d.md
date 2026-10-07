```
// Bug: Assignment operator overrides
// previous assignment
thermostat.OnTemperatureChange =
cooler.OnTemperatureChanged;
```

```
Console.Write("Enter temperature: ");
string? temperature = Console.ReadLine();
if (!int.TryParse(temperature, out int currentTemperature))
{
    Console.WriteLine($"{temperature}" is not a valid integer.");
    return;
}
thermostat.CurrentTemperature = currentTemperature;
```

Listing 14.10 is almost identical to Listing 14.6, except that instead of the += operator, you use a simple assignment operator. As a result, when the code assigns cooler.OnTemperatureChanged to OnTemperatureChange, heater.OnTemperatureChanged is cleared because an entirely new chain is assigned to replace the previous one. The potential for mistakenly using an assignment operator, when the += assignment was intended, is so high that it would be preferable if the assignment operator were not supported for objects except within the containing class. The event keyword provides this additional encapsulation so that you cannot inadvertently cancel other subscribers.

# Encapsulating the Publication

The second important difference between delegates and events is that events ensure that only the containing class can trigger an event notification. Consider Listing 14.11.

Listing 14.11: Firing the Event from Outside the Events Container

```
public class Program
{
    public static void Main()
    {
        Thermostat thermostat = new();
        Heater heater = new(60);
        Cooler cooler = new(80);
    }
```