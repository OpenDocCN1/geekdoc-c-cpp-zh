

# 464 第 10 章 类与对象：深入探讨

| 25 | Console.WriteLine({x} + {y} = {x + y}); |
| 26 | Console.WriteLine({x} - {y} = {x - y}); |
| 27 | Console.WriteLine({x} * {y} = {x * y}); |
| 28 | } |

输入复数 x 的实部: 2
输入复数 x 的虚部: 4
输入复数 y 的实部: 4
输入复数 y 的虚部: -2

```
(2 + 4i) + (4 - 2i) = (6 + 2i)
(2 + 4i) - (4 - 2i) = (-2 + 6i)
(2 + 4i) * (4 - 2i) = (16 + 12i)
```

> 图 10.15 | 复数的运算符重载。（部分 2，共 2 部分。）

在第 25–27 行，使用重载的运算符（在字符串插值表达式中）对 x 和 y 进行加减乘并输出结果。在第 25 行，我们对 ComplexNumber 操作数 x 和 y 使用 + 运算符。如果没有运算符重载，x+y 将是有意义的——编译器将知道如何相加两个 ComplexNumber 对象。此表达式在这里是有意义的，因为我们已经在图 10.14 的第 24–28 行中为 ComplexNumber 系统定义了 + 运算符。当在 10.15 的第 25 行将两个 ComplexNumbers“相加”时，这会调用运算符声明，并将左操作数作为第一个参数，右操作数作为第二个参数。当我们在第 26–27 行中使用减法和乘法运算符时，各自的重载运算符声明会被隐式调用。

每个计算结果都是由相应的重载运算符方法返回的新 ComplexNumber 对象。当此对象置于字符串插值表达式中，会隐式地调用它的 ToString 方法（图 10.14，第 20–21 行）。10.15 的第 25 行中的表达式 x+y 可以重写为显式调用结果 ComplexNumber 对象的 ToString 方法，如下：

```
(x + y).ToString()
```

## 10.14 时间类研究：扩展方法

你可以使用扩展方法为现有类型添加功能，而无需修改该类型。你在第 9.3 节中看到 LINQ 的功能是通过扩展方法实现的。图 10.16 使用扩展方法为类（第 10.5 节）添加了两个新方法：DisplayTime 和 AddHours。

```csharp
// 图 10.16: TimeExtensions.cs
// 演示扩展方法。
using System;
class TimeExtensions
{
```

> 图 10.16 | 演示扩展方法。（部分 1，共 2 部分。）

## 10.14 时间类研究：扩展方法

```csharp
static void Main()
{
    var myTime = new Time2(); // 调用 Time2 构造函数
    myTime.Set(11, 34, 15); // 设置时间为 11:34:15

    // 测试 DisplayTime 方法
    Console.Write("使用 DisplayTime 方法: ");
    myTime.DisplayTime();

    // 测试 AddHours 方法
    Console.Write("使用 AddHours 方法增加 5 小时: ");
    var timeAdded = myTime.AddHours(5); // 添加五个小时
    timeAdded.DisplayTime(); // 显示新的 Time2 对象

    // 在语句中添加小时并显示时间
    Console.Write("使用 AddHours 方法增加 15 小时: ");
    myTime.AddHours(15).DisplayTime(); // 添加小时并显示时间

    // 使用全限定方法名显示时间
    Console.Write("使用全限定方法名: ");
    TimeExtensions.DisplayTime(myTime);
}

// 扩展方法类
static class TimeExtensions
{
    // 在控制台中显示 Time2 对象
    public static void DisplayTime(this Time2 aTime)
    {
        Console.WriteLine(aTime.ToString());
    }

    // 向时间添加指定数量的小时数
    // 并返回一个新的 Time2 对象
    public static Time2 AddHours(this Time2 aTime, int hours)
    {
        // 创建一个新的 Time2 对象
        var newTime = new Time2()
        {
            Minute = aTime.Minute,
            Second = aTime.Second
        };
        // 给给定时间添加指定的小的小数
        newTime.Hour = (aTime.Hour + hours) % 24;

        return newTime; // 返回新的 Time2 对象
    }
}
```

| DisplayTime 方法: 11:34:15 AM |
| 使用 AddHours 方法增加 5 小时: 4:34:15 PM |
| 使用 AddHours 方法增加 15 小时: 23:34:15 AM |
| 使用全限定方法名: 11:34:15 AM |

> 图 10.16 | 演示扩展方法。（部分 2，共 2 部分。）

# 466 第 10 章 类与对象：深入探讨

### 扩展方法 DisplayTime

扩展方法 DisplayTime（第 35–38 行）在控制台中显示时间的字符串表示。`this` 关键字在方法头中指示该方法是针对 Time2 类的扩展方法。扩展方法必须定义在静态类中，例如 TimeExtensions（第 32–53 行）。如果你声明的扩展方法已经定义了签名兼容的实例方法，那么实例方法将覆盖（即隐藏）该扩展方法。

### 调用扩展方法 DisplayTime

第 45 行使用 myTime 调用 DisplayTime 扩展方法。注意，我们不需要为方法提供参数——编译器会隐式地传递对象作为方法的第一个参数。这允许你像调用实例方法一样调用 DisplayTime。在 IntelliSense 窗口中，扩展方法会通过特定的图标进行标识。图标中的向下箭头表示这是一个扩展方法。

### 扩展方法 AddHours

第 42–52 行声明了 AddHours 扩展方法。再次，第一个参数中的 `this` 关键字表明可以在 Time2 对象上调用。第二个参数是 int 类型，指定要添加的小时数。AddHours 方法返回一个添加了指定小时的新 Time2 对象。

第 45–46 行创建了新的 Time2 对象，并使用初始化器设置其 Minute 和 Second 属性为对应的值——当我们添加小时时，这些属性不会被修改。第 49 行将原始 Time2 对象的 Hour 属性加上第二个参数的小时，然后使用 % 运算符确保值在 0–23 的范围内。结果被赋值给 Time2 对象的 Hour 属性。第 51 行返回新的 Time2 对象给调用者。

### 调用扩展方法 AddHours

第 18 行调用 AddHours 扩展方法，为 myTime 对象增加五小时。注意该方法只指定了一个参数——要添加的小时数。再次，编译器隐式地传递调用方法的对象。

### 在单语句中调用多个扩展方法

第 23 行在单语句中使用两个扩展方法。同一语句中的多次方法调用被称为链式方法调用。当方法返回一个对象时，你可以在方法调用后跟随成员访问运算符。在第 23 行，DisplayTime 调用在 AddHours 返回的对象上。

### 使用全限定名调用扩展方法

第 27 行使用其全限定名调用 DisplayTime——即定义扩展方法的类名（TimeExtensions），随后是成员访问运算符（即方法名 (DisplayTime) 及其参数列表）。在第 27 行中，调用传递 Time2 作为参数。使用全限定名，你必须为扩展方法的第一个参数指定一个参数。

### 扩展方法的注意事项

如果你声明的扩展方法所在的类型已经定义了签名兼容的实例方法，那么实例方法将覆盖（即隐藏）该扩展方法。此外，如果预定义类型后来更新包含一个覆盖扩展方法的实例方法，编译器不会报告任何错误，且扩展方法也不会出现在 IntelliSense 中。

