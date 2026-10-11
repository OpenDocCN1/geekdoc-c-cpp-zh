
```csharp
public class Vehicle {

    public string model;      // 模型名称

    public string manufacturer; // 同上

    public int numOfDoors;      // 车辆的门数

    public int numOfWheels;     // 你懂我意思的。

}
```

类的定义以 `public class` 单词开始，后面跟着类名——在本例中是 `Vehicle`。

和 C# 中的所有内容一样，类名对大小写敏感。C# 不强制执行任何关于命名的规则，但有一个非正式的规定：类名以大写字母开头。

类名后面是一对大括号。类的成员是构成类部分的变量。在这个示例中，`class Vehicle` 类从成员 `string model` 开始，它包含车辆的模型名称。如果这辆车是汽车，它的名字可以是 `Trooper II`。（你见过或听过 `Trooper II` 吗？）第二个

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_241_0.png)

### 定义类和对象 217

这个 `Vehicle` 类示例成员是 `string manufacturer`。另外两个属性是车辆的门数和轮数。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_242_0.png)

提示：像任何变量一样，成员名称尽可能描述。

### 展现类

### 什么是实例（instance）？

在 C# 术语中，你说 `myCar` 是一个类的对象。你也可以把 `instance` 当作动词用，即实例化（instantiating）。它的意思是：“……的一个例子”或“之一”。

### 定义类

### 访问对象的成员

以下代码创建了一个 `Vehicle` 对象：

```csharp
Vehicle myCar;
myCar = new Vehicle();
```

第一行声明了一个变量 `myCar`，第二行将一个新创建的 `Vehicle` 类型对象分配给该变量。`new Vehicle()` 表达式为 CPU、为世界、为整个宇宙分配了描述一个车辆所需的内存！

### 一个基于对象的程序示例

简单的 `VehicleDataOnly` 程序执行了这些任务：

- 定义 `Vehicle` 类。
- 创建对象 `myCar`。

# 一个基于对象的程序示例 219

- 给 `myCar` 分配属性。
- 从对象中检索值以进行显示。

这里是 `VehicleData` 程序的代码：

```csharp
// VehicleDataOnly - 创建一个 Vehicle 对象
```

程序列表从 `Vehicle` 类的定义开始。

## 220 区分对象

类的定义可以出现在类之前，也可以出现在之后——这并不重要。然而，不要像我一样，请选择一种风格并坚持下去。介绍 Visual Studio 的第四部分展示了更常规的技巧，即创建一个单独的 `.cs` 文件来包含每个类，但目前只需将额外的类放在你的 `Program.cs` 文件中即可。

该程序创建了类型为 `Vehicle` 的对象 `myCar`，然后通过从键盘读取适当的数据来填充每个字段。（输入数据没有经过检查——但应该检查其合法性。）程序以略微不同的格式写入了 `myCar` 的属性。

执行此程序的输出显示如下：

```
Enter the properties of your vehicle
Model name = Metropolitan
Manufacturer name = Nash
Number of wheels = 2
Number of wheels = 4
```

```
Your vehicle is
Nash Metropolitan
with 2 doors, riding on 4 wheels
Press Enter to terminate...
```

调用 `Read()` 而不是 `ReadLine()` 会让光标直接留在输出字符串之后，这使得使用者的输入显示在提示词的同一行。此外，在字符串中插入换行符 `'\n'` 会生成一个空行，而不需要执行 `WriteLine()`。

### 区分对象

底特律汽车制造商可以跟踪他们制造的每一辆汽车而不会混淆它们。同样，程序可以创建该类的多个对象，如示例所示：

```csharp
Vehicle car1 = new Vehicle();
car1.manufacturer = "Studebaker";
car1.model = "Austin";
// 以下操作对 car1 没有影响。
Vehicle car2 = new Vehicle();
car2.manufacturer = "Hudson";
car2.model = "Hornet";
```

创建对象 `car2` 并为其分配制造商名称 `Hudson` 对 `car1` 对象（制造商为 `Studebaker`）没有影响。

在某种，区分对象的能力是类结构的真正威力。与 `Hudson Hornet` 关联的对象可以作为一个独立的实体进行创建、操作和处理，它与其他对象（包括 `Avanti`）是分离的。（两者都是经典汽车，尤其是后者。）

### 你能给我引用吗？

点运算符和赋值运算符是定义在引用类型上的唯一两个运算符：

```csharp
// 创建一个空引用。
// yourCar;
// 分配引用值。
yourCar = new Vehicle();
// 使用点运算符访问成员。
yourCar.manufacturer = "Rambler";
// 创建一个新引用并使其指向同一个对象。
yourSpousalCar = yourCar;
```

第一行创建了 `yourCar` 但没有给它赋值。未初始化的引用被认为指向空对象（null object）。任何尝试使用未初始化（空）引用的行为都会立即产生错误并终止程序。

C# 编译器可以捕获大多数使用未初始化引用的尝试，并在编译时生成警告。如果你以某种方式绕过了编译器，访问未初始化的引用将立即终止程序。

第二个语句创建了一个新的 `Vehicle` 并将其赋值给 `yourCar`。这段代码段的最后一条语句将引用 `yourSpousalCar` 赋值给引用 `yourCar`。此操作调用的目的是让 `yourSpousalCar` 指向与 `yourCar` 相同的对象。这种关系如图 2-1 所示。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_246_0.png)

图 2-1：指向同一个对象的两个引用。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_246_1.png)

## 222 你能给我引用吗？

以下两个调用具有相同的效果：

```csharp
// 构建你的汽车。
yourCar = new Vehicle();
yourCar.model = "Kaiser";
// 它属于你的配偶。
yourSpousalCar = yourCar;
// 修改其中一个会改变另一个。
yourSpousalCar.model = "Henry J";
Console.WriteLine("Your car is a " + yourCar.model);
```

执行此程序将输出 `Henry J` 而不是 `Kaiser`。注意，`yourSpousalCar` 并不是指向 `yourCar`；相反，`yourCar` 和 `yourSpousalCar` 都指向同一辆汽车。

此外，即使变量 `yourCar` 以某种方式“丢失”（例如超出了作用范围），在这一段代码中，引用 `yourSpousalCar` 仍然有效：

```csharp
// 构建你的汽车。
yourCar = new Vehicle();
yourCar.model = "Kaiser";
// 它属于你的配偶。
yourSpousalCar = yourCar;
// 当你的配偶拿走你的车时
yourCar = null;
// .../yourCar 现在指向“空对象”。
// .../yourSpousalCar 仍然指向同一辆汽车
Console.WriteLine("Your car is a " + yourSpousalCar.model);
```

执行此程序会输出 `Your car was a Kaiser`，即使 `yourCar` 已不再有效。

该对象已无法通过 `yourCar` 访问。只有当 `yourCar` 和 `yourSpousalCar` 都“丢失”或置为空时，该对象才会变得完全无法访问。

在那个时候——至少在某个不可预测的晚期——C# 垃圾回收器会介入，并将之前该特定对象使用的空间返回到用于分配更多 `Vehicle`（或者 `Student`）的可用空间池中（我会在本小书后面的部分详细介绍垃圾回收）。

让一个对象变量（引用类型的变量，如 `Vehicle` 或 `Student`，而不是简单类型 `int` 或 `double`）指向不同的对象——正如我在这里所做的——使得在数组和集合中存储和操作对象非常高效。数组的每个元素都存储指向对象的引用，当你交换数组内的元素时，你移动的是引用而不是对象本身。引用在内存中的大小是固定的，与它们所指向的对象不同。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_247_0.png)

### 类的类是世界上最快乐的类

类的成员本身可以是指向其他类的引用。例如，车辆有发动机，发动机有功率效率因子。

```csharp
public class Vehicle {
    public string model;
    public string manufacturer;
    public int doors;
    public int wheels;
    public Motor motor;
}
public class Motor {
    public double power;
    public double efficiency;
}
```

与 `Hudson Hornet` 关联的对象可以作为一个独立的实体进行创建、操作和处理，它与其他对象（包括 `Avanti`）是分离的。（两者都是经典汽车，尤其是后者。）

## 224 生成静态成员

```csharp
// 现在创建汽车。
friendsCar = new Vehicle();
friendsCar.model = "Cherokee Sport";
friendsCar.manufacturer = "Jeep";
friendsCar.doors = 2;
friendsCar.wheels = 1;
// 将发动机到汽车。
friendsCar.motor = largerMotor;
```

从 `Vehicle` 可以分阶段访问发动机位移。你可以一步步进行，如这段代码：

```csharp
m = friendsCar.motor;
Console.WriteLine("The motor displacement is " + m.displacement);
```

或者，你可以直接访问，如下所示：

```csharp
Console.WriteLine("The motor displacement is " + friendsCar.motor);
```

无论哪种方式，你都只能通过 `Motor` 访问位移。

这些被封装在简单的 `VehicleAndMotor` 网站中，此处未完整显示。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_249_0.png)

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

## 本章内容

- 定义方法
- 向方法传递参数
- 获取返回结果
- 回顾 `WriteLine()` 方法

程序需要将大型程序拆分成易于处理的小块。例如，本微型书籍之前章节中包含的程序达到了一个人一次能消化的编程信息的极限。

C# 允许你将类代码分成称为“方法”（methods）的块。设计和实现良好的方法可以极大简化编写复杂程序的工作。

方法等同于其他语言中的函数、过程或子程序。区别在于，方法始终是类的一部分。

### 定义和使用方法

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
```
