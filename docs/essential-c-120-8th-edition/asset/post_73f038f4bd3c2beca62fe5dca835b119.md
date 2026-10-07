
# LISTING 14.5: Invoking a Delegate

```csharp
public class Thermostat
{
    // Define the event publisher
    public Action<float>? OnTemperatureChange { get; set; }

    public float CurrentTemperature
    {
        get { return _CurrentTemperature; }
        set
        {
            if(value != CurrentTemperature)
            {
                _CurrentTemperature = value;
                // If there are any subscribers,
                // notify them of changes in
                // temperature by invoking said subscribers
                OnTemperatureChange?.Invoke(value); // C# 6.0
            }
        }
    }

    private float _CurrentTemperature;
}
```

Notice the call to the Invoke() method that follows the null-conditional operator. Although this method may be called using only a dot operator, there is little point, since that is the equivalent of calling the delegate directly (see OnTemperatureChange(value) in Listing 14.4). An important advantage underlying the use of the null-conditional operator is special logic to ensure that after checking for null, there is no possibility that a subscriber might invoke a stale handler (one that has changed after checking for null), leaving the delegate again.

# Guidelines

- DO check that the value of a delegate is not null before invoking it.
- DO use the null-conditional operator prior to calling Invoke() starting in C# 6.0.

# ADVANCED TOPIC

## The -= Operator for a delegate Returns a New Instance
Given that a delegate is a reference type, it is perhaps somewhat surprising that assigning a local variable and using that local variable is sufficient for making the null check thread-safe. Since localOnChange refers to the same location as OnOnChange does, you might imagine that any changes in OnOnChange would be reflected in localOnChange as well.

This is not the case because, effectively, any calls made to OnTemperatureChange -= <subscriber> will not simply remove the delegate from OnTemperatureChange so that it contains one less delegate than before. Rather, such a call will assign an entirely new delegate to which localOnChange also refers.

# ADVANCED Delegate Invocation

### Thread-Safe Invocation
If subscribers can be added and removed from the delegate on different threads, it is wise (as noted earlier) to conditionally invoke it or copy the delegate reference into a local variable before checking it for null. Although this approach prevents the invocation of a null delegate, it does not avoid all possible race conditions. For example, one thread could copy the delegate, and then another thread could reset the delegate to null, and then the original thread would invoke the previous value of the delegate, thereby notifying a subscriber that is no longer on the list of subscribers. Subscribers in multithreaded programs should ensure that their code remains robust in this scenario; it is always possible that a “stale” subscriber will be invoked.

# Delegate Operators

To combine the two subscribers in the Thermostat example, you used the += operator. This operator takes the first delegate and adds the second delegate to the chain.

# Coding the Publish–Subscribe Pattern with Multicast Delegates

Now, after the first delegate’s method returns, the second delegate is called. To remove delegates from a delegate chain, use the -= operator, as shown in Listing 14.6 with Output 14.1.

# LISTING 14.6: Using the += and -= Delegate Operators

```csharp
//...
Thermostat thermostat = new();
Heater heater = new(60);
Cooler cooler = new(80);

Action<float> delegate1;
Action<float> delegate2;
Action<float> delegate3;

delegate1 = heater.OnTemperatureChanged;
delegate2 = cooler.OnTemperatureChanged;

Console.WriteLine("Invoke both delegates:");
delegate3 = delegate1;
delegate3 += delegate2;
delegate3(90);

Console.WriteLine("Invoke only delegate2");
delegate3 -= delegate1;
delegate3!(30);
//...
```

Invoke both delegates:
Heater: Off
Cooler: On
Invoke only delegate2
Cooler: Off

You can also use the + and - operators to combine delegates, as shown in Listing 14.7.

# LISTING 14.7: Using the + and - Delegate Operators

```csharp
//...
Thermostat thermostat = new();
Heater heater = new(60);
Cooler cooler = new(80);
```

# Chapter 14: Events

```csharp
Action<float> delegate1;
Action<float> delegate2;
Action<float> delegate3;
```

```csharp
delegate1 = heater.OnTemperatureChanged;
delegate2 = cooler.OnTemperatureChanged;
```

```csharp
Console.WriteLine("Combine delegates using + operator:");
delegate3 = delegate1 + delegate2;
delegate3(60);
```

```csharp
Console.WriteLine("Uncombine delegates using operator:");
delegate3 = (delegate3 - delegate2)!;
delegate3(60);
///...
```

Using the assignment operator clears out all previous subscribers and to replace them with new subscribers. This is an unfortunate characteristic of a delegate. It is simply too easy to mistakenly code an assignment when, in fact, the += operator is introduced. The solution, called events, is described in the "Understanding Events" section later in this chapter.

Both the + and - operators and their assignment equivalents, += and -=, are implemented internally using the static methods System.Delegate.Combine() and System.Delegate.Remove(), respectively. These methods take two parameters of type delegate. The first method, Combine(), joins the two parameters so that the first parameter refers to the second within the list of delegates. The second, Remove(), searches through the chain of delegates specified in the first parameter and returns the delegate specified by the second.

Interesting thing to note about Combine() is that either of its parameters can be null. If one of them is null, Combine() returns the non-null parameter. If both are null, Combine() returns null. This explains why you can call thermostat.OnTemperatureChange += delegate; and not throw an exception, even if the value of thermostat.OnTemperatureChange is still null.

# Coding the Publish–Subscribe Pattern with Multicast Delegates

### Sequential Invocation

Figure 14.1 highlights the sequential notification of both heater and cooler.

![](img/ffe0f34eac7523830420733690014d17_771_0.png)

FIGURE 14.1: Delegate invocation sequence

Although you coded only single call to OnTemperatureChange(), the call is broadcast to both subscribers. Thus, with one call, both cooler and heater are notified of the change in temperature. If you added more subscribers, they, too, would be notified by OnChange().

Although a single call, OnTemperatureChange(), caused the notification of each subscriber, the subscribers are still called sequentially, not simultaneously, because they are all called on the same thread of execution.

# ADVANCED Delegate Internals

### Multicast Delegate Internals

To understand how events work, you need to revisit the first examination of the System.Delegate type internals. Recall that the delegate keyword is alias for a type derived from System.MulticastDelegate. In turn, System.MulticastDelegate is derived from System.Delegate, which, for its part, is composed of an object reference (needed for nonstatic methods) and a method reference. When you create a delegate, the compiler automatically employs the System.MulticastDelegate type rather than the System.Delegate type. The MulticastDelegate class includes an object reference and a method reference, just like its delegate base class, but also contains a reference to another System.MulticastDelegate object.

When you add a method to a multicast delegate, the MulticastDelegate class creates a new instance of the delegate type, stores the object reference and the method reference for the added method into the new instance, and adds the new delegate as the next item in a list of delegate instances. In effect, the MulticastDelegate class maintains a list of Delegate objects. Conceptually, you can represent the thermostat example as shown in Figure 14.2.

![](img/ffe0f34eac7523830420733690014d17_772_0.png)

FIGURE 14.2: Multicast delegates chained together
