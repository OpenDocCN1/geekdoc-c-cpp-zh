
图 3-8 所示的输出说明了值参数如何保持不变。它们在调用方法中保留其原始值。这是因为实际上对原始值创建了一个副本。当返回调用方法时，保留的原始值是可见的。

使用 `ref` 和 `out` 发送的参数在控制权返回调用方法时会发生变化。`out` 参数不需要在调用之前初始化；但该参数在方法返回之前必须被赋值。C# 不允许使用未初始化的变量。

![](img/45e6f245af31396d967c3186f19d331_191.png)

图 3-8 示例的参数输出

图 3-9 形象地说明了值传递和引用传递之间的区别。它还引起了 `out` 参数类型在调用之前不需要初始化。请注意，示例 3-18 中的程序语句用于此图。

## 参数类型

![](img/45e6f245af31396d967c3186f19d331_192.png)

图 3-9 引用传递与值传递

当你查看示例 3-18 时，注意方法头中的参数名称与 `Main()` 方法中使用的参数名称不同。这并没有产生问题。对于默认参数类型（值传递），你应该注意，如图 3-9 所示，`TestOut()` 方法中的 `aValue` 与 `Main()` 方法中的 `testValue` 引用的是不同的内存位置。

然而，如果使用 `ref` 和 `out` 关键字（引用传递），方法头中的参数和调用处的参数可以使用不同的标识符，但它们引用相同的内存位置。在这些情况下，为调用处的参数使用相同的标识符是恰当的。当你设计解决方案时，你可能希望为引用传递和值传递的参数使用相同的标识符。

在在之前的程序示例（示例 3-18）中，注意 `Console.WriteLine()` 方法的一个调用显示为注释。在 Visual Studio 中，有两个可用工具允许你通过点击来取消注释。这对于调试非常有用。图 3-10 中圈出的图标用于取消注释*工具提示*显示在右侧。

## 第 3 章 方法与行为

![](img/45e6f245af31396d967c3186f19d33193.png)

图 3-10 Visual Studio 注释图标

之前代码中的行被注释掉了以消除语法错误。在 `testValue` 有值之前无法显示内容。

本章介绍了大量材料。接下来的编程示例使用了大部分这些新概念。

## 命名和可选参数

随着 C# 的每个新版本引入了新功能。C# 4.0 包含了若干与方法相关的新功能。通过这些新功能，你可以在方法调用中命名参数。这可以增加方法调用的可读性，并允许你通过参数名称传递值，而无需担心调用方法时的确切顺序。你也可以为参数分配默认值，这样除非值与默认值不同，否则方法调用不需要传递值。虽然这些功能应该节制使用，但它们是语言的很好的补充，将在后续章节中讨论。

### 带默认值的可选参数

当你为参数分配默认值时，它就变成了可选参数。你不需要每次调用方法都传递值。相反，如果没有传递值，则使用默认值。一个方法可以关联多个可选参数。但是，如果有多个，它们必须放在参数列表的最后，位于任何必需参数之后。示例 3-19 展示了带默认值的可选参数。

#### 示例 3-19

```c
public static void DoSomething(string name, int age = 21, bool
    currentStudent = true,
    string major = "CS")
{
    // 此处编写额外的程序语句
}
```

现在你可以调用 `DoSomething()` 并传递默认值的参数，或者将默认值分配给参数。示例 3-20 显示了 `DoSomething()` 方法的有效调用。

#### 示例 3-20

```c
DoSomething ("Elizabeth Abbott", 20);
DoSomething ("James Gabriel");
DoSomething("Jonathan Byle", 25, false, "MS");
```

默认值必须是常量。如果未为特定参数发送参数，则使用默认值。如果为特定参数发送了一个参数，则使用默认值。如果为特定参数发送了一个参数，则使用默认值。

### 命名参数

命名参数让你不再需要查找参数的顺序。每个参数的参数可以使用其名称后跟冒号（:）以及值来指定。示例 3-21 展示了对 `DoSomething()` 的调用。

#### 示例 3-21

```c
DoSomething(name: "Robert Wiser", age: 20);
DoSomething(name: "Paul Nelson", major: "BIO");
DoSomething(name: "Fred Terrell", age: 25, major: "MS");
```

可选参数已经是 Visual Basic 的一部分了。随着 C# 4.0 的引入，开发者现在可以使用此功能，并能够使用命名参数。

可选参数让你能够省略方法调用中的，而命名参数允许你通过名称而不是位置指定参数。

![](img/45e6f245af31396d967c3186f19d33194.png)

## 编程示例：JGINGDISTANCE

本示例演示了程序中使用方法。问题规格如图 3-11 所示。

![](img/45e6f245af31396d967c3186f19d33195.png)

图 3-11 RunningDistance 问题规格

### 分析问题

你应该查看图 3-11 中的问题规格，并确保理解问题定义。某些值必须作为字符串变量输入，然后解析为数值字段，以便进行算术运算。

### 表 3-3 RunningDistance 类变量

| 数据项 | 类型 | 标识符 |
|---|---|---|
| 第一分钟的步数 | int | initialStride |
| 最后分钟的步数 | int | finalStrideCount |
| 跑步时间 | int | hrs, mins, totalMinutes |
| 每分钟平均步数 | double | numberOfStepsPerMin |
| 总距离 | double | distanceTraveled |

**常量** 步（每步英尺）被设置为常量值。标识符和预设常量值将为

```c
STRIDE = 2.5;
```

每英里的英尺也被设置为常量。
`FEET_PER_MILE = 5280;`

### 设计解决方案

目标输出是显示给定跑步期间的距离（以英里计算）。图 3-12 显示了预期输出的原型。xxx.xx 被放在原型中，表示计算出的值出现的位置。

## 第 3 章 方法与行为

![](img/45e6f245af31396d967c3186f196d331_197_0.png)

图 3-12 原型

面向对象的方法更关注对象。类图用于帮助设计和记录这些特征。图 3-13 显示了 JoggingDistance 示例类图。

```
JoggingDistance
-initialStrideCount : int
-finalStrideCount : int
-mins : int
-totalMinutes : int
-numberOfStepsPerMin : double
-distanceTraveled : double
+DisplayInstructions()
+SetStride(when string) : int
+InputTime(time out int, out mins) : void
+CalculateAvgSteps(initialStrideCount : int, finalStrideCount : int) : double
+CalculateDistance(numberOfStepsPerMin : double, totalMinutes : int) : double
+DisplayResults(numberOfStepsPerMin : double, mins : int, in distanceTraveled : double) : void
```

图 3-13 类图

在设计过程中，开发显示解决问题逐步步骤的算法非常重要。结构化英语（也称为伪代码）适用于面向对象的方法论。除了 `Main()` 方法外，还需要设计七个额外的方法。图 3-14 显示了 JoggingDistance 示例的结构化英语设计。

### 编程示例：JoggingDistance

```
Main() {
    DisplayInstructions()
    set initialStrideCount = GetNumberStrides("first")
    set finalStrideCount = GetNumberStrides("last")
    InputJoggingTime(hrs, mins)
    set totalMinutes = CalculateTime(hrs, mins)
    set numberOfStepsPerMin = {
        CalculateAvg(initialStrideCount, finalStrideCount)
        set distanceTraveled =
            CalculateDistance(numberOfStepsPerMin, totalMinutes)
    }
    DisplayResults()
}
```

```
DisplayInstructions() {
    Write message indicating what program will be
    Write message alerting to user what values will be entered
}
```

```
int GetNumberStrides(string when) {
    Write prompt to enter numberOfSteps using when argument
    Read numberOfSteps into string inValue
    numberOfSteps = parse(inValue)
    return numberOfSteps
}
```

```
InputJoggingTime(int hrs, int mins) {
    Write prompt to enter hrs
    Read hrs into string inValue
    hrs = parse(inValue)
    Write prompt to enter mins
    Read mins into string inValue
    mins = parse(inValue)
}
```

```
double CalculateAvgSteps(int initialStrideCnt, int finalStrideCnt) {
    return (initialStrideCnt + finalStrideCnt) / 2.0
}
```

```
int CalculateTime(int hrs, int mins) {
    return hrs * 60
}
```

```
double CalculateDistance(double numberOfStepsPerMin, int totalMinutes) {
    return numberOfStepsPerMin * 2.5 * totalMinutes / 5280
}
```

```
DisplayResults() {
    Write averageStride
    Write JoggingTime
    Write distanceTraveled
}
```

图 3-14 JoggingDistance 示例的结构化英语

这些方法说明了 `void`（空）操作和返回值的操作。注意 `DisplayInstructions()`、`InputJoggingTime()` 和 `DisplayResults()` 都是非返回值方法。当你实现解决方案时，关键字 `void` 出现在它们的标题中。这些方法的体内部没有出现 `return` 语句。当方法的语句执行完毕，控制权返回调用这些方法的 `Main()`。

其他方法（`GetNumberStrides()`、`CalculateTime()`、`CalculateAvg()`、`CalculateDistance()`）都将值返回给 `Main()`。不是在方法名处使用 `void`，而是数据类型出现在方法名之前。该数据类型描述了方法结束时将返回的内容。这四个方法的最后一行都需要一个 `return` 语句。

此外注意某些方法带有参数。`JoggingTime()` 方法有两个特殊参数。方法只能返回一个值。另一个选项是使用 `out` 类型，这本质上是让 `hrs` 和 `mins` 返回给 `Main()`。在算法开发后，应该检查设计的正确性。当你遇到方法调用时，在 `Main()` 中保留你的位置。在被调用方法中执行语句。当被调用方法执行完成后，返回到保存的位置。

使用以下数据测试你的算法：
- 第 1 分钟：185
- 最后一分钟：120
- 跑步时间：12

## 解决方案

在你完成设计并验证算法的正确性后，将设计翻译成代码。最终应用程序列表如下：

- `JoggingDistance.cs`
- 作者：Doyle
- 该应用程序计算距离。用户被要求输入第一分钟和最后一分钟的步以及以及跑步时间。使用 2.5 的步长进行计算。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace JoggingDistance
{
class JoggingDistance
{
    static void Main(string[] args)
    {
        int initialStrideCount,
        finalStrideCount,
        hrs,
        mins,
        totalMinutes;
        double numberOfStepsPerMin,
        distanceTraveled;
        DisplayInstructions();
        initialStrideCount = GetNumberStrides("first");
        finalStrideCount = GetNumberStrides("last");
        InputJoggingTime(out hrs, out mins);
        totalMinutes = CalculateTime(hrs, mins);
        numberOfStepsPerMin = CalculateAvgSteps(initialStrideCount, finalStrideCount);
        distanceTraveled = CalculateDistance(numberOfStepsPerMin, totalMinutes);
        DisplayResults(numberOfStepsPerMin, mins, distanceTraveled);
        Console.ReadKey();
    }
    public static void DisplayInstructions()
    {
        Console.WriteLine("How many miles did you jog?");
        Console.WriteLine("Distance (in miles) will be calculated");
        Console.WriteLine("based on stride and number of steps per minute.");
        Console.WriteLine("You will be asked to enter the");
        Console.WriteLine("initial and ending strides...");
        Console.WriteLine("OR how many steps you took the");
        Console.WriteLine("first minute and how many");
        Console.WriteLine("steps during the last minute.");
        Console.WriteLine("Average stride is calculated from");
        Console.WriteLine("those entries.");
        Console.WriteLine("Calculations are based on a");
    }
    static int GetNumberStrides(string when)
    {
        Console.Write("Enter number of steps for " + when + ": ");
        string inValue = Console.ReadLine();
        int numberOfSteps = int.Parse(inValue);
        return numberOfSteps;
    }
    public static void InputJoggingTime(out int hrs, out int mins)
    {
```
