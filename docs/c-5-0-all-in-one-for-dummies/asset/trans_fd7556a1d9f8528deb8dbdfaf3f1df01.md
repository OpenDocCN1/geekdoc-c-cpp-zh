
该程序创建 `Vehicle` 类的对象 `myCar`，然后通过从键盘读取适当数据来填充每个字段。（输入数据没有——但应该——进行合法性检查。）然后程序以略有不同的格式写出 `myCar` 的属性。

执行此程序的输出如下所示：

```
Enter the properties of your vehicle
Model name = Metropolitan
Manufacturer name = Nash
Number of doors = 2
Number of wheels = 4

Your vehicle is a
Nash Metropolitan
with 2 doors, riding on 4 wheels
Press Enter to terminate...
```

调用 `Read()` 而不是 `ReadLine()` 会使光标直接留在输出字符串之后，这使得用户输入显示在提示符同一行。此外，在写入中插入换行字符 '\n' 会生成一个空行，而无需单独执行 `WriteLine()`。

![](img/80ff26f06fc9ab951e1cd4257b867366_241_0.png)

## 区分对象

底特律汽车制造商可以追踪他们制造的每一辆车，而不会把车弄混。同样，程序可以创建同一类的多个对象，如下例所示：

```
Vehicle car1 = new Vehicle();
car1.manufacturer = "Studebaker";
car1.model = "Avanti";
// The following has no effect on car1.
Vehicle car2 = new Vehicle();
car2.manufacturer = "Hudson";
car2.model = "Hornet";
```

创建对象 `car2` 并为其分配制造商名称 Hudson，对 `car1` 对象（制造商名称为 Studebaker）没有影响。

在某种程度上，区分对象的能力正是类构造的真正威力所在。与 Hudson Hornet 关联的对象可以作为一个单独的实体创建、操作和处置，并独立于其他对象，包括 Avanti。（两者都是经典汽车，尤其是后者。）

## 能给我引用吗？

点运算符和赋值运算符是引用类型上仅有的两个已定义运算符：

```
// Create a null reference.
Vehicle yourCar;
// Assign the reference a value.
yourCar = new Vehicle();
// Use the dot to access a member.
yourCar.manufacturer = "Rambler";
// Create a new reference and point it to the same object.
Vehicle yourSpousalCar = yourCar;
```

第一行创建对象 `yourCar`，但没有为其赋值。尚未初始化的引用称为指向 null 对象。任何使用未初始化（null）引用的尝试都会立即产生错误并终止程序。

![](img/80ff26f06fc9ab951e1cd4257b867366_242_0.png)

C# 编译器可以在构建时捕获大多数使用未初始化引用的尝试，并生成警告。如果你以某种方式绕过编译器，访问未初始化的引用会立即终止程序。

第二条语句创建一个新的 `Vehicle` 对象，并将其赋给 `yourCar`。此代码片段中的最后一条语句将引用 `yourSpousalCar` 赋给引用 `yourCar`。此操作使 `yourSpousalCar` 引用与 `yourCar` 相同的对象。这种关系如图 2-1 所示。

图 2-1：
两个引用指向同一对象。

![](img/80ff26f06fc9ab951e1cd4257b867366_242_1.png)

以下两个调用具有相同的效果：

```
// Build your car.
Vehicle yourCar = new Vehicle();
yourCar.model = "Kaiser";
// It also belongs to your spouse.
Vehicle yourSpousalCar = yourCar;
// Changing one changes the other.
yourSpousalCar.model = "Henry J";
Console.WriteLine("Your car is a " + yourCar.model);
```

执行此程序将输出 Henry J，而不是 Kaiser。请注意，`yourSpousalCar` 并不指向 `yourCar`；相反，`yourCar` 和 `yourSpousalCar` 都引用同一辆车。

此外，即使变量 `yourCar` 以某种方式“丢失”（例如超出作用域），引用 `yourSpousalCar` 仍然有效，如这段代码所示：

```
// Build your car.
Vehicle yourCar = new Vehicle();
yourCar.model = "Kaiser";
// It also belongs to your spouse.
Vehicle yourSpousalCar = yourCar;
// When your spouse takes your car away...
yourCar = null; // yourCar now references the "null object."
// ...yourSpousalCar still references the same vehicle.
Console.WriteLine("your car was a " + yourSpousalCar.model);
```

执行此程序会生成输出 Your car was a Kaiser，即使引用 `yourCar` 不再有效。

对象不再能从引用 `yourCar` 访问。直到 `yourCar` 和 `yourSpousalCar` 都“丢失”或置空，对象才完全不可达。

此时——好吧，总之在某个不可预测的较晚时刻——C# 垃圾回收器介入，将该 `Vehicle` 对象先前使用的空间返还到可用于分配更多 Vehicles（或 Students）的空间池。（关于垃圾回收，我在本迷你书第 6 章末尾的边栏中再多说一点。）

![](img/80ff26f06fc9ab951e1cd4257b867366_243_0.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_243_1.png)

使一个对象变量（引用类型变量，如 `Vehicle` 或 `Student`，而不是 `int` 或 `double` 这样的简单类型）指向不同对象——如我在此所做的——使得在数组和集合中存储和操作引用对象非常高效。数组的每个元素存储对对象的引用，当你在数组中交换元素时，只是移动引用，而不是对象本身。引用在内存中有固定大小，不同于它们引用的对象。

## 包含类的类是世界最幸福的类

类的成员本身可以是对其他类的引用。例如，车辆有发动机，发动机有功率和效率因素，包括排量。你可以这样直接把这些因素塞进类中：

```
public class Vehicle
{
    public string model;        // Name of the model
    public string manufacturer; // Ditto
    public int numOfDoors;      // The number of doors on the vehicle
    public int numOfWheels;     // You get the idea.
    // New stuff:
    public int power;           // Power of the motor [horsepower]
    public double displacement; // Engine displacement [liter]
}
```

然而，功率和发动机排量不是汽车的属性。例如，你朋友的 Jeep 可能有两个不同的发动机选项，马力水平差异很大。2.4 升的 Jeep 是蜗牛，而同样车配备 4.0 升发动机则相当轻快。

发动机是独立概念，值得拥有自己的类：

```
public class Motor
{
    public int power;       // Power [horsepower]
    public double displacement; // Engine displacement [liter]
}
```

你可以将此组合到 `Vehicle` 中（见粗体文本）：

```
public class Vehicle
{
    public string model;        // Name of the model
    public string manufacturer; // Ditto
    public int numOfDoors;      // The number of doors on the vehicle
    public int numOfWheels;     // You get the idea.
    public Motor motor;
}
```

现在创建 `myCar` 如下所示：

```
// First create a Motor.
Motor largerMotor = new Motor();
largerMotor.power = 230;
largerMotor.displacement = 4.0;
// Now create the car.
Vehicle friendsCar = new Vehicle();
friendsCar.model = "Cherokee Sport";
friendsCar.manufacturer = "Jeep";
friendsCar.numOfDoors = 2;
friendsCar.numOfWheels = 4;
// Attach the motor to the car.
friendsCar.motor = largerMotor;
```

从 `Vehicle` 可以分两步访问发动机排量。可以一次一步，如这段代码所示：

```csharp
Motor m = friendsCar.motor;
Console.WriteLine("The motor displacement is " + m.displacement);
```

或者，可以直接访问，如下所示：

```csharp
Console.WriteLine("The motor displacement is " + friendsCar.motor.displacement);
```

无论哪种方式，都只能通过 `Motor` 访问排量。

此示例包含在本书网站上的简单程序 VehicleAndMotor 中，此处不完整展示。

![](img/80ff26f06fc9ab951e1cd4257b867366_245_0.png)

## 类成员中的静态

类的大多数数据成员特定于包含它们的对象，而不是其他对象。考虑 `Car` 类：

```csharp
public class Car
{
    public string licensePlate;     // The license plate ID
}
```

因为车牌 ID 是 *对象属性*，它唯一描述 `Car` 类的每个对象。例如，谢天谢地我的车牌和你的不同；否则你可能出不了车道，如这段代码所示：

```csharp
Car myCar = new Car();
myCar.licensePlate = "XYZ123";

Car yourCar = new Car();
yourCar.licensePlate = "ABC789";
```

然而，有些属性是所有汽车共有的。例如，已制造的汽车数量是 `Car` 类的属性，但不是任何单个对象的属性。这些 *类属性* 在 C# 中用关键字 `static` 标记：

```csharp
public class Car
{
    public static int numberOfCars;  // The number of cars built
    public string licensePlate;      // The license plate ID
}
```

![](img/80ff26f06fc9ab951e1cd4257b867366_245_1.png)

静态成员不是通过对象访问。相反，通过类本身访问它们，如这段代码片段所示：

```csharp
// Create a new object of class Car.
Car newCar = new Car();
newCar.licensePlate = "ABC123";
// Now increment the count of cars to reflect the new one.
Car.numberOfCars++;
```
