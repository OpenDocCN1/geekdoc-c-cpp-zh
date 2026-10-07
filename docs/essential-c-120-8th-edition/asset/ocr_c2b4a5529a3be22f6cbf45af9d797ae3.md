event keyword restricts assignment to occur only within the class, any reassignment of the delegate could occur only from within the class. Assuming null is never assigned, there will be no need to check for null whenever the code invokes the delegate.5

# Coding Conventions

All you need to do to gain the desired functionality is to change the original delegate variable declaration to a field and add the event keyword. With these two changes, you provide the necessary encapsulation; all other functionality remains the same. However, an additional change occurs in the delegate declaration in the code in Listing 14.12. To follow standard C# coding conventions, you should replace Action<float> with a new delegate type: EventHandler<TEventArgs>, a Common Language Runtime (CLR) type whose declaration is shown in Listing 14.13.

LISTING 14.13: The Generic Event Handler Type

```
public delegate void EventHandler<TEventArgs>(nobject sender, TEventArgs e)
where TEventArgs : EventArgs;
```

The result is the single parameter in the Action<TEventArgs> delegate type is replaced with two new parameters—one for the publisher or “sender” and a second for the event data. This change is not something that the C# compiler will enforce, but passing two parameters of these types is the norm for a delegate intended for an event.

The first parameter, sender, contains an instance of the class that invoked the delegate. This is especially helpful if the same subscriber registers with multiple events—for example, the heater.OnChanged event subscribes to two different Thermostat instances. In such a scenario, either Thermostat instance can trigger a call to OnTemperatureChanged. To determine which instance of Thermostat triggered the event, you use the sender parameter from inside Heater.OnTemperatureChanged(). If the

5. While rare, note that this pattern doesn’t work when the event is contained within a struct.