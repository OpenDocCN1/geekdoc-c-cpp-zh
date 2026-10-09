

// 如果使用 C# 2.0
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

图 14.3 展示了一个更新后的序列图。尽管 cooler 和 heater 都订阅了消息接收，但 lambda 表达式抛出的异常终止了调用链，并阻止了 cooler 对象接收到通知。

![](img/ef6a8a417630b222bfb3f3b949facff0_624_0.png)

## 图 14.3：带异常的委托调用序列图

为避免此问题，确保所有订阅者都能接收到通知（无论先前订阅者的行为如何），您必须手动遍历订阅者列表并单独调用它们。代码清单 14.10 展示了在 CurrentTemperature 属性中所需的更新。结果如输出 14.2 所示。

## 代码清单 14.10：处理来自订阅者的异常

```csharp
public class Thermostat
{
    // 定义事件发布者
    public Action<float> OnTemperatureChange;

    public float CurrentTemperature
    {
        get { return _CurrentTemperature; }
        set
        {
            if (value != CurrentTemperature)
            {
                _CurrentTemperature = value;
                Action<float> onTemperatureChange = OnTemperatureChange;
                if (onTemperatureChange != null)
                {
                    List<Exception> exceptionCollection =
                        new List<Exception>();
                    foreach (
                        Action<float> handler in
                        onTemperatureChange.GetInvocationList())
                    {
                        try
                        {
                            handler(value);
                        }
                        catch (Exception exception)
                        {
                            exceptionCollection.Add(exception);
                        }
                    }
                    if (exceptionCollection.Count > 0)
                    {
                        throw new AggregateException(
                            "There were exceptions thrown by "
                            + "OnTemperatureChange event subscribers.",
                            exceptionCollection);
                    }
                }
            }
        }
    }
    private float _CurrentTemperature;
}
```

## 输出 14.2

```
Enter temperature: 45
Heater: On
Error in the application
Cooler: Off
```

此代码清单演示了你可以从委托的 `GetInvocationList()` 方法中获取订阅者列表。枚举该列表中的每一项会返回各个独立的订阅者。如果你将每个订阅者的调用放在 try/catch 块中，就可以在继续枚举循环之前处理任何错误条件。在这个示例中，尽管委托订阅者抛出了异常，cooler 仍然接收到了温度变化的通知。在所有通知发送完毕后，代码清单 14.10 通过抛出 `AggregateException` 来报告任何异常，该异常封装了一个异常集合，可通过 `InnerExceptions` 属性访问。通过这种方式，所有异常仍然会被报告，同时所有订阅者也都得到了通知。

实际上，本示例中没有使用空条件运算符，因为大量代码依赖于非空委托。

## 方法返回值和引用传递

还有另一种场景，在这种情况下，遍历委托调用列表比直接激活通知更为有用。该场景与那些不返回 void 或具有 ref 或 out 参数的委托相关。在恒温器示例中，`OnTemperatureChange` 委托的类型是 `Action<float>`，它返回 void 且没有 out 或 ref 参数。因此，没有数据返回给发布者。这一考量很重要，因为委托的调用可能会触发向多个订阅者的通知。如果每个订阅者都返回一个值，那么使用哪个订阅者的返回值将是模棱两可的。

如果你将 `OnTemperatureChange` 更改为返回一个枚举值，以指示设备是否因温度变化而开启，那么新的委托类型将是 `Func<float, Status>`，其中 `Status` 是一个具有 On 和 Off 元素的枚举。所有订阅者方法都必须使用与委托相同的方法签名，因此，每个方法都需要返回一个状态值。此外，由于 `OnTemperatureChange` 可能对应一个委托链，有必要遵循你用于错误处理的相同模式。换句话说，你必须使用 `GetInvocationList()` 方法遍历每个委托调用列表，以获取每个独立的返回值。同样，使用 ref 和 out 参数的委托类型需要特别考虑。然而，尽管在特殊情况下可以使用这种方法，但准则是尽量避免这种场景，仅返回 void。

## 理解事件

到目前为止，本章中使用的委托存在两个关键问题。为克服这些问题，C# 使用了 event 关键字。在本节中，你将了解为什么要使用事件以及它们如何工作。

### 为什么要使用事件？

本章和前一章涵盖了你需要了解的所有关于委托工作原理的知识。不幸的是，委托结构的弱点可能会无意中允许程序员引入 bug。这些问题与封装有关，订阅或发布事件都无法充分控制这种封装。

### 封装订阅

如前所示，可以使用赋值运算符将一个委托赋值给另一个委托。不幸的是，这种能力引入了常见的 bug 来源。请考虑代码清单 14.11。

## 代码清单 14.11：使用赋值运算符 = 而不是 +=

```csharp
class Program
{
    public static void Main()
    {
        Thermostat thermostat = new Thermostat();
        Heater heater = new Heater(60);
        Cooler cooler = new Cooler(80);
        string temperature;

        // 注意：如果使用 C# 1.0，请使用 new Action (cooler.OnTemperatureChanged)
        thermostat.OnTemperatureChange =
            heater.OnTemperatureChanged;

        // Bug: 赋值运算符覆盖了
        // 之前的赋值
        thermostat.OnTemperatureChange =
            cooler.OnTemperatureChanged;

        Console.Write("Enter temperature: ");
        temperature = Console.ReadLine();
        thermostat.CurrentTemperature = int.Parse(temperature);
    }
}
```

代码清单 14.11 与代码清单 14.7 几乎相同，不同之处在于这里没有使用 += 运算符，而是使用了简单的赋值运算符。因此，当代码将 `cooler.OnTemperatureChanged` 赋值给 `OnTemperatureChange` 时，`heater.OnTemperatureChanged` 会被清除，因为一个新的完整调用链被分配以替换之前的调用链。当意图使用 += 赋值时，错误地使用赋值运算符的可能性极高，因此最好不支持对对象使用赋值运算符，除非在包含类内部。event 关键字提供了这种额外的封装，使你无法无意中取消其他订阅者。

### 封装发布

委托和事件之间的第二个重要区别是，事件确保只有包含类才能触发事件通知。请考虑代码清单 14.12。

## 代码清单 14.12：在事件容器外部触发事件

```csharp
class Program
{
    public static void Main()
    {
        Thermostat thermostat = new Thermostat();
        Heater heater = new Heater(60);
        Cooler cooler = new Cooler(80);
        string temperature;
        
        // 注意：如果使用 C# 1.0，请使用 new Action (cooler.OnTemperatureChanged)
        thermostat.OnTemperatureChange +=
            heater.OnTemperatureChanged;
        thermostat.OnTemperatureChange +=
            cooler.OnTemperatureChanged;
        thermostat.OnTemperatureChange(42);
    }
}
```

在代码清单 14.12 中，尽管 `thermostat` 的 `CurrentTemperature` 没有改变，`Program` 仍然可以调用 `OnTemperatureChange` 委托。因此，`Program` 向所有 `thermostat` 订阅者触发温度已变化的通知，尽管 `thermostat` 的温度并未发生变化。与之前一样，委托存在的问题

