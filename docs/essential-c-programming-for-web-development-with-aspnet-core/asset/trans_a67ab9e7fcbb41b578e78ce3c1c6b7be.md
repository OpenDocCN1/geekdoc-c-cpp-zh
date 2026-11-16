

继承是面向对象编程（OOP）中的一种强大机制，它允许你基于现有类（基类或超类）创建新类（派生类或子类）。派生类继承基类的所有成员（字段、属性和方法），促进代码复用，并建立类之间的层次关系。

让我们扩展我们的 `Car` 示例：

```csharp
class ElectricCar : Car
{
    public int BatteryCapacity;

    public ElectricCar(string make, string model, int year, int batteryCapacity)
        : base(make, model, year)
    {
        BatteryCapacity = batteryCapacity;
    }

    public void ChargeBattery()
    {
        Console.WriteLine("Battery charging...");
    }
}
```

在这段代码中，我们创建了一个新类 `ElectricCar`，它继承自 `Car` 类。它添加了一个新字段 `BatteryCapacity` 和一个新方法 `ChargeBattery`，同时也继承了 `Car` 类的所有成员。

## 多态：多种形式，一个接口

多态是面向对象编程的基石，它允许将不同类的对象视为共同基类的对象。这使你能够编写可处理多种相关对象的代码，从而增强灵活性和适应性。

让我们看看多态的实际应用：

```csharp
Car myCar = new Car("Toyota", "Camry", 2023);
Car myElectricCar = new ElectricCar("Tesla", "Model 3", 2024, 75);
myCar.StartEngine(); // Output: Engine started!
myElectricCar.StartEngine(); // Output: Engine started!
// Polymorphism at play: Both cars can be started using the same method, even though they are of different types
```

本节我们踏上了一段探索 C# 中面向对象编程核心原则的旅程。我们探讨了类、对象、继承和多态，见证了它们如何使我们能够建模现实世界实体、促进代码复用并创建可适应的程序。掌握这些知识后，你现在已具备在 C# 开发中充分发挥面向对象编程潜力的能力，编写优雅且易于维护、经得起时间考验的代码。在下一节中，我们将深入探讨错误处理和异常管理的复杂性，确保你的程序能够优雅地处理意外情况，并向用户提供有信息量的反馈。在本节中，我们将深入探讨 C# 中的错误处理，探索异常、try-catch 块以及构建弹性应用程序的最佳实践。

### 异常：信号错误

异常是一个对象，表示程序执行期间发生的错误或意外事件。当异常被抛出时，程序的正常流程会被中断，控制权会转移到异常处理程序（如果存在）。C# 提供了丰富的内置异常类层次结构，每个类都旨在表示特定类型的错误。

一些常见的异常类包括：

- ArgumentException : 当向方法传递无效参数时抛出。
- DivideByZeroException : 当尝试除以零时抛出。
- FileNotFoundException : 当找不到文件时抛出。
- IndexOutOfRangeException : 当数组或列表索引超出范围时抛出。
- NullReferenceException : 当尝试访问 null 对象的成员时抛出。

### try-catch 块：捕获和处理异常

try-catch 块是 C# 中处理异常的主要工具。它允许你将可能抛出异常的代码块包含在 try 块中，并指定一个或多个 catch 块来处理不同类型的异常。

通用语法如下：

```csharp
try
{
    // Code that might throw an exception
}
catch (ExceptionType1 ex)
{
    // Code to handle ExceptionType1
}
catch (ExceptionType2 ex)
{
    // Code to handle ExceptionType2
}
// ... more catch blocks
finally
{
    // Code to execute regardless of whether an exception occurred
}
```

让我们通过一个示例来说明：

```csharp
try
{
    int result = 10 / 0; // This will throw a DivideByZeroException
}
catch (DivideByZeroException ex)
{
    Console.WriteLine("Error: Division by zero.");
}
finally
{
    Console.WriteLine("This code will always execute.");
}
```

在这段代码中，我们尝试除以零，这会触发 DivideByZeroException。catch 块捕获此特定异常并打印错误消息。finally 块是可选的，包含无论是否发生异常都将始终执行的代码。

### 异常处理的最佳实践

- **具体化**：尽可能捕获特定的异常类型，而不是使用通用的 `catch (Exception ex)` 块。这样可以提供更有针对性的错误处理，并避免无意中捕获你不打算处理的异常。
- **提供有信息量的错误消息**：包含清晰简洁的错误消息，向用户解释问题的性质。
- **记录异常**：考虑将异常记录到文件或数据库中，以便进一步分析和故障排除。
- **不要吞噬异常**：避免静默忽略异常，因为这可能导致隐藏的 bug 和意外行为。
- **谨慎使用 `finally` 块**：`finally` 块对于释放资源或执行无论是否发生异常都必须进行的清理操作非常有用。

本节我们探讨了 C# 中错误处理和异常管理的关键方面。我们了解了异常、try-catch 块以及构建弹性应用程序的最佳实践。通过将这些技术融入你的代码，你可以预见并优雅地处理意外情况，确保你的程序保持稳定，并向用户提供有信息量的反馈。凭借对错误处理的扎实理解，你现在已充分准备好应对现实世界软件开发的挑战，并创建能够经受生产环境考验的强大应用程序。在下一章中，我们将把重点转移到 ASP.NET Core 3 的 Web 开发精彩世界中，踏上构建动态交互式 Web 应用程序的旅程。

## 第 2 章：使用数据

### 数组、列表和集合

在编程领域，数据很少孤立存在。更多时候，我们需要处理相关信息的集合，例如学生列表、产品价格数组或员工记录字典。C# 提供了一套丰富的工具来管理此类集合，包括数组、列表和其他专用集合类型。在本节中，我们将深入探讨 C# 中的数据集合世界，了解它们的特性、优势和实际应用。

### 数组：固定大小的数据结构

数组是一种基本的数据结构，用于存储相同类型的固定大小、顺序的元素集合。它就像一排编号的盒子，每个盒子存放一个项目，并可以使用其索引（位置）进行访问。

### 声明和初始化数组

在 C# 中声明数组时，你需要指定元素类型，后跟方括号和数组名：

```csharp
int[] numbers;
```

这声明了一个名为 `numbers` 的数组，可用于存储整数值。要初始化数组，请使用 `new` 关键字并在方括号内指定大小：

```csharp
numbers = new int[5]; // Creates an array with 5 elements
```

