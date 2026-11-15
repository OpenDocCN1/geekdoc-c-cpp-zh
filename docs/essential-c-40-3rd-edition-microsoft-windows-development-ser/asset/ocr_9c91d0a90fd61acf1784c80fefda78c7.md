With these two changes, you provide the necessary encapsulation and all other functionality remains the same. However, an additional change occurs in the delegate declaration in the code in Listing 13.14. To follow standard C# coding conventions, you changed OnTemperatureChangeHandler so that the single temperature parameter was replaced with two new parameters, sender and temperatureArgs. This change is not something that the C# compiler will enforce, but passing two parameters of these types is the norm for declaring a delegate intended for an event.

The first parameter, sender, should contain an instance of the class that invoked the delegate. This is especially helpful if the same subscriber method registers with multiple events—for example, if the heater.OnTemperatureChanged event subscribes to two different Thermostat instances. In such a scenario, either Thermostat instance can trigger a call to heater.OnTemperatureChanged. In order to determine which instance of Thermostat triggered the event, you use the sender parameter from inside Heater.OnTemperatureChanged().

The second parameter, temperatureArgs, is of type Thermostat.TemperatureArgs. Using a nested class is appropriate because it conforms to the same scope as the OnTemperatureChangeHandler delegate itself. The important part about TemperatureArgs, at least as far as the coding convention goes, is that it derives from System.EventArgs. The only significant property on System.EventArgs is Empty and it is used to indicate that there is no event data. When you derive TemperatureArgs from System.EventArgs, however, you add an additional property, NewTemperature, as a means to pass the temperature from the thermostat to the subscribers.

To summarize the coding convention for events: The first argument, sender, is of type object and it contains a reference to the object that invoked the delegate. The second argument is of type System.EventArgs or something that derives from System.EventArgs but contains additional data about the event. You invoke the delegate exactly as before, except for the additional parameters. Listing 13.15 shows an example.

# LISTING 13.15: Firing the Event Notification

```
public class Thermostat
{
    ...
}
```