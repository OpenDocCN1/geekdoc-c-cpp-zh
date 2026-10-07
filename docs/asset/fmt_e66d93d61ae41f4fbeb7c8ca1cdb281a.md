
这应该是合逻辑的，因为卡车和汽车不是同一种东西。然而，从逻辑上讲，卡车和汽车都是 `FourWheeledVehicle`。

## 3. 在 `Program.cs` 文件的 `Main` 方法中输入以下代码：

```csharp
Vehicle v1 = new Vehicle();
Car c1 = (Car)v1;
```

## 4. 按 `Ctrl+F5` 运行应用程序。你应该遇到一个 `InvalidCastException`，如图 5.2 所示。

![](img/d08df1b94a49a49b95ebbdc5e982bda6_134_0.png)

### 图 5.2

显示 `InvalidCastException` 的结果。

## 5. 移除你之前在步骤 2 中输入的语句，并将其替换为图 5.2 所示的代码。

## 6. 再次按 `Ctrl+F5` 运行应用程序，观察输出是否与图 5.3 一致。

![](img/d08df1b94a49a49b95ebbdc5e982bda6_134_1.png)

### 图 5.3

使用类继承和多态的结果。

列表 5.3 显示了列表 5.1 中代码层次的修改版本，为某些派生类提供了构造函数，这些构造函数调用了基类构造函数之一。

### 注意

#### 构造函数链和默认构造函数

如果没有显式地链接基类构造函数，编译器会尝试链接默认构造函数。

问题在于，并非所有类都有公共的默认构造函数，在这种情况下，忘记显式地链接正确的基类构造函数会导致编译器错误。

### 列表 5.3 派生类中的构造函数

```csharp
public class Vehicle
{
    private Vehicle() { }

    public Vehicle(int wheels)
    {
        Console.WriteLine("The number of wheels requested is {0}", wheels);
    }
}

public class FourWheeledVehicle : Vehicle
{
    public FourWheeledVehicle() : base(4) {}
}

public class TwoWheeledVehicle : Vehicle
{
    public TwoWheeledVehicle() : base(2) { }
}

public class Car : FourWheeledVehicle { }

public class Truck : FourWheeledVehicle { }

public class Motorcycle : TwoWheeledVehicle { }
```

## 构造函数链

通过这些步骤，你修改了在前节中创建的类层次以探索构造函数链。如果你关闭了 Visual Studio，请重复之前的练习。确保在练习结束时保持 Visual Studio 打开，因为你稍后会用到。

- 1. 打开名为 `Vehicles.cs` 的文件。
- 2. 修改类以反映列表 5.3 所示的代码。
- 3. 在 `Program.cs` 文件的 `main` 方法中，将代码替换为创建新汽车、卡车和三轮车的代码。
- 4. 使用 `Ctrl+F5` 运行应用程序，观察输出是否与图 5.4 Consistent。

## 继承与多态

![](img/d08df1b94a49a49b95ebbdc5e982bda6_136_0.png)

### 图 5.4 使用构造函数链的结果。

## 使用继承的成员

有时，派生类需要一个具有相同名称的方法或属性，但行为是通过成员重写（member overriding）来实现的。为了保持尽可能清晰，C# 要求使用两个不同的关键字来重写成员。在基类中，成员声明必须包含 `virtual`，而在派生类中，成员声明必须包含 `override`。

通常，`virtual` 成员在它们实现的行为上是类似的——如果它们确实提供了行为的话。其目的是确保在所有情况下，派生类都拥有该成员，并且它将执行某些默认行为。预期派生类将用更合适、更具体的行为来重写 `virtual` 成员。

就像使用构造函数一样，你可以使用 `base` 关键字来访问原始实现。基类的行为与此关键字类似，但它引用的是直接基类，而不是当前类。

成员重写具有某些限制：

- 重写的成员声明不能更改 `virtual` 成员声明的访问可见性。
- 原生成员和被重写的成员都不能声明为 `private`。
- 两个声明必须具有相同的签名。
- 重写的成员不能包含新的、静态的或 `virtual` 修饰符。

### 注意

#### 默认 virtual 成员

虽然 Java 等面向对象的语言默认将成员设为 `virtual`，但 C# 则不是。这意味着你必须显式说明成员可能被重写，包括使用 `virtual` 关键字，因为只有声明为 `virtual` 的成员才能被重写。

## 重写基类成员

按照这些步骤修改你之前创建的类，以创建 `virtual` 和重写的类成员。如果你关闭了 Visual Studio，请重复之前的练习。确保在练习结束时保持 Visual Studio 打开，因为你稍后会用到此应用程序。

- 1. 打开名为 `Vehicles.cs` 的文件。
- 2. 修改 `Vehicle` 类包含一个 `virtual Operate` 方法，该方法只需向控制台打印“Default”。
- 3. 修改 `FourWheeledVehicle` 和 `TwoWheeledVehicle` 类以重写 `Operate` 方法，并在调用 `base.Operate()` 后分别打印“Driving a four-wheeled vehicle” 和“Riding a two-wheeled vehicle”。
- 5. 在 `Program.cs` 文件的 `Main` 方法中，每个每个实例之后添加对 `Operate` 的调用。随后使用 `Console.WriteLine()` 打印空行。
- 6. 使用 `Ctrl+F5` 运行应用程序，观察输出是否与图 5.5 一致。

```
C\system32\cmd.exe
The number of wheels requested is 4
Driving a car
The number of wheels requested is 2
Default
Riding a two-wheeled vehicle
The number of wheels requested is 4
Default
Driving a four-wheeled vehicle
The number of wheels requested is 3
Default
Press any key to continue...
```

### 图 5.5 显示重写基类成员的行为结果。

正如你从上一个练习看到的，被重写的成员隐式是 `virtual` 的，并且可以被后续派生类进一步重写。你在 `Car` 类中为 `Drive` 实现 `override` 时就执行了这一点，尽管 `FourWheeledVehicle` 已经重写了。通常这种行为是理想的；但有时你可能希望防止其发生。

## 继承与多态 119

### 注意

#### 成员隐藏

除了成员重写外，C# 还允许你隐藏基类成员。这通常在你需要重新定义一个非 `virtual` 基类成员时完成，通过在在新定义前面添加 `new` 关键字来实现。由于成员隐藏基于签名，因此你可以使用成员隐藏来更改成员的返回类型。

隐藏基类成员可能会产生意料之外或至少是非预期的结果。虽然在派生类中隐藏基类成员可能是故意的，但它通常是由于基类的变化（你可能或无法控制）导致你无意中隐藏了基类成员或设计错误的类层次结构。因此，当基类成员被隐藏时，编译器会生成警告。使用 `new` 关键字并不能消除隐藏基类成员时谨慎的必要；它只是使其变得显式。

你可以通过密封（sealing）类成员或类来阻止进一步继承。要密封一个类成员，除了 `override` 关键字外还必须包含 `sealed` 关键字。要密封一个类，只需包含 `sealed` 关键字。

例如，要密封“Overriding Class Members” Try It Yourself 中的 `FourWheeledVehicle.Oper` 方法，你需要在方法签名中添加 `sealed` 关键字，如下所示：

```csharp
public class FourWheeledVehicle
{
    public FourWheeledVehicle() : base(4) {}

    public sealed override void Operate()
    {
        base.Operate();
        Console.WriteLine("Driving a four-wheeled vehicle");
    }
}
```

同样，如果你想防止从 `TwoWheeledVehicle` 类进一步衍生，你需要在类定义中添加 `sealed` 关键字，如下所示：

```csharp
public sealed class TwoWheeledVehicle
{
    public TwoWheeledVehicle() : base(2) {}

    public override void Operate()
    {
        base.Operate();
        Console.WriteLine("Riding a two-wheeled vehicle");
    }
}
```

### 密封类 (Sealing Classes)

为继承正确设计类可能是一项大量工作，因此你有三个选择：

- 保持类为未密封状态，但通过工作使其能够安全地被继承，如果没有人继承你的类，这些工作最终可能是不必要的。
- 保持类为未密封状态但不进行这些工作。这会将理解如何安全地扩展你的类的负担留给使用者。
- 密封该类。如果你有理由确定没有人需要继承你的类，那么这可能是最好的选择。密封的类总是可以取消密封的，而且这不会对已经使用该类的代码产生任何破坏性影响。密封类还允许在 JIT 编译期间发生某些运行时优化。

## 抽象类和成员 (Abstract Classes and Members)

虽然继承一个类可以带来很多好处，但在某些情况下，你需要为派生类提供标准的实现，并需要保证派生类为特定的属性或方法提供实现，或者仅仅是拥有没有实例的类在逻辑上是合理的。回想车辆层级结构，根本不存在既是“车辆”又是更特定类型车辆的对象。为了实现这些目标，C# 提供了 `abstract` 修饰符，该修饰符可以同时应用于类和类成员。

通过将类声明为 `abstract`，你防止了它被直接实例化。因此，抽象类通常具有受保护（protected）构造函数而不是公共（public）构造函数。如果你不提供默认构造函数，编译器会为你创建一个受保护的默认构造函数。抽象类可以包含虚（virtual）、非虚（nonvirtual）和抽象（abstract）成员。抽象成员用 `abstract` 修饰符声明，但不提供实现。列表 5.4 显示了 `Vehicle` 类作为抽象类的示例，它包含一个名为 `Operate` 的抽象方法。

## 静态类 (Static Classes)

编译器实际上将静态类实现为密封的抽象类（sealed abstract classes），防止它们被实例化或继承。

## 列表 5.4 抽象车辆类

```csharp
public abstract class Vehicle
{
    int wheels;

    protected Vehicle() {

    public Vehicle(int wheels)
    {
    this.wheels = wheels;
    }

    public abstract void Operate();
```

与派生类可以选择性重写的虚成员不同，抽象成员必须在具体的（非抽象）派生类中被重写。如果派生类也是抽象的，则它不需要重写基类成员。由于抽象成员在派生类中被重写之前没有实现，因此该重写成员无法调用来自基类中的同一个成员。

## 使用抽象类 (Using Abstract Classes)

通过遵循以下步骤，你将探索如何创建一个抽象类，并将其用作派生类的基类。如果你关闭了 Visual Studio，请先重复之前的练习。确保在本次练习结束时保持 Visual Studio 打开，你稍后会使用此应用程序。

1. 打开名为 `Vehicles.cs` 的文件。
2. 修改 `Vehicle` 类使其成为抽象类，并使 `Operate` 方法成为抽象方法。
3. 修正产生的编译器错误。
4. 使用 `Ctrl+F5` 运行应用程序，并观察输出与图 5.6 所示。

![](img/d08df1b94a49a49b95ebbdc5e982bda6_140_0.png)

### 图 5.6

使用抽象类的结果。

### 接口操作 (Working with Interfaces)

由于 C# 不允许继承自多个基类，你需要仔细选择那个基类。幸运的是，C# 提供了另一种允许多重继承的替代方案。接口定义了一组公共特征和行为（以公共属性和方法的形式），所有派生类都保证实现这些内容。将接口视为一种部分类型定义或类型描述。

与抽象类一样，接口不能被直接实例化，它可以包含方法、属性和事件。接口不能包含字段、构造函数或析构函数。

注意

## 接口不是合约 (Interfaces Are Not Contracts)

通常说接口定义了任何派生类必须实现的合约。这仅在以下意义是正确的：即继承的接口定义了保证在派生类上可用的方法签名和属性。

你完全没有对特定的实现提供任何保证。完全可以在不提供任何有用实现的情况下满足接口。接口仅仅要求任何继承它的类具有特定的属性和方法。

你声明接口的方式与声明类相同，只需将关键字替换为 `class` 关键字即可。接口可以是 `internal`、`public`、`protected` 或 `private`；但是，如果你不显式指定访问权限，接口将默认为 `internal` 访问权限。所有接口成员自动为 `public` 不能指定访问修饰符。由于接口成员也是抽象的，它们不能提供实现。

当一个类继承接口时（称为接口继承或接口实现），它只继承成员名称和签名，因为接口不提供实现。这意味着派生类必须为该接口定义的所有成员提供实现。要继承接口，你提供接口的名称，就像你继承一个类一样。你只需通过提供一个用逗号分隔的接口名称列表，就可以继承多个接口。

注意

## 同时继承基类和接口 (Inheriting Both a Base Class and Interfaces)

C# 使用位置表示法来指示继承列表中的基类和接口。如果一个类同时继承一个基类和一个或多个接口，则基类总是列在前面。

你也可以“混合组合”继承，这意味着你可以只继承一个基类、只继承一个或多个接口，或者同时继承一个基类和一个或多个接口。如果基类继承自接口，任何派生自该基类的类都会继承该实现。

虽然接口不能继承自类，但它们可以继承其他接口。接口继承仅意味着为了满足一个接口，你还必须满足其他接口。这允许你创建高度特化的接口，然后聚合这些接口以形成一个更大的接口。当你有多个不相关的类需要实现类似的功能（例如将数据保存到 ZIP 文件）时，这特别有用。与此相关的行为可以通过接口定义，然后可以作为定义你的业务对象的其他接口的一部分。

### 提示 (TIP)

## 接口与扩展方法 (Interfaces and Extension Methods)

在接口上下文中，扩展方法变得更加强大，因为你可以扩展接口。这样做允许实现该接口的所有类型获得该扩展方法。事实上，泛型集合的语言集成查询（LINQ）功能就是这种实现的。

当接口继承另一个接口时，派生接口仅定义继承接口的新成员；当一个类实现此聚合接口时，它必须为所有定义的成员提供实现。

当接口与抽象类结合使用时，真正发挥了接口的力量和灵活性。由于接口方法是隐式抽象的，抽象类不需要为接口成员提供实现。相反，它可以为接口成员提供它自己的抽象成员。在这种情况下，任何派生类必须重写它并提供实现。

查看列表 5.1 中的车辆层级结构，如果想引入紧急车辆的概念（如消防车、警车和警察摩托车）会怎样？你可以引入一个新类，名为 `EmergencyVehicle`，但并不完全清楚它在现有层级结构中的位置，因为它需要成为与 `FourWheeledVehicle` 和 `TwoWheeledVehicle` 同级别的基类，并且任何具体类都想要继承 `EmergencyVehicle` 和 `Truck` 或 `Motorcycle`。你已经知道这种多重继承是不可能的，但如果改用接口，情况会有什么变化？

## 124 小时第 5 节：继承、接口与抽象类

### 动手尝试

### 接口操作

这些步骤探索了如何同时使用接口和基类来创建灵活的类层次结构。如果你关闭了 Visual Studio，请先重复上一个练习。

1. 创建一个名为 `IVehicle` 的新接口，定义一个名为 `Operate` 的方法，并修改 `Vehicle` 类使其继承它。`IVehicle.Oper` 方法的签名应与 `Vehicle.Oper` 方法相同。
2. 创建一个名为 `EmergencyVehicle` 的新接口，它继承自 `IVehicle` 并提供一个无参数的 void 方法 `SoundSiren`。
3. 创建名为 `PoliceCar`、`PoliceMotorcycle` 和 `FireTruck` 的新类，它们派生自相应的基类并实现 `EmergencyVehicle` 接口。对于 `SoundSiren` 的实现，只需向控制台打印消息即可。
4. 在 `Program.cs` 文件的 `Main` 方法中，将现有代码替换为：

   a. 创建 `Car` 的新实例并赋值给变量 `car`，然后调用 `Operate` 方法。
   b. 将 `PoliceCar` 的新实例赋值给 `car` 并调用 `Operate` 方法。
   c. 创建一个名为 `policeCar` 的 `PoliceCar` 新实例并将 `car` 赋值给它。你需要将 `car` 转换为 `PoliceCar` 类型。
   d. 在 `policeCar` 上调用 `SoundSiren`。
5. 使用 `Ctrl+F5` 运行应用程序，观察输出是否与图 5.7 所示。
