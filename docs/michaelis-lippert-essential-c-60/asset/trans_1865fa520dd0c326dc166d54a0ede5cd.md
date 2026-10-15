

```
public Action<float> OnTemperatureChange { get; set; }
public float CurrentTemperature { get; set; }
}
```

Thermostat 包含一个名为 OnTemperatureChange 的属性，其类型为 Action<float> 委托类型。OnTemperatureChange 存储一个订阅者列表。请注意，只需要一个委托字段即可存储所有订阅者。换句话说，Cooler 和 Heater 类都将从这个单一发布者接收温度变化的通知。

Thermostat 的最后一个成员是 CurrentTemperature 属性。此属性设置并检索 Thermostat 类报告的当前温度值。

## Hooking up the Publisher and Subscribers

最后，我们在 Main() 方法中将所有这些部分组合在一起。清单 13.3 显示了 Main() 可能的样子示例。

### LISTING 13.3: Connecting the Publisher and Subscribers

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
        thermostat.OnTemperatureChange +=
            cooler.OnTemperatureChanged;

        Console.Write("Enter temperature: ");
        temperature = Console.ReadLine();
        thermostat.CurrentTemperature = int.Parse(temperature);
    }
}
```

此清单中的代码已通过直接使用 += 运算符将两个订阅者（heater.OnTemperatureChanged 和 cooler.OnTemperatureChanged）注册到 OnTemperatureChange 委托。

通过获取用户输入的温度值，您可以设置 thermostat 的 CurrentTemperature。然而，您尚未编写任何代码来向订阅者发布温度变化事件。

## Invoking a Delegate

每次 Thermostat 类上的 CurrentTemperature 属性发生变化时，您都希望调用委托以通知订阅者（heater 和 cooler）温度的变化。为了实现这一目标，您必须修改 CurrentTemperature 属性以保存新值并向每个订阅者发布通知。代码修改出现在清单 13.4 中。

### LISTING 13.4: Invoking a Delegate without Checking for null

```
public class Thermostat
{
    ...
    public float CurrentTemperature
    {
        get { return _CurrentTemperature; }
        set
        {
            if (value != CurrentTemperature)
            {
                _CurrentTemperature = value;

                // INCOMPLETE: Check for null needed
                // Call subscribers
                OnTemperatureChange(value);
            }
        }
    }
    private float _CurrentTemperature;
}
```

现在对 CurrentTemperature 的赋值包含了一些特殊逻辑，用于通知订阅者 CurrentTemperature 的变化。通知所有订阅者的调用只是单个 C# 语句，OnTemperatureChange(value)。此单个语句将温度变化发布给 cooler 和 heater 对象。在这里，您在实践中看到，使用单个调用通知多个订阅者的能力正是委托更具体地被称为多播委托的原因。

## Check for null

清单 13.4 中缺少事件发布代码的一个重要部分。如果没有订阅者注册接收通知，OnTemperatureChange 将为 null，并且执行 OnTemperatureChange(value) 语句将抛出 NullReferenceException。为了避免这种情况，有必要在触发事件之前检查 null。清单 13.5 演示了如何使用 C# 6.0 的空条件运算符在调用 Invoke() 之前执行此操作。

```
public class Thermostat
{
    ...
    public float CurrentTemperature
    {
        get { return _CurrentTemperature; }
        set
        {
            if (value != CurrentTemperature)
            {
                _CurrentTemperature = value;
                // If there are any subscribers,
                // notify them of changes in temperature
                // by invoking said subscribers
                OnTemperatureChange?.Invoke(value);  // C# 6.0
            }
        }
    }
    private float _CurrentTemperature;
}
```

请注意在空条件之后对 Invoke() 方法的调用。虽然此方法可以使用仅点运算符调用，但这样做意义不大，因为这等同于直接调用委托（参见清单 13.4 中的 OnTemperatureChange(value)）。空条件运算符的根本优势在于特殊逻辑，可确保在检查 null 之后，不会出现订阅者取消订阅导致委托再次变为 null 的可能性。

不幸的是，在 C# 6.0 之前不存在这种特殊的不可中断的空检查逻辑。因此，在更早的 C# 版本中的实现要冗长得多，如清单 13.6 所示。

### LISTING 13.6: Invoking a Delegate with Null Check Prior to C# 6.0

```
public class Thermostat
{
    ...
    public float CurrentTemperature
    {
        get{return _CurrentTemperature;}
        set
        {
            if (value != CurrentTemperature)
            {
                _CurrentTemperature = value;
                // If there are any subscribers,
                // notify them of changes in temperature
                // by invoking said subscribers
                Action<float> localOnChange =
                    OnTemperatureChange;
                if(localOnChange != null)
                {
                    // Call subscribers
                    localOnChange(value);
                }
            }
        }
    }
    private float _CurrentTemperature;
}
```

而不是直接检查 null，此代码首先将 OnTemperatureChange 分配给第二个委托变量 localOnChange。此简单修改可确保如果在检查 null 和发送通知之间（由不同线程）删除了所有 OnTemperatureChange 订阅者，您不会引发 NullReferenceException。

本书其余部分的示例都将依赖 C# 6.0 的空条件运算符进行委托调用。

## Guidelines

- DO check that the value of a delegate is not null before invoking it.
- DO use the null conditional operator prior to calling Invoke() starting in C# 6.0.

## ADVANCED TOPIC

## -= Operator for a Delegate Returns a New Instance

鉴于委托是引用类型，分配一个局部变量然后使用该局部变量足以使空检查线程安全，这也许有些令人惊讶。由于 localOnChange 指向与 OnTemperatureChange 相同的位置，您可能会想象 OnTemperatureChange 的任何更改也会反映在 localOnChange 中。

情况并非如此，因为实际上，任何对 OnTemperatureChange -= <listener> 的调用都不会简单地从 OnTemperatureChange 中删除一个委托，使其包含的委托比之前少。相反，此类调用将分配一个全新的多播委托，而不会对 localOnChange 也指向的原始多播委托产生任何影响。

## ADVANCED TOPIC

## Thread-Safe Delegate Invocation

如果订阅者可以在不同线程上添加到委托并从中删除，那么明智的做法是（正如前面所述）在检查 null 之前将委托引用复制到局部变量。虽然这种方法可以防止调用 null 委托，但它并不能避免所有可能的竞争条件。例如，一个线程可以进行复制，然后另一个线程可以将委托重置为 null，然后原始线程可以调用委托的先前值，从而通知不再在订阅者列表中的订阅者。多线程程序中的订阅者应确保其代码在此场景下保持健壮；始终有可能“过时”的订阅者会被调用。

## Delegate Operators

为了将 Thermostat 示例中的两个订阅者组合在一起，您使用了 += 运算符。此运算符采用第一个委托并将第二个委托添加到链中。现在，在第一个委托的方法返回后，将调用第二个委托。要从委托链中删除委托，请使用 -= 运算符，如清单 13.7 所示。

