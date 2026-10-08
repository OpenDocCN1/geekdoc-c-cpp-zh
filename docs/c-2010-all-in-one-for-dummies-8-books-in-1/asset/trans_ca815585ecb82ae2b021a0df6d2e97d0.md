

# 一个基于对象的程序示例 219

- 给 myCar 分配属性。
- 从对象中检索值以进行显示。

这里是 VehicleData 程序的代码：

```csharp
// VehicleDataOnly - 创建一个 Vehicle 对象
```

程序列表从 Vehicle 类的定义开始。

## 220 区分对象

类的定义可以出现在类之前，也可以出现在之后——这并不重要。然而，不要像我一样，请选择一种风格并坚持下去。介绍 Visual Studio 的第四部分展示了更常规的技巧，即创建一个单独的 .cs 文件来包含每个类，但目前只需将额外的类放在你的 Program.cs 文件中即可。

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

## 区分对象

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

在某种，区分对象的能力是类结构的真正威力。与 Hudson Hornet 关联的对象可以作为一个独立的实体进行创建、操作和处理，它与其他对象（包括 Avanti）是分离的。（两者都是经典汽车，尤其是后者。）

## 你能给我引用吗？

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

执行此程序将输出 Henry J 而不是 Kaiser。注意，`yourSpousalCar` 并不是指向 `yourCar`；相反，`yourCar` 和 `yourSpousalCar` 都指向同一辆汽车。

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

执行此程序会输出 Your car was a Kaiser，即使 `yourCar` 已不再有效。

该对象已无法通过 `yourCar` 访问。只有当 `yourCar` 和 `yourSpousalCar` 都“丢失”或置为空时，该对象才会变得完全无法访问。

在那个时候——至少在某个不可预测的晚期——C# 垃圾回收器会介入，并将之前该特定对象使用的空间返回到用于分配更多 `Vehicle`（或者 `Student`）的可用空间池中（我会在本小书后面的部分详细介绍垃圾回收）。

让一个对象变量（引用类型的变量，如 `Vehicle` 或 `Student`，而不是简单类型 `int` 或 `double`）指向不同的对象——正如我在这里所做的——使得在数组和集合中存储和操作对象非常高效。数组的每个元素都存储指向对象的引用，当你交换数组内的元素时，你移动的是引用而不是对象本身。引用在内存中的大小是固定的，与它们所指向的对象不同。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_247_0.png)

## 类的类是世界上最快乐的类

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

与 Hudson Hornet 关联的对象可以作为一个独立的实体进行创建、操作和处理，它与其他对象（包括 Avanti）是分离的。（两者都是经典汽车，尤其是后者。）

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

