

```csharp
}
class Owner
{
}
class Car : Vehicle
{
    static void Main()
    {
        Vehicle vehicle = new Vehicle();
        vehicle.Print();
    }
}
```

在前面的程序中，*Vehicle* 类有一个名为 *type* 的私有成员和一个名为 *Print()* 的方法，该方法在控制台上打印变量 type 的值。由于 type 定义在 Vehicle 类的范围内，因此此操作不会引发任何错误。此外，程序中定义了 Car 类，它继承 *Vehicle* 类。Vehicle 类中定义的 *Main()* 方法使用 *Vehicle* 类的对象调用 *Print()* 方法。程序的输出如下所示：

```text
The type of the car is Two-wheeler
```

## 受保护

当程序中实现继承时，会使用受保护访问修饰符。如果将基类的成员定义为 protected，则可以从派生该基类的类访问该成员。因此，这些成员的访问仅限于基类及其派生类。关键字 protected 用于将成员声明为受保护。清单 18.32 展示了受保护访问修饰符的示例。

**清单 18.32：** 展示受保护访问修饰符的示例

```csharp
using System;
class Vehicle
{
    protected string type;
}
class Owner
{
}
class Car : Vehicle
{
    static void Main()
    {
        Car car = new Car();
        car.type = "Four-wheeler";
        Console.WriteLine("The type of the car is " + car.type);
    }
}
```

如前面的程序所示，Owner 类不派生自 Vehicle 类；因此，它无法访问 Vehicle 类的受保护成员。代码的输出如下所示：

```text
The type of the car is Four-wheeler
```

## 内部

声明为 internal 的类成员只能从定义在程序集（或 .dll 文件）内部的类访问。我们在类成员声明之前使用 internal 关键字。清单 18.33 展示了内部访问修饰符的示例：

清单 18.33：展示内部访问修饰符的示例

```csharp
using System;
class Vehicle
{
    internal string type;
}
class Owner
{
    public void OwnerVehicle()
    {
        Vehicle vehicle = new Vehicle();
        vehicle.type = "Two-wheeler";
        Console.WriteLine("The owner has a " + vehicle.type);
    }
}
class Car : Vehicle
{
    static void Main()
    {
        Vehicle vehicle = new Vehicle();
        vehicle.type = "Four-wheeler";
        Console.WriteLine("The type of the car is " + vehicle.type);
        Owner owner = new Owner();
        owner.OwnerVehicle();
    }
}
```

在前面的程序中，Vehicle 类包含一个内部变量 type，该变量在 Owner 类以及派生类 Car 中均有引用。该程序的输出与公共访问修饰符所示的输出相同。

## 受保护内部

受保护内部修饰符表示受保护修饰符和内部修饰符的并集。我们使用 protected internal 关键字将成员声明为受保护内部成员。如果类的成员被声明为 protected internal，则它具有以下可访问性：

- 属于不同程序集的继承类可以访问当前程序集的受保护内部成员
- 位于同一程序集内的成员可以访问受保护内部成员

表 18.1 展示了 enum、class、interface 和 struct 的默认访问权限（√）以及支持的访问修饰符（♣）：

| C# 类型 | 公共 | 私有 | 受保护 | 内部 | 受保护内部 |
|---|---|---|---|---|---|
| enum | √ |  |  |  |  |
| class | ♣ | √ | ♣ | ♣ | ♣ |
| interface | √ |  |  |  |  |
| struct | ♣ | √ |  | ♣ |  |

现在，让我们详细了解接口。

```csharp
interface Ishape
{
    void CalculateArea();
    void PrintResult();
}
class Circle : Ishape
{
    public double result;
    public void CalculateArea()
    {
        result = 3.14 * 2 * 2;
    }
    public void PrintResult()
    {
        Console.WriteLine("The area of the circle of radius 2 mt is " + result + " sq mt");
    }
}
class Triangle : Ishape
{
    public double result;
    public void CalculateArea()
    {
        result = .5 * 2 * 2;
    }
    public void PrintResult()
    {
        Console.WriteLine("The area of the triangle of vertical height and base 2 mt is " + result + " sq mt");
    }
}
```

如清单 18.35 所示，接口 Ishape 有两个方法声明：CalculateArea() 和 PrintResult()。Circle 和 Triangle 类继承该接口，然后二者都定义了这两个方法，其访问修饰符设置为 public。Program 类中的 Main() 方法使用适当的类实例调用这两个成员方法。程序的输出如下所示：

```text
The area of the circle of radius 2 mt is 12.56 sq mt
The area of the triangle of vertical height and base 2 mt is 2 sq mt
```

## 显式接口

如果类的方法是在接口上定义的，则该接口称为显式接口。如清单 18.36 所示，方法定义是接口的显式声明。

**清单 18.36：** 在类中显式定义接口方法

```csharp
interface IInterface
{
    void Imethod();
}
class Iclass : IInterface
{
    //Explicit declaration of interface method
    public void IInterface.Imethod()
    {
        Console.WriteLine("This is an example of implicit interface");
    }
}
```

当一个类继承多个同名接口时，我们使用接口的显式定义。清单 18.37 展示了显式接口的示例。

清单 18.37：展示显式接口的示例

```csharp
using System;
class Program
{
    public static void Main()
    {
        GUIClass gui = new GUIClass();
        //Explicitly cast the IWin interface
        ((IWin)gui).GetMenu();
        //Explicitly cast the IOther interface
        ((IOther)gui).GetMenu();
    }
}
interface IWin
{
    void GetMenu();
}
interface IOther
{
    void GetMenu();
}
class GUIClass: IWin, IOther
{
    //Explicit definition of the methods of two interfaces
    void IWin.GetMenu()
    {
        Console.WriteLine("Windows menu is called");
    }
    void IOther.GetMenu()
    {
        Console.WriteLine("Other menu is called");
    }
}
```

在清单 18.37 中，我们定义了两个接口 IWin 和 IOther，其中两个接口都声明了名为 GetMenu() 的同一个方法。接下来，我们声明了一个名为 GUIClass 的类，并在其中显式定义了两个接口的方法。Program 类中声明的 Main() 方法通过将接口强制转换为类实例来调用接口方法；从而实现类型安全。当程序涉及多个接口定义时，使用显式接口是一种良好做法。前面程序的输出如下所示：

```text
windows menu is called
Other menu is called
```

现在让我们学习 C# 中的枚举器。

## 枚举器

枚举是强类型常量，其基础类型为整型。枚举器用于将一些常量分组，以定义对象的确定属性，而该对象的基础类型将由用户定义。在处理枚举器时，我们需要了解以下要点：

- 枚举器的基础类型可以是除 char 之外的任何整型。
- 一种类型的枚举器不能隐式赋值给另一种类型的枚举器，即使底层成员相同。这就是它被称为强类型的原因。
- 枚举器不能被继承，因为它是值类型，并且包含自己特定的值。
- 如果未显式定义基础类型，则从 0 开始的整数会自动分配给枚举器类型的成员。

