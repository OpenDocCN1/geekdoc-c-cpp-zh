Listing 14.11 is almost identical to Listing 14.7, except that instead of using the += operator, you use a simple assignment operator. As a result, when code assigns `cooler.OnTemperatureChanged` to `OnTemperatureChange`, `heater.OnTemperatureChanged` is cleared out because an entirely new chain is assigned to replace the previous one. The potential for mistakenly using an assignment operator, when the += assignment is intended, is so high that it would be preferable if the assignment operator were not even supported for objects except within the containing class. The event keyword provides this additional encapsulation so that you cannot inadvertently cancel other subscribers.

# **Encapsulating the Publication**

The second important difference between delegates and events is that events ensure that only the containing class can trigger an event notification. Consider Listing 14.12.

**LISTING 14.12: Firing the Event from Outside the Events Container**

```
```
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
```

In Listing 14.12, `Program` can invoke the `OnTemperatureChange` delegate even though the `CurrentTemperature` on `thermostat` did not change. `Program`, therefore, triggers a notification to all `thermostat` subscribers that the temperature changed, even though there was no change in the `thermostat` temperature. As before, the problem with the delegate