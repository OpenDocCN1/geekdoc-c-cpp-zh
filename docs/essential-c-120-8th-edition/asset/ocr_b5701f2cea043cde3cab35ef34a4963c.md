# 746 Chapter 14: Events

```
public float CurrentTemperature;
// ...
private float _CurrentTemperature;
}
```

The new Thermostat class has four changes relative to the original class. First, the OnTemperatureChange property has been removed, and OnTemperatureChange has instead been declared as a public field. This seems contrary to solving the earlier encapsulation problem. It would make more sense to increase the encapsulation, not decrease it by making a public field. However, the second change was to add the event keyword immediately before the field declaration. This simple change provides all the encapsulation needed. By adding the event keyword, you prevent the use of the assignment operator on a public delegate field (e.g., thermostat.OnTemperatureChange = cooler .TemperatureChanged). In addition, only the containing class is able to invoke the delegate that triggers the publication to all subscribers (e.g., disallowing thermostat.OnTemperatureChange(42) from the class). In other words, the event keyword provides the needed encapsulation that prevents any external class from publishing an event or unsubscribing previous subscribers it did not add. This resolves the two previously mentioned issues with plain delegates and is one of the key reasons for the inclusion of the event keyword in C#.

Another potential pitfall with plain delegates is that it is all too easy to forget to check for null before invoking the delegate. This omission may result in an unexpected NullReferenceException. Fortunately, the encapsulation that the event keyword provides an alternative possibility during declaration (or within the constructor), as shown in Listing 14.12. Notice that when declaring the event, we assign delegate { }—a-null delegate, which does nothing. By assigning the empty delegate, we can raise the event when checking whether there are any subscribers.(This behavior is similar to assigning an array of zero items to a variable. Doing allows the invocation of an array member without first checking whether the variable is null.) Of course, if there is any change that the delegate could be reassigned to have a null value, a check is still required. However, because the

+   1. Using the null conditional operator in C# 6.0.