

actor : actor
1: Main()
2: Thermostat()
Thermostat() : Thermostat
3: Heater(temperature) ----------------------> heater : Heater
4: Cooler(temperature) ----------------------> cooler : Cooler
OnTemperatureChange-delegate-TemperatureChangeHandler
5: operator+=
6: operator+=
Console
7: Write("Enter temperature:") --------------->
8: ReadLine() -------------------------------->
9: CurrentTemperature(value)
10: OnTemperatureChange(value)
11: OnTemperatureChanged(newTemperature)
12: WriteLine("Heater off") -------------------->
13: OnTemperatureChanged(newTemperature)
14: WriteLine("Cooler on") -------------------->

图 13.1：委托调用序列图

## 多播委托内部

要了解事件的工作原理，需要重新审视 System.Delegate 类型内部的初步检查。请记住，delegate 关键字是派生自 System.MulticastDelegate 的类型的别名。同样，System.MulticastDelegate 派生自 System.Delegate，而 System.Delegate 由一个对象引用和一个方法指针（类型为 System.Reflection.MethodInfo）组成。当你创建委托时，编译器会自动使用 System.MulticastDelegate 类型，而不是 System.Delegate 类型。MulticastDelegate 类包含一个对象引用和一个方法指针，与其 Delegate 基类一样，但它还包含对另一个 System.MulticastDelegate 对象的引用。

当你向多播委托添加方法时，MulticastDelegate 类会创建委托类型的新实例，将添加方法的对象引用和方法指针存储到新实例中，并将新委托实例作为委托实例列表中的下一项添加进去。实际上，MulticastDelegate 类维护了一个 Delegate 对象的链表。从概念上讲，你可以像图 13.2 所示那样表示恒温器示例。

![](img/ef1bd88b5fdf5fb56f8510479607fe66_566_0.png)

图 13.2：链在一起的多播委托

调用多播委托时，链表中的每个委托实例会被依次调用。通常，委托会按照添加顺序调用，但此行为未在 CLI 规范中指定，而且还可以被重写。因此，程序员不应依赖调用顺序。

## 错误处理

错误处理使得对顺序通知的认识变得至关重要。如果某个订阅者抛出异常，链中后续的订阅者将不会收到通知。例如，考虑如果你修改了 Heater 的 OnTemperatureChanged() 方法，使其抛出异常，会发生什么情况，如清单 13.8 所示。

### 清单 13.8: OnTemperatureChanged() 抛出异常

```
class Program
{
    public static void Main()
    {
        Thermostat thermostat = new Thermostat();
        Heater heater = new Heater(60);
        Cooler cooler = new Cooler(80);
        string temperature;

        // Using C# 2.0 or Later syntax.
        // thermostat.OnTemperatureChange +=
        //     heater.OnTemperatureChanged;

        // Using C# 3.0. Change to anonymous method
        // if using C# 2.0.
        // thermostat.OnTemperatureChange +=
        (newTemperature) =>
        {
            throw new ApplicationException();
        };

        thermostat.OnTemperatureChange +=
            cooler.OnTemperatureChanged;

        Console.Write("Enter temperature: ");
        temperature = Console.ReadLine();
        thermostat.CurrentTemperature = int.Parse(temperature);
    }
}
```

图 13.3 显示了更新后的序列图。

![](img/ef1bd88b5fdf5fb56f8510479607fe66_568_0.png)

图 13.3：带异常的委托调用序列图

尽管 cooler 和 heater 都订阅了消息，但 lambda 表达式异常会终止链条，并阻止 cooler 对象接收通知。

为了避免这个问题，使所有订阅者都能接收通知，无论早期订阅者的行为如何，你都必须手动遍历订阅者列表并逐个调用它们。清单 13.9 显示了 CurrentTemperature 属性所需的更新。结果显示在输出 13.2 中。

### 清单 13.9: 处理来自订阅者的异常

```
public class Thermostat
{
    // Define the delegate data type
    public delegate void TemperatureChangeHandler(
        float newTemperature);

    // Define the event publisher
    public event TemperatureChangeHandler OnTemperatureChange;

    public float CurrentTemperature
    {
        get
        {
            return _CurrentTemperature;
        }
        set
        {
            if (value != CurrentTemperature)
            {
                _CurrentTemperature = value;
                if (OnTemperatureChange != null)
                {
                    foreach (
                        TemperatureChangeHandler handler in
                        OnTemperatureChange.GetInvocationList())
                    {
                        try
                        {
                            handler(value);
                        }
                        catch (Exception exception)
                        {
                            Console.WriteLine(exception.Message);
                        }
                    }
                }
            }
        }
    }
    private float _CurrentTemperature;
}
```

输出 13.2:
```
Enter temperature: 45
Heater: On
Error in the application
Cooler: Off
```

此清单演示了你可以从委托的 GetInvocationList() 方法中检索订阅者列表。遍历此列表中的每个项会返回各个订阅者。如果你随后将每个订阅者的调用放在 try/catch 块中，则可以在继续枚举循环之前处理任何错误条件。在此示例中，即使委托侦听器抛出异常，cooler 仍会接收温度变化的通知。

## 方法返回值和按引用传递

还有另一种场景，遍历委托调用列表比直接激活通知更有用。此场景涉及不返回 void 或带有 ref 或 out 参数的委托。在迄今为止的恒温器示例中，OnTemperatureChangeHandler 委托的返回类型为 void。此外，它不包含任何 ref 或 out 类型参数，即向调用方返回数据的参数。这一点很重要，因为委托调用可能会触发向多个订阅者发送通知。如果订阅者返回一个值，则不明确将使用哪个订阅者的返回值。

如果你将 OnTemperatureChangeHandler 更改为返回一个枚举值，指示设备是否因温度变化而开启，则新委托将如清单 13.10 所示。

### 清单 13.10: 声明带有方法返回值的委托

```
public enum Status
{
    On,
    Off
}

// Define the delegate data type
public delegate Status TemperatureChangeHandler(
    float newTemperature);
```

所有订阅者方法都必须使用与委托相同的方法签名，因此每个方法都需要返回一个状态值。假设你以类似之前的方式调用委托，例如，在清单 13.11 中 status 的值会是什么？

### 清单 13.11: 调用带有返回值的委托实例

```
Status status = OnTemperatureChange(value);
```

由于 OnTemperatureChange 可能对应于一个委托链，status 仅反映最后一个委托的值。所有其他值都将完全丢失。

为了解决这个问题，有必要遵循与错误处理中使用的相同模式。换句话说，你必须使用 GetInvocationList() 方法遍历每个委托调用列表，以检索每个单独的返回值。同样，使用 ref 和 out 参数的委托类型需要特别考虑。

## 事件

在本章中，你迄今使用的委托存在两个关键问题。为了解决这些问题，C# 使用 event 关键字。在本节中，你将了解为何要使用事件以及它们的工作原理。

### 为何使用事件？

本章和前一章涵盖了你了解委托工作原理所需的所有内容。但是，委托结构中的弱点可能会无意中允许程序员引入错误。这些问题与封装有关，事件的订阅和发布都无法充分控制封装。

### 封装订阅

如前所示，可以使用赋值运算符将一个委托赋值给另一个委托。不幸的是，此功能引入了错误的常见来源。考虑清单 13.12。

### 清单 13.12: 使用赋值运算符 = 而非 +=

```
class Program
{
    public static void Main()
    {
        Thermostat thermostat = new Thermostat();
        Heater heater = new Heater(60);
        Cooler cooler = new Cooler(80);
        string temperature;

        // Note: Use new Thermostat.TemperatureChangeHandler(
        //     cooler.OnTemperatureChanged) if C# 1.0
        thermostat.OnTemperatureChange =
            heater.OnTemperatureChanged;

        // Bug: assignment operator overrides
        // previous assignment.
        thermostat.OnTemperatureChange =
            cooler.OnTemperatureChanged;
    }
}
```

