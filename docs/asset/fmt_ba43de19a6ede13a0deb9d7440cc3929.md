
而不是直接检查 `null`，此代码首先将 `OnTemperatureChange` 分配给第二个委托变量 `localOnChange`。此简单修改可确保如果在检查 `null` 和发送通知之间（由不同线程）删除了所有 `OnTemperatureChange` 订阅者，您不会引发 `NullReferenceException`。

本书其余部分的示例都将依赖 C# 6.0 的空条件运算符进行委托调用。

## Guidelines

- DO check that the value of a delegate is not null before invoking it.
- DO use the null conditional operator prior to calling `Invoke()` starting in C# 6.0.

## ADVANCED TOPIC

### -= Operator for a Delegate Returns a New Instance

鉴于委托是引用类型，分配一个局部变量然后使用该局部变量足以使空检查线程安全，这也许有些令人惊讶。由于 `localOnChange` 指向与 `OnTemperatureChange` 相同的位置，您可能会想象 `OnTemperatureChange` 的任何更改也会反映在 `localOnChange` 中。

情况并非如此，因为实际上，任何对 `OnTemperatureChange -= <listener>` 的调用都不会简单地从 `OnTemperatureChange` 中删除一个委托，使其包含的委托比之前少。相反，此类调用将分配一个全新的多播委托，而不会对 `localOnChange` 也指向的原始多播委托产生任何影响。

## ADVANCED TOPIC

### Thread-Safe Delegate Invocation

如果订阅者可以在不同线程上添加到委托并从中删除，那么明智的做法是（正如前面所述）在检查 `null` 之前将委托引用复制到局部变量。虽然这种方法可以防止调用 `null` 委托，但它并不能避免所有可能的竞争条件。例如，一个线程可以进行复制，然后另一个线程可以将委托重置为 `null`，然后原始线程可以调用委托的先前值，从而通知不再在订阅者列表中的订阅者。多线程程序中的订阅者应确保其代码在此场景下保持健壮；始终有可能“过时”的订阅者会被调用。

## Delegate Operators

为了将 `Thermostat` 示例中的两个订阅者组合在一起，您使用了 `+=` 运算符。此运算符采用第一个委托并将第二个委托添加到链中。现在，在第一个委托的方法返回后，将调用第二个委托。要从委托链中删除委托，请使用 `-=` 运算符，如清单 13.7 所示。

### LISTING 13.7: Using the += and -= Delegate Operators

```
// ...
Thermostat thermostat = new Thermostat();
Heater heater = new Heater(60);
Cooler cooler = new Cooler(80);

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
delegate3(30);
// ...
```

The results of Listing 13.7 appear in Output 13.1.

### OUTPUT 13.1

```
Invoke both delegates:
Heater: Off
Cooler: On
Invoke only delegate2
Cooler: Off
```

Furthermore, you can also use the `+` and `-` operators to combine delegates, as Listing 13.8 shows.

### LISTING 13.8: Using the + and - Delegate Operators

```
// ...
Thermostat thermostat = new Thermostat();
Heater heater = new Heater(60);
Cooler cooler = new Cooler(80);

Action<float> delegate1;
Action<float> delegate2;
Action<float> delegate3;

// Note: Use new Action (cooler.OnTemperatureChanged)
// for C# 1.0 syntax.
```

```
delegate1 = heater.OnTemperatureChanged;
delegate2 = cooler.OnTemperatureChanged;

Console.WriteLine("Combine delegates using + operator:");
delegate3 = delegate1 + delegate2;
delegate3(60);

Console.WriteLine("Uncombine delegates using - operator:");
delegate3 = delegate3 - delegate2;
delegate3(60);
// ...
```

Use of the assignment operator clears out all previous subscribers and allows you to replace them with new subscribers. This is an unfortunate characteristic of a delegate. It is simply too easy to mistakenly code an assignment when, in fact, the `+=` operator is intended. The solution, called events, appears in the “Events” section later in this chapter.

Both the `+` and `-` operators and their assignment equivalents, `+=` and `-=`, are implemented internally using the static methods `System.Delegate.Combine()` and `System.Delegate.Remove()`. These methods take two parameters of type delegate. The first method, `Combine()`, joins the two parameters so that the first parameter points to the second within the list of delegates. The second, `Remove()`, searches through the chain of delegates specified in the first parameter and then removes the delegate specified by the second parameter.

One interesting thing to note about the `Combine()` method is that either or both of its parameters can be `null`. If one of them is `null`, `Combine()` returns the non-null parameter. If both are `null`, `Combine()` returns `null`. This explains why you can call `thermostat.OnTemperatureChange += heater.OnTemperatureChanged;` and not throw an exception, even if the value of `thermostat.OnTemperatureChange` is still `null`.

## Sequential Invocation

Figure 13.1 highlights the sequential notification of both heater and cooler.

Although you coded only a single call to `OnTemperatureChange()`, the call is broadcast to both subscribers. Thus, with just one call, both cooler and heater are notified of the change in temperature. If you added more subscribers, they, too, would be notified by `OnTemperatureChange()`.

![](img/25683ccec0773ba5b8794b11f2b12877_591_0.png)

### FIGURE 13.1: Delegate Invocation Sequence Diagram

Although a single call, `OnTemperatureChange()`, caused the notification of each subscriber, the subscribers are still called sequentially, not simultaneously, because they are all called on the same thread of execution.

## ADVANCED TOPIC

### Multicast Delegate Internals

To understand how events work, you need to revisit the first examination of the `System.Delegate` type internals. Recall that the `delegate` keyword is an alias for a type derived from `System.MulticastDelegate`. In turn, `System.MulticastDelegate` is derived from `System.Delegate`, which, for its part, is composed of an object reference (needed for nonstatic methods) and a method reference. When you create a delegate, the compiler automatically employs the `System.MulticastDelegate` type rather than the `System.Delegate` type. The `MulticastDelegate` class includes an object reference and a method reference, just like its `Delegate` base class, but it also contains a reference to another `System.MulticastDelegate` object.

When you add a method to a multicast delegate, the `MulticastDelegate` class creates a new instance of the delegate type, stores the object reference and the method reference for the added method into the new instance, and adds the new delegate instance as the next item in a list of delegate instances. In effect, the `MulticastDelegate` class maintains a linked list of `Delegate` objects. Conceptually, you can represent the thermostat example as shown in Figure 13.2 on the facing page (denoted as a continuation of this advanced topic).

When invoking a multicast delegate, each delegate instance in the linked list is called sequentially. Generally, delegates are called in the order they were added, but this behavior is not specified within the CLI specification. Furthermore, it can be overridden. Therefore, programmers should not depend on an invocation order.

## Error Handling

Error handling makes awareness of the sequential notification critical. If one subscriber throws an exception, later subscribers in the chain do not receive the notification. Consider, for example, what would happen if you changed the `Heater`’s `OnTemperatureChanged()` method so that it threw an exception, as shown in Listing 13.9.

![](img/25683ccec0773ba5b8794b11f2b12877_593_0.png)

### FIGURE 13.2: Multicast Delegates Chained Together

### LISTING 13.9: OnTemperatureChanged() Throwing an Exception

```
class Program
{
    public static void Main()
    {
        Thermostat thermostat = new Thermostat();
        Heater heater = new Heater(60);
        Cooler cooler = new Cooler(80);
        string temperature;

        thermostat.OnTemperatureChange +=
            heater.OnTemperatureChanged;
        // Using C# 3.0. Change to anonymous method
        // if using C# 2.0.
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
}
```

![](img/25683ccec0773ba5b8794b11f2b12877_594_0.png)

### FIGURE 13.3: Delegate Invocation with Exception Sequence Diagram

Figure 13.3 shows an updated sequence diagram. Even though cooler and heater subscribed to receive messages, the lambda expression exception terminates the chain and prevents the cooler object from receiving notification.
