
将 myCar 的声明与一个名为 num 的 int 变量的声明进行比较：

```csharp
int num;
num = 1;
```

第一行声明了变量 num，第二行将一个已创建的 int 类型常量赋给变量 num 所在的位置。

int 类型的 num 和对象 myCar 在内存中的存储方式不同。常量 1 不占用内存，因为 CPU 和 C# 编译器始终知道 1 是什么。你的 CPU 没有 Vehicle 的概念。new Vehicle 表达式会分配必要的内存，以便向 CPU、向 C#、向世界，乃至向宇宙描述一辆车！

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_243_0.png)

## 访问对象的成员

Vehicle 类的每个对象都有自己的一组成员。以下表达式将数字 1 存入 myCar 所引用对象的 numberOfDoors 成员：

```csharp
myCar.numberOfDoors = 1;
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_243_1.png)

每个 C# 操作都必须按类型和值进行求值。对象 myCar 是 Vehicle 类型的对象。变量 Vehicle.numberOfDoors 的类型为 int。（再查看一下 Vehicle 类的定义。）常量 1 的类型也是 int，因此赋值运算符右侧的变量类型与左侧的变量类型匹配。

类似地，以下代码存储指向描述 myCar 型号和制造商名称的字符串的引用：

```csharp
myCar.manufacturer = "BMW";    // Don't get your hopes up.
myCar.model = "Isetta";       // The Urkel-mobile
```

Isetta 是 20 世纪 50 年代制造的一款小型汽车，只有一扇门，打开时整个车头都会敞开。我把 Urkel 留给你和你最喜欢的搜索引擎。

## 一个基于对象的程序示例

简单的 VehicleDataOnly 程序执行以下任务：

- 定义 Vehicle 类。
- 创建对象 myCar。
- 为 myCar 分配属性。
- 从对象中检索这些值以进行显示。

以下是 VehicleDataOnly 程序的代码：

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_244_0.png)

```csharp
// VehicleDataOnly -- Create a Vehicle object, populate its
// members from the keyboard, and then write it back out.
using System;
namespace VehicleDataOnly
{
    public class Vehicle
    {
        public string model;    // Name of the model
        public string manufacturer; // Ditto
        public int numOfDoors;  // The number of doors on the vehicle
        public int numOfWheels; // You get the idea.
    }
    public class Program
    {
        // This is where the program starts.
        static void Main(string[] args)
        {
            // Prompt user to enter her name.
            Console.WriteLine("Enter the properties of your vehicle!");
            // Create an instance of Vehicle.
            Vehicle myCar = new Vehicle();
            // Populate a data member via a temporary variable.
            Console.Write("Model name = ");
            string s = Console.ReadLine();
            myCar.model = s;
            // Or you can populate the data member directly.
            Console.Write("Manufacturer name = ");
            myCar.manufacturer = Console.ReadLine();
            // Enter the remainder of the data.
            // A temp is useful for reading ints.
            Console.Write("Number of doors = ");
            s = Console.ReadLine();
            myCar.numOfDoors = Convert.ToInt32(s);
            Console.Write("Number of wheels = ");
            s = Console.ReadLine();
            myCar.numOfWheels = Convert.ToInt32(s);
            // Now display the results.
            Console.WriteLine("\nYour vehicle is a ");
            Console.WriteLine(myCar.manufacturer + " " + myCar.model);
            Console.WriteLine("with " + myCar.numOfDoors + " doors, ");
            Console.WriteLine("and " + myCar.numOfWheels + " wheels.");
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}
```

程序清单以 Vehicle 类的定义开始。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_245_0.png)

类的定义可以出现在 Program 类之前或之后——这无关紧要。不过，你应当（不要像我这样）采用一种风格并坚持下去。第 IV 册讨论了 Visual Studio，展示了更常规的技术：创建单独的 .cs 文件来包含每个类；不过现在只需把额外的类放在 Program.cs 文件中即可。

该程序创建 Vehicle 类的对象 myCar，然后通过从键盘读取相应数据来填充每个字段。（输入数据并未——但本应——进行合法性检查。）随后，程序以略微不同的格式写出 myCar 的属性。

执行该程序后的输出如下所示：

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

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_245_1.png)

调用 Write() 而不是 WriteLine() 会使光标直接停留在输出字符串之后，从而使用户的输入与提示显示在同一行。此外，在 Write 中插入换行字符 '\n' 会生成一个空行，而无需单独执行 WriteLine()。

## 区分对象

底特律的汽车制造商能够追踪他们制造的每一辆汽车，而不会把汽车弄混。类似地，程序可以创建同一个类的许多对象，如下例所示：

```csharp
Vehicle car1 = new Vehicle();
car1.manufacturer = "Studebaker";
car1.model = "Avanti";
// The following has no effect on car1.
Vehicle car2 = new Vehicle();
car2.manufacturer = "Hudson";
car2.model = "Hornet";
```

创建对象 car2 并为其分配制造商名称 Hudson，不会影响 car1 对象（其制造商名称为 Studebaker）。

在某种程度上，区分对象的能力正是类构造的真正威力所在。与 Hudson Hornet 关联的对象可以作为一个单独的实体创建、操作和丢弃，并与其他对象（包括 Avanti）分开。（两者都是经典汽车，尤其是后者。）

## 你能给我引用吗？

点运算符和赋值运算符是引用类型上仅有的两个已定义运算符：

```csharp
// Create a null reference.
Vehicle yourCar;
// Assign the reference a value.
yourCar = new Vehicle();
// Use dot to access a member.
yourCar.manufacturer = "Rambler";
// Create a new reference and point it to the same object.
Vehicle yourSpousalCar = yourCar;
```

第一行创建引用 yourCar，但没有为其赋值。尚未初始化的引用被称为指向 null 对象。任何使用未初始化（null）引用的尝试都会立即产生错误并终止程序。

C# 编译器可以捕获大多数使用未初始化引用的尝试，并在构建时生成警告。如果你不知怎么让一个这样的用法逃过了编译器，访问未初始化的引用会立即终止程序。

第二条语句创建一个新的 Vehicle 对象，并将其赋给 yourCar。代码片段中的最后一条语句将引用 yourSpousalCar 赋给引用 yourCar。此操作使 yourSpousalCar 引用与 yourCar 相同的对象。这种关系如图 2-1 所示。

图 2-1：指向同一对象的两个引用。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_246_0.png)

以下两次调用具有相同的效果：

```csharp
// Build your car.
Vehicle yourCar = new Vehicle();
yourCar.model = "Kaiser";
// It also belongs to your spouse.
Vehicle yourSpouseCar = yourCar;
// Changing one changes the other.
yourSpouseCar.model = "Henry J";
Console.WriteLine("Your car is a " + yourCar.model);
```

执行该程序将输出 Henry J，而不是 Kaiser。注意，yourSpouseCar 并不指向 yourCar；相反，yourCar 和 yourSpouseCar 都引用同一辆车。

此外，即使变量 yourCar 以某种方式“丢失”（例如超出作用域），引用 yourSpouseCar 仍然有效，如下面这段代码所示：

```csharp
// Build your car.
Vehicle yourCar = new Vehicle();
yourCar.model = "Kaiser";
// It also belongs to your spouse.
Vehicle yourSpouseCar = yourCar;
// When your spouse takes your car away . . .
yourCar = null;      // yourCar now references the "null object."
                     // yourSpouseCar still references the same vehicle.
Console.WriteLine("Your car was a " + yourSpouseCar.model);
```

执行该程序会生成输出 Your car was a Kaiser，即使引用 yourCar 已不再有效。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_247_0.png)

该对象不再能从引用 yourCar 访问到。直到 yourCar 和 yourSpouseCar 都“丢失”或被置为 null，该对象才会变得完全不可访问。

到那时——好吧，反正是在某个不可预测的稍后时刻——C# 垃圾回收器会介入，并将该特定 Vehicle 对象原先使用的空间返还到可用于分配更多 Vehicle（就此而言，也可以是 Student）的空间池中。（我在本迷你书第 6 章末尾的边栏中还会稍微多讲一点垃圾回收。）

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_247_1.png)

让一个对象变量（引用类型的变量，如 Vehicle 或 Student，而不是 int 或 double 这样的简单类型变量）指向另一个对象——就像我在这里所做的——会使在数组和集合中存储和操作引用对象变得相当高效。数组的每个元素都存储一个指向对象的引用；当你在数组中交换元素时，你只是在移动引用，而不是对象本身。引用在内存中具有固定大小，这一点与它们所引用的对象不同。
