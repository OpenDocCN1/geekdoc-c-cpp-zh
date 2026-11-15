
## 摘要

本章首先讨论了委托及其作为方法或回调引用的用法。它介绍了一个强大的概念，用于传递一组指令以在不同位置调用，而不是在编码指令时立即调用。

紧接着简要介绍了 C# 2.0 的匿名方法概念后，本章引入了 C# 3.0 的 Lambda 表达式概念，这是一种取代（但并未消除） C# 2.0 匿名方法语法的语法。无论语法如何，这些构造允许程序员直接将一组指令分配给变量，而无需定义包含指令的显式方法。这为在方法中动态编程指令提供了很大的灵活性——这是一个强大的概念，通过称为 LINQ（Language Integrated Query，语言集成查询）的 API 大大简化了集合的编程。

最后，本章以表达式树的概念结束，以及它们如何编译成表示 Lambda 表达式的数据，而不是委托实现本身。这是一个关键特性，使 LINQ to SQL 和 LINQ to XML 等库成为可能，这些库解释表达式树并在 CIL 以外的上下文中使用它。

Lambda 表达式一词涵盖了语句 Lambda 和表达式 Lambda。换句话说，语句 Lambda 和表达式 Lambda 都是 Lambda 表达式的类型。

本章提到但未详细阐述的一件事是多播委托。下一章将详细探讨多播委托，并解释它们如何通过事件实现发布-订阅模式。

## 13 事件

在前一章中，你学习了如何将单个方法存储在委托类型的实例中，并通过委托调用该方法。委托是称为发布-订阅的更大模式的构建块。委托的使用及其对发布-订阅模式的支持是本章的重点。本章中描述的几乎所有内容都可以仅使用委托来完成。但是，本章重点介绍的事件构造提供了额外的封装，使发布-订阅模式更容易实现且不易出错。

![](img/ef1bd88b5fdf5fb56f8510479607fe66_555_0.png)

在前一章中，所有委托都用于单个回调（多重性为一）。但是，单个委托变量可以引用一系列委托，其中每个后续委托以链的形式指向下一个委托，有时称为多播委托。使用多播委托，你可以通过单个方法对象调用方法链，创建引用方法链的变量，并将委托作为参数传递以传递方法。

C# 中多播委托的实现是一种常见模式，否则需要大量手动代码。这种模式称为观察者或发布-订阅模式，它表示将单个事件（例如对象状态更改）的通知广播到多个订阅者的场景。

### 使用多播委托编写观察者模式

考虑一个温度控制示例，其中加热器和冷却器连接到同一个恒温器。为了使设备适当开启和关闭，你会通知设备温度变化。一个恒温器将温度变化发布到多个订阅者——加热和冷却设备。下一节将探讨代码。1

### 定义订阅者方法

首先定义 Heater 和 Cooler 对象（参见清单 13.1）。

### 清单 13.1: Heater 和 Cooler 事件订阅者实现

```csharp
class Cooler
{
    public Cooler(float temperature)
    {
        Temperature = temperature;
    }

    public float Temperature
    {
        get { return _Temperature; }
        set { _Temperature = value; }
    }

    private float _Temperature;

    public void OnTemperatureChanged(float newTemperature)
    {
        if (newTemperature > Temperature)
        {
            System.Console.WriteLine("Cooler: On");
        }
        else
        {
            System.Console.WriteLine("Cooler: Off");
        }
    }
}

class Heater
{
    public Heater(float temperature)
    {
        Temperature = temperature;
    }

    public float Temperature
    {
        get { return _temperature; }
        set { Temperature = value; }
    }

    private float _Temperature;

    public void OnTemperatureChanged(float newTemperature)
    {
        if (newTemperature < Temperature)
        {
            System.Console.WriteLine("Heater: On");
        }
        else
        {
            System.Console.WriteLine("Heater: Off");
        }
    }
}
```

1. 在此示例中，我使用恒温器一词，因为人们更常在供暖和制冷系统的语境下思考它。然而，从技术上讲，温度计会更合适。

这两个类基本相同，除了温度比较之外。（事实上，如果你在 OnTemperatureChanged 方法中使用委托作为比较的方法指针，可以消除其中一个类。）每个类存储开启设备的温度。此外，两个类都提供 OnTemperatureChanged() 方法。调用 OnTemperatureChanged() 方法是向 Heater 和 Cooler 类指示温度已更改的方式。方法实现使用 newTemperature 与存储的触发温度进行比较，以确定是否开启设备。

OnTemperatureChanged() 方法是订阅者方法。重要的是，它们的参数和返回类型必须与 Thermostat 类中的委托匹配，我将在下一节讨论。

### 定义发布者

Thermostat 类负责将温度变化报告给加热器和冷却器对象实例。Thermostat 类代码出现在清单 13.2 中。

### 清单 13.2: 定义事件发布者 Thermostat

```csharp
public class Thermostat
{
    // Define the delegate data type
    public delegate void TemperatureChangeHandler(
        float newTemperature);

    // Define the event publisher
    public TemperatureChangeHandler OnTemperatureChange
    {
        get { return _OnTemperatureChange; }
        set { _OnTemperatureChange = value; }
    }

    private TemperatureChangeHandler _OnTemperatureChange;

    public float CurrentTemperature
    {
        get { return _CurrentTemperature; }
        set
        {
            if (value != CurrentTemperature)
            {
                _CurrentTemperature = value;
            }
        }
    }

    private float _CurrentTemperature;
}
```

Thermostat 类的第一个成员是 TemperatureChangeHandler 委托。虽然不是必须的，但 Thermostat.TemperatureChangeHandler 是一个嵌套委托，因为其定义特定于 Thermostat 类。该委托定义了订阅者方法的签名。因此，请注意，在 Heater 和 Cooler 类中，OnTemperatureChanged() 方法都与 TemperatureChangeHandler 的签名匹配。

除了定义委托类型外，Thermostat 还包含一个名为 OnTemperatureChange 的属性，其类型为 OnTemperatureChangeHandler 委托。OnTemperatureChange 存储订阅者列表。请注意，只需要一个委托字段来存储所有订阅者。换句话说，Cooler 和 Heater 类都将从此单个发布者接收温度变化通知。

Thermostat 的最后一个成员是 CurrentTemperature 属性。它设置和获取 Thermostat 类报告的当前温度值。

### 连接发布者和订阅者

最后，将所有这些部分放在 Main() 方法中组合在一起。清单 13.3 显示了 Main() 可能的示例。

### 清单 13.3: 连接发布者和订阅者

```csharp
class Program
{
    public static void Main()
    {
        Thermostat thermostat = new Thermostat();
        Heater heater = new Heater(60);
        Cooler cooler = new Cooler(80);

        string temperature;

        // Using C# 2.0 or later syntax.
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
