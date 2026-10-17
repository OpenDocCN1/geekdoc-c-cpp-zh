
## 第 3 章：程序控制语句 115

## 嵌套循环

正如你在前面的示例中所看到的，一个循环可以嵌套在另一个循环内部。嵌套循环用于解决各种编程问题，是编程中不可或缺的一部分。因此，在结束 C# 循环语句主题之前，让我们来看另一个嵌套循环示例。以下程序使用嵌套的 `for` 循环来寻找 2 到 100 之间数字的因数：

```
// 使用嵌套循环寻找 2 到 100 之间数的因数。
using System;
class FindFac {
    static void Main() {
        for(int i=2; i <= 100; i++) {
            Console.Write("Factors of " + i + ": ");
            for(int j = 2; j <= i/2; j++) {
                if ((i%j) == 0) Console.Write(j + " ");
            }
            Console.WriteLine();
        }
    }
}
```

以下是该程序生成的输出：

- 2 的因数：
- 3 的因数：
- 4 的因数：2
- 5 的因数：
- 6 的因数：2 3
- 7 的因数：
- 8 的因数：2 4
- 9 的因数：3
- 10 的因数：2 5
- 11 的因数：
- 12 的因数：2 3 4 6
- 13 的因数：
- 14 的因数：2 7
- 15 的因数：3 5
- 16 的因数：2 4 8
- 17 的因数：
- 18 的因数：2 3 6 9
- 19 的因数：
- 20 的因数：2 4 5 10

在程序中，外层循环 `i` 从 2 运行到 100。内层循环连续测试从 2 到 `i` 的数字，打印出能整除 `i` 的数字。

## 第 3 章自测

- 1. 写一个程序，从键盘读取字符直到接收到句号。让程序统计空格的数量。在程序结束时报告总数。
- 2. 在 `switch` 中，从一个 `case` 的代码序列可以执行到下一个吗？
- 3. 显示 `if-else-if` 阶梯的通用形式。
- 4. 给定

```
if(x < 10)
  if(y > 100) {
    if(!done) x = z;
    else y = z;
  }
else Console.WriteLine("error");
```

最后的 `else` 与哪个 `if` 关联？
- 5. 显示一个从 1000 计数到 0 的循环 `for` 语句。
- 6. 下面片段有效吗？

```
for(int i = 0; i < num; i++)
  sum += i;
count = i;
```
- 7. 解释 `break` 的作用。
- 8. 在以下片段中，执行 `break` 语句后，会显示什么？

```
for(int i = 0; i < 10; i++)
  while(running) {
    if(x<y) break;
    //...
  }
  Console.WriteLine("after while");
Console.WriteLine("After for");
```
- 9. 下面片段打印什么？

```
for(int i = 0; i<10; i++)
  Console.Write(i + " ");
  if((i%2) == 0) continue;
  Console.WriteLine();
```
- 10. `for` 循环中的迭代表达式并不总是按固定量改变循环控制变量。相反，循环控制变量可以以任何任意方式改变。使用这个概念，写一个程序，使用 `for` 循环生成并显示 1, 2, 4, 8, 16, 32 等递增。
- 11. ASCII 小写字母与大写字母之间相差 32。因此，要将小写字母转换为大写字母，需对其减去 32。利用这一信息写一个程序，从键盘读取字符。让它将所有小写字母转换为大写，所有大写字母转换为小写，并显示结果。对任何其他字符不做修改。当用户按下句号键时程序停止。在最后，让程序显示发生的大小转换次数。

## 第 4 章：引入类、对象和方法

![](img/bced2a82848b29e0ff396f252376b6d4_136_0.png)

## 核心技能与概念

- 类基础
- 实例化对象
- 方法基础
- 方法参数
- 从方法返回值
- 构造函数
- `new`
- 垃圾回收
- 析构函数

在深入学习 C# 之前，你需要学习类。类是 C# 的本质，因为它定义了对象的性质。因此，类构成了 C# 面向对象编程的基础。类内部定义了数据以及处理这些数据的代码。由于类、对象和方法是 C# 的基础，它们在这一章中被介绍。对这些特征的基本了解将允许你编写更复杂的程序，并更好地理解第 5 章中描述的某些元素。

### 类基础

从本书开始，我们一直在使用类。当然，我们一直使用的是极其简单的类，并且没有利用它们的大部分功能。正如你所看到的，类比这些有限的类要强大得多。类是一个定义对象形式的模板。它通常同时指定代码和数据。对象是类的实例。因此，类本质上是一个抽象；直到该类的对象被创建后，内存中才存在物理表示。回想构成类的方法和变量被称为成员。

### 类的通用形式

当你定义一个类时，你声明它包含的数据和操作这些数据的代码。虽然非常简单的类可能只包含代码或数据，但现实世界的类二者兼备。从通俗来说，数据包含在类定义的实例变量中，代码包含在方法中。需要说明的是，C# 定义了几种类型的成员，包括实例变量、常量、构造函数、析构函数、索引器、事件和运算符。现在我们把对类的讨论限制在它的要素元素：实例变量和方法。在本章的晚些时候，将讨论构造函数和析构函数。

### 类的实例化与成员访问

每当你创建一个类的实例时，你都会创建一个对象，该对象包含了该类中定义的每个实例变量的独立拷贝。因此，每个 `Vehicle` 对象都包含其实例变量 `Passengers`、`FuelCap` 和 `Mpg` 的拷贝。要访问这些变量，你将使用成员访问运算符，它是一个句号 `.`。它通常被称为点运算符。点运算符将对象的名称与成员的名称连接起来。形式为：

```
object.member
```

例如，使用以下语句将 `minivan` 的 `FuelCap` 变量赋值为 16：

```
minivan.FuelCap = 16;
```

通常，你可以使用点运算符来访问实例变量和方法。这里是一个使用 `Vehicle` 类的完整程序：

```csharp
/* 使用 Vehicle 类的程序。请将此文件命名为 UseVehicle.cs */
using System;
// 一个封装车辆信息的类。
class Vehicle {
    public int Passengers; // 客员人数
    public int FuelCap; // 油箱容量（加仑）
    public int Mpg; // 每加仑英里的油耗
}
// 此类声明了一个 Vehicle 类型的对象。
class VehicleDemo {
    static void Main() {
        Vehicle minivan = new Vehicle();
        // 为 minivan 中的字段赋值。
        minivan.Passengers = 7;
        minivan.FuelCap = 16;
        minivan.Mpg = 21;
        // 假设油箱是满，计算行驶里程。
        int range = minivan.FuelCap * minivan.Mpg;
        Console.WriteLine("Minivan can carry " + minivan.Passengers + " with a range of " + range);
    }
}
```

此程序由两个类组成：`Vehicle` 和 `VehicleDemo`。在 `VehicleDemo` 内部，`Main()` 方法创建名为 `minivan` 的 `Vehicle` 实例。然后，代码内部访问与 `minivan` 相关的实例变量，为它们赋值并使用这些值。`Vehicle` 和 `VehicleDemo` 是两个独立的类。它们之间唯一的的关系是其中一个创建另一个的实例。尽管它们是独立的类，但如果 `Vehicle` 的成员没有赋予 `public` 访问修饰符，`VehicleDemo` 内部将无法访问这些成员。

编译此程序会创建一个 `UseVehicle.exe` 文件。`Vehicle` 和 `VehicleDemo` 类都自动成为可执行文件的一部分。该程序将显示以下输出：

```
Minivan can carry 7 with a range of 336
```

`Vehicle` 和 `VehicleDemo` 两个类并不非要位于同一个源文件中。你可以将每个类放在它们自己的文件中，例如命名为 `Vehicle.cs` 和 `VehicleDemo.cs`。只需使用 C# 编译器编译这两个文件并将它们链接在一起即可。例如：

```
csc Vehicle.cs VehicleDemo.cs
```

这将创建 `VehicleDemo.exe`，因为该类是包含 `Main()` 方法。

每个对象都拥有其类所定义的实例变量的独立拷贝。因此，一个对象中的变量内容可能与另一个对象中的变量内容不同。以下程序演示了这一事实：

```csharp
// 演示每个对象拥有其类定义的实例变量的拷贝。
using System;
class Vehicle {
    public int Passengers;
    public int FuelCap;
    public int Mpg;
}
class VehicleDemo {
    static void Main() {
        Vehicle minivan = new Vehicle();
        minivan.Passengers = 7;
        minivan.FuelCap = 16;
        minivan.Mpg = 21;
```
