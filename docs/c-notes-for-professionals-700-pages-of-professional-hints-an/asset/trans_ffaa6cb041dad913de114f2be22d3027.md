
```csharp
r = new Random();
}
public int Measure() { return r.Next(-25, 60); }
public void TurnOff() { Console.WriteLine("AmMeter flashes lights saying good bye!"); }
public void TurnOn() { Console.WriteLine("AmMeter turns on..."); }
}
public class OhmMeter : IDevice
{
    private Random r = null;
    public OhmMeter()
    {
        r = new Random();
    }

    public int Measure() { return r.Next(0, 100000); }
    public void TurnOff() { Console.WriteLine("OhmMeter flashes lights saying good bye!"); }
    public void TurnOn() { Console.WriteLine("OhmMeter turns on..."); }
}
public class VoltMeter : IDevice
{
    private Random r = null;
    public VoltMeter()
    {
        r = new Random();
    }

    public int Measure() { return r.Next(-230, 230); }
    public void TurnOff() { Console.WriteLine("VoltMeter flashes lights saying good bye!"); }
    public void TurnOn() { Console.WriteLine("VoltMeter turns on..."); }
}
```

现在我们需要定义工厂方法。让我们创建包含静态方法的 DeviceFactory 类：

```csharp
public enum Device
{
    AM,
    VOLT,
    OHM
}
public class DeviceFactory
{
    public static IDevice CreateDevice(Device d)
    {
        switch(d)
        {
            case Device.AM: return new AmMeter();
            case Device.VOLT: return new VoltMeter();
            case Device.OHM: return new OhmMeter();
            default: return new AmMeter();
        }
    }
}
```

太好了！让我们测试我们的代码：

```csharp
public class Program
{
    static void Main(string[] args)
    {
        IDevice device = DeviceFactory.CreateDevice(Device.AM);
        device.TurnOn();
        Console.WriteLine(device.Measure());
        Console.WriteLine(device.Measure());
    }
}
```

```
Console.WriteLine(device.Measure());
Console.WriteLine(device.Measure());
Console.WriteLine(device.Measure());
device.TurnOff();
Console.WriteLine();

device = DeviceFactory.CreateDevice(Device.VOLT);
device.TurnOn();
Console.WriteLine(device.Measure());
Console.WriteLine(device.Measure());
Console.WriteLine(device.Measure());
Console.WriteLine(device.Measure());
Console.WriteLine(device.Measure());
device.TurnOff();
Console.WriteLine();

device = DeviceFactory.CreateDevice(Device.OHM);
device.TurnOn();
Console.WriteLine(device.Measure());
Console.WriteLine(device.Measure());
Console.WriteLine(device.Measure());
Console.WriteLine(device.Measure());
Console.WriteLine(device.Measure());
device.TurnOff();
    Console.WriteLine();
}
}
```

这是运行此代码后您可能会看到的示例输出：

AmMeter turns on...

36

6

33

43

24

AmMeter flashes lights saying good bye!

VoltMeter turns on...

102

-61

85

138

36

VoltMeter flashes lights saying good bye!

OhmMeter turns on...

723828

368536

685412

800266

578595

OhmMeter flashes lights saying good bye!

## 第 134.3 节：抽象工厂模式

提供一个接口用于在不指定其具体类的情况下创建相关或依赖对象的族。

此示例演示了使用不同工厂为计算机游戏创建不同的动物世界。

虽然大陆工厂创建的动物不同，但动物之间的交互保持不变。

```
using System;

namespace GangOfFour.AbstractFactory
{
    /// <summary>
    /// MainApp startup class for Real-World
    /// Abstract Factory Design Pattern.
    /// </summary>
    class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        public static void Main()
        {
            // Create and run the African animal world
            ContinentFactory africa = new AfricaFactory();
            AnimalWorld world = new AnimalWorld(africa);
            world.RunFoodChain();

            // Create and run the American animal world
            ContinentFactory america = new AmericaFactory();
            world = new AnimalWorld(america);
            world.RunFoodChain();

            // Wait for user input
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'AbstractFactory' abstract class
    /// </summary>
    abstract class ContinentFactory
    {
        public abstract Herbivore CreateHerbivore();
        public abstract Carnivore CreateCarnivore();
    }
```

```
/// <summary>
/// The 'ConcreteFactory1' class
/// </summary>
class AfricaFactory : ContinentFactory
{
    public override Herbivore CreateHerbivore()
    {
        return new Wildebeest();
    }
    public override Carnivore CreateCarnivore()
    {
        return new Lion();
    }
}

/// <summary>
/// The 'ConcreteFactory2' class
/// </summary>
class AmericaFactory : ContinentFactory
{
    public override Herbivore CreateHerbivore()
    {
        return new Bison();
    }
    public override Carnivore CreateCarnivore()
    {
        return new Wolf();
    }
}

/// <summary>
/// The 'AbstractProductA' abstract class
/// </summary>
abstract class Herbivore
{
}

/// <summary>
/// The 'AbstractProductB' abstract class
/// </summary>
abstract class Carnivore
{
    public abstract void Eat(Herbivore h);
}

/// <summary>
/// The 'ProductA1' class
/// </summary>
class Wildebeest : Herbivore
{
}

/// <summary>
/// The 'ProductB1' class
/// </summary>
class Lion : Carnivore
{
    public override void Eat(Herbivore h)
    {
        // Eat Wildebeest
        Console.WriteLine(this.GetType().Name +
```

```
  " eats " + h.GetType().Name);
}
}
```

```
/// <summary>
/// The 'ProductA2' class
/// </summary>
class Bison : Herbivore
{
}

/// <summary>
/// The 'ProductB2' class
/// </summary>
class Wolf : Carnivore
{
    public override void Eat(Herbivore h)
    {
        // Eat Bison
        Console.WriteLine(this.GetType().Name +
            " eats " + h.GetType().Name);
    }
}

/// <summary>
/// The 'Client' class
/// </summary>
class AnimalWorld
{
    private Herbivore _herbivore;
    private Carnivore _carnivore;

    // Constructor
    public AnimalWorld(ContinentFactory factory)
    {
        _carnivore = factory.CreateCarnivore();
        _herbivore = factory.CreateHerbivore();
    }

    public void RunFoodChain()
    {
        _carnivore.Eat(_herbivore);
    }
}
```

输出：

Lion eats Wildebeest

Wolf eats Bison

## 第 134.4 节：建造者模式

将复杂对象的构建与其表示分离，以便相同的构建过程可以创建不同的表示，并提供对对象组装的高级控制。

此示例演示了建造者模式，其中不同的车辆以逐步的方式组装。Shop 使用 VehicleBuilders 在一系列顺序步骤中构建各种车辆。

```csharp
using System;
using System.Collections.Generic;

namespace GangOfFour.Builder
{
    /// <summary>
    /// MainApp startup class for Real-World
    /// Builder Design Pattern.
    /// </summary>
    public class MainApp
    {
        /// <summary>
        /// Entry point into console application.
        /// </summary>
        public static void Main()
        {
            VehicleBuilder builder;

            // Create shop with vehicle builders
            Shop shop = new Shop();

            // Construct and display vehicles
            builder = new ScooterBuilder();
            shop.Construct(builder);
            builder.Vehicle.Show();

            builder = new CarBuilder();
            shop.Construct(builder);
            builder.Vehicle.Show();

            builder = new MotorCycleBuilder();
            shop.Construct(builder);
            builder.Vehicle.Show();

            // Wait for user
            Console.ReadKey();
        }
    }

    /// <summary>
    /// The 'Director' class
    /// </summary>
    class Shop
    {
        // Builder uses a complex series of steps
        public void Construct(VehicleBuilder vehicleBuilder)
        {
            vehicleBuilder.BuildFrame();
            vehicleBuilder.BuildEngine();
            vehicleBuilder.BuildWheels();
            vehicleBuilder.BuildDoors();
        }
    }

    /// <summary>
    /// The 'Builder' abstract class
    /// </summary>
    abstract class VehicleBuilder
    {
        protected Vehicle vehicle;
```
