```
private float _CurrentTemperature;
}
```

You usually specify the sender using the container class (this) because it is the only class that can invoke the delegate for events.

In this example, the subscriber could cast the sender parameter to Thermostat and access the current temperature that way, as well as via the TemperatureArgs instance. However, the current temperature on the Thermostat instance may change via a different thread. When events may occur due to state changes, passing the previous value along with the new value is a pattern frequently used to control which state transitions are allowable.

Guidelines
DO check the value of a delegate is not null before invoking it (possibly by using the null-conditional operator in C# 6.0).
DO pass the instance of the class as the value of the sender for nonstatic events.
DO pass null as the sender for static events.
DO NOT pass null as the value of the eventArgs argument.
DO use System.EventArgs or a type that derives from System.EventArgs for a TEventArgs type.
CONSIDER using System.Event.EventArgs as the event argument type (TEventArgs) unless you are sure the event will never need to carry any data.

# ADVANCED TOPIC

# Event Internals

As mentioned earlier, events provide encapsulation that restricts external classes to only subscribing and unsubscribing methods to the publisher via the += and -= operators respectively. In addition, they restrict classes, other than the containing class, from invoking the event. To do so, the C# compiler takes the public delegate