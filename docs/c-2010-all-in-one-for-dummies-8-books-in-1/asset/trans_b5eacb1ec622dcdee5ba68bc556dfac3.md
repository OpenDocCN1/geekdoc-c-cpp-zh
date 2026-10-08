

# 定义 const 和只读数据成员 225

```csharp
public class Car
{
  public static int numberOfCars; // 构建的汽车数量
  public string licensePlate; // 牌牌 ID
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_250_0.png)

静态成员不是通过对象访问的。相反，你通过类名本身来访问它们，如下代码所示：

```csharp
// 创建 Car 类的一个新对象。
Car newCar = new Car();
newCar.licensePlate = "ABC123";
// 增加汽车计数以反映新汽车。
newCar.numberOfCars++;
```

对象 `newCar.licensePlate`是通过对象 `newCar` 访问的，而（静态）成员 `Car.numberOfCars`是通过类 `Car` 访问的。所有汽车共享同一个 `numberOfCars`，因此每辆汽车的值与其他所有汽车完全相同。

第二卷
第 2 章

类成员是静态成员。非静态成员特定于“实例”（每个单独的对象），并且是实例成员。你使用的斜体短语是指代这类成员的通用方式。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_250_1.png)

显示某些类成员

# 定义 const 和只读数据成员

静态成员的一种特殊类型是 `const` 数据成员，它代表一个常量。你必须在声明中建立 `const` 变量的值，并且不能在程序的任何地方更改它，如下：

```csharp
class Program
{
  // 一年的天数（包括闰日）
  public const int daysInYear = 366; // 必须有初始化器。
  public static void main(string[] args)
  {
    // 这是一个数组，在本章稍后介绍。
    int[] maxTemperatures = new int[daysInYear];
    for (int index = 0; index < daysInYear; index++)
    {
      // ...累积每年的
      // 最高温度 ...
    }
  }
}
```

你可以在程序中使用常量 `daysInYear` 来替代值 `366`。`const` 变量非常有用，因为它可以将神秘的数字（如 `366`）替换为描述性名称 `daysInYear`，以增强程序的可读性。

# 226 定义 const 和只读数据成员

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_251_0.png)

C# 提供了另一种声明常量的方法——你可以在变量声明前加上 `readonly` 修饰符，如下：

```csharp
public readonly int daysInYear = 366; // 这也可以是静态的。
```

与 `const` 一样，在分配初始值后，它就无法更改。虽然原因对于本书来说太技术性，但使用 `readonly` 方法声明常量比 `const` 更好。

你可以将 `const` 用于类数据成员，就像你在本章中和类方法内部看到的那些。但在方法内部不允许使用 `readonly`。本微型书籍的第 3 章将深入探讨方法。

常量命名还有另一种惯例。许多程序员倾向于像命名变量那样（如 `daysInYear`）命名它们，而是使用下划线分隔的大字母，例如 `DAYS_IN_YEAR`。这种惯例将常量与普通的读写变量区分开来。

# 第 3 章：我们有了方法

# 本章内容

- 定义方法
- 向方法传递参数
- 获取返回结果
- 回顾 `WriteLine()` 方法

程序需要将大型程序拆分成易于处理的小块。例如，本微型书籍之前章节中包含的程序达到了一个人一次能消化的编程信息的极限。

C# 允许你将类代码分成称为“方法”（methods）的块。设计和实现良好的方法可以极大简化编写复杂程序的工作。

方法等同于其他语言中的函数、过程或子程序。区别在于，方法始终是类的一部分。

# 定义和使用方法

考虑以下示例：

```csharp
class Example
{
    public int anInt; // 实例
    public static int staticInt; // 静态
    public void InstanceMethod() // 实例
    {
        Console.WriteLine("this is an instance");
    }
    public static void ClassMethod() // 静态
    {
        Console.WriteLine("this is a class method");
    }
}
```

元素 `anInt` 是数据成员，就像第一卷中所示的。然而，元素 `InstanceMethod()` 是新的。`InstanceMethod()` 被称为实例方法（废话！），它是一组你可以通过引用方法名来执行的 C# 语句。这个概念 ![](img/36596fb11aa4233d5cab0d6ddd1d82e8_252_0.png)

# 228 定义和使用方法

通过示例解释得最清楚——尽管 `Main()` 和 `WriteLine()` 在此书几乎每个示例中都被使用，而且它们都是方法。注意：静态方法和非静态方法之间的区别很重要。我在本章中涵盖了部分内容，并在本微型书籍的第 4 章继续详细介绍，重点关注非静态（或实例）方法。要调用实例方法，你需要该类的实例。要调用静态方法，你可以调用类名，而不是实例。以下代码段显示了如何访问数据成员 `anInt` 以及类方法或静态方法 `staticInt`：![](img/36596fb11aa4233d5cab0d6ddd1d82e8_253_0.png)

```csharp
Example example = new Example(); // 创建一个实例。
example.anInt = 1; // 通过实例初始化实例成员。
example.staticInt = 2; // 通过类初始化类方法。
```

以下代码段以几乎相同的方式定义并访问 `InstanceMethod()` 和 `ClassMethod()`：

```csharp
Example example = new Example(); // 创建一个实例。
example.InstanceMethod(); // 调用实例方法。
ClassMethod(); // 通过类调用方法。

以下几行无法编译：
example.ClassMethod(); // 无法通过实例访问类方法。
example.InstanceMethod(); // 无法通过类访问实例方法。
```

类的每个实例都有自己的实例方法副本。但同一类的所有实例具有相同的类成员——包括数据成员和方法——以及它们的值![](img/36596fb11aa4233d5cab0d6ddd1d82e8_253_1.png)

`InstanceMethod()` 将控制权传递给 `ClassMethod()`。执行最后所示的代码生成输出：

```
this is an instance
this is a class method
```

在方法完成后，控制权返回到调用处。通过阅读 C# 代码的注释，你应该能够对程序的意图有一个良好的理解。如果不能，说明你注释得不当。相反，如果你无法剥离注释并通过方法和变量名来理解意图，说明你的方法命名不够清晰，或者方法分得不够小（或者两者兼有）。

# TIP

在描述方法时我会加上括号——例如 `InstanceMethod()`，以便它们更容易识别。否则，你可能会在理解我在说什么时感到困惑。

# 一个供你的方法示例

在本节中，我将第一卷第 5 章的 `CalculateInterestTable` 拆分为几个合理的方法；演示了正确的定义定义如何有助于编写和理解程序。

# REMEMBER

我将在章的后续章节详细解释方法定义和调用的细节。这个示例仅提供了一个概述。

