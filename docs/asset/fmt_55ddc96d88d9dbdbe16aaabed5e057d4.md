
## 17.2.1 解释父类和子类之间的“是”（is-a）关系。

## 17.2.2 解释类与类之间的“拥有”（has-a）关系。

## 17.3 虚函数

### 17.3.1 定义纯虚方法。

### 17.3.2 区分何时使用纯虚方法。

### 17.3.3 编写声明纯虚方法的语句。

### 17.3.4 定义抽象类。

### 17.3.5 识别何时使用抽象类。

## 17.1 多态的目的

### 编码时的灵活性 (17.1)

作为一名程序员，除了努力编写能够处理需求变化的代码外，你还应该旨在创建能够处理任何变化的代码。为了提供这种灵活性，编程语言采用了多态（polymorphism）的概念，这个词由前缀 `poly`（多）和 `morph`（形状或形式）组合而成。换句话说，多态指的是一个可以采取多种形式的对象。

简单来说，多态意味着父类的对象可以被用作其任何后代类。例如，如果你在为汽车经销商编写程序，你正在创建一个帮助业主管理各种机动车辆的系统，如图 17 所示的类层次结构。

经销商中的所有对象都继承自 `MotorVehicle` 类。通过多态，如果你定义了一个以 `MotorVehicle` 为参数的方法，那么该方法就可以接收任何对象作为参数，只要它是派生自 `MotorVehicle` 即可。`Motorcycle`（摩托车）、`Car`（汽车）、`Truck`（卡车）、`GasCar`、`HybridCar` 和 `ElectricCar`（电动汽车）都可以用于任何指定 `MotorVehicle` 为参数的方法。

## 使用 C++ 编程

![](img/7921c83706ea2c639325e413353f7951_329_0.png)

图 17 `MotorVehicle` 继承层次结构

代码中的 `add_vehicle()` 方法向经销商的库存添加车辆。如果 `add_vehicle()` 方法接受 `MotorVehicle` 作为输入，无论添加的是 `MotorVehicle` 的哪个子类，代码都能运行。

```
public void Dealership:add_vehicle(MotorVehicle motor_vehicle) throws Out_of_Range_Exception
```

```
if (num_vehicles + 1 <= capacity) then
    inventory[num_vehicles] = motor_vehicle
    num_vehicles = num_vehicles + 1
else
    throw Out_of_Range_Exception
```

此代码将任何 `MotorVehicle`（或 `MotorVehicle` 的子类）作为参数传入 `add_vehicle()` 方法。如果库存中有空间，则添加 `MotorVehicle`。如果没有空间，则抛出 `Out_of_Range_Exception`。通过这样创建 `add_vehicle()` 方法，代码的其他部分都可以向库存中添加 `MotorVehicle`（或 `MotorVehicle` 的任何子类）。

以下代码在 `MotorVehicle` 子类的类中声明了三个车辆对象：`HybridCar`、`Truck` 和 `Motorcycle`。它还使用了：

```
dealership
declare HybridCar
declare Truck
declare Motorcycle
```

# 第 17 节 多态 313

多态允许你以多种方式执行同一个操作。例如，你只需通过向库存中添加六种对象，就可以执行 `add_vehicle()` 行为。向库存中添加新的机动车辆的代码如图14所示。

在 `MotorVehicle.cpp` 中

```cpp
void Dealership::add_vehicle(MotorVehicle vehicle)
{
    if (num_vehicles + 1 <= capacity) // 检查是否有空间
    { // 添加车辆
        inventory[num_vehicles] = vehicle; // 如果有，则增加数量
        num_vehicles++; //
        cout << "Successfully added a new vehicle to the inventory." << endl;
        cout << "There are now " << num_vehicles << " cars on the lot;" << endl;
        cout << "with " << capacity - num_vehicles << " spaces left." << endl;
    }
    else
    {
        throw runtime_error("lot_full"); // 抛出运行时错误
    } // 如果停车场已满
    return;
}
```

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    Dealership zoesZippyCar; // 创建一个 Dealership 变量
    // 用于初始化 zoesZippyCar 成员变量的代码

    GasCar corolla;
    Motorcycle yamaha; // 创建继承自 MotorVehicle 的不同类型的车辆
    Truck gms; //
    ElectricCar tesla;

    // 初始化车辆成员变量的代码
    zoesZippyCar.add_vehicle(corolla);
    zoesZippyCar.add_vehicle(yamaha);
    zoesZippyCar.add_vehicle(gms);
    zoesZippyCar.add_vehicle(tesla);

    return 0;
 // 在上处调用 add_vehicle()（方法）
// 将每辆车辆都添加到 Dealership 的库存中
}
```

输出：

Successfully added a new vehicle to the inventory.

There are now 1 cars on the lot with 49 spaces left.

Successfully added a new vehicle to the inventory.

There are now 2 cars on the lot with 48 spaces left.

Successfully added a new vehicle to the inventory.

There are now 3 cars on the lot with 47 spaces left.

Successfully added a new vehicle to the inventory.

There are now 4 cars on the lot with 46 spaces left.

# 图-14 添加车辆的方法

Copyright 2022 C Learning. 版权所有。您不得以任何形式进行复制、修改、分发或包含。在此电子版本中，某些第三方材料可能来自作者或出版者的删除（第1章）。对本文档进行的编辑更改不会影响学习体验。如果其他权利需要，C Learning 保留随时添加额外内容的权利。

# 314 使用 C++ 编程

通过创建一个 `add_vehicle()` 方法，可以将任何派生自 `MotorVehicle`（包括 `MotorVehicle` 本）的对象添加到库存，你正在使用多态。代码的 `main()` 部分创建了一个 `Dealership` 变量并创建了继承自 `MotorVehicle` 的车辆。在初始化每个对象的成员变量后，你可以使用 `add_vehicle()` 方法将它们添加到 `zoes_zippy_cars` 的库存中。输出显示该行为执行成功。

### 动态绑定的原理 (17.1.2, 17.1.3, 17.1.4)

计算机如何知道足够的信息来执行此类灵活的代码？编译器如何知道在多态中应该使用哪个变量或方法？动态绑定隐藏了继承体系中相关类之间的差异，以便它们可以互换使用。

回想，方法重写（method overriding）允许类对其已从其一个祖先继承的方法提供它自己的实现。将方法连接到类的主体是在程序运行时完成的，而多态具有动态绑定。

在此例中，多态意味着变量的方法调用会执行到不同的方法，这取决于调用该方法的变量类型。在动态绑定中，任何对象所属的精确类是在代码运行时决定的。这样做的好处是计算机可以决定执行最合适的方法实现，而不需要局限于特定的对象类型，从而增强代码的灵活性。

# 17.2 多态基础 (17.2.1, 17.2.2)

## 类中的类

类之间可以建立不同的关系来解决问题。继承使得“是一个...（is-a）”关系成为可能。“是一个...”关系发生在父类和子类之间，其中一个类是另一个类的子类。在 `Dealership` 中，`MotorVehicle` 类与 `Car`、`GasCar`、`HybridCar`、`ElectricCar`、`Truck` 和 `Van`（子类）之间存在关系。在“是一个...”的关系中，你可以将子类视为父类。

第二种关系被称为“有一个...（has-relationship）”关系，其中一个类是另一个类的成员变量。组合（Composition）使得“有一个...”关系成为可能。仅仅一个类包含另一个类，并不意味着它继承了所包含类的功能。例如，`Dealership` 包含一个 `MotorVehicle` 数组。`Dealership` 包含 `MotorVehicle`。这是一个“有一个...”的关系，因为 `Dealership` 不是 `MotorVehicle`，它也没有继承 `MotorVehicle` 类的能力。“是一个...”关系和“有一个...”关系区别的示例如图 17-5 所示。

![](img/7921c83706ea2c639325e413353f7951_333)

Copyright 2022 C Learning. 版权所有。您不得以任何形式进行复制、修改、分发或包含。在此电子版本中，某些第三方材料可能来自作者或出版者的删除（第1章）。对本文档进行的编辑更改不会影响学习体验。如果其他权利需要，C Learning 保留随时添加额外内容的权利。

### 对象对象 (17.2.3)

有时你使用对象来代表另一种类型。例如，你可以将 `Truck` 对象传递给任何接收 `MotorVehicle` 的方法。转换有两种：隐式转换和显式转换。以下是隐式转换的示例。假设 `Truck` 已经继承自 `MotorVehicle`。隐式转换允许以下代码：

```cpp
declare mv as MotorVehicle
declare t as Truck
```

此示例声明了一个 `MotorVehicle` 对象和一个 `Truck` 对象。当一种类型的对象赋值给另一种类型的对象时，发生了隐式转换，发生在赋值语句中。隐式转换要求你为子类实现拷贝构造函数或重载 `=` 方法。

在强类型编程语言（如 C++、Java 和 Python）中，每个变量必须声明数据类型。如果变量与表达式或参数中的预期类型不匹配，将发生错误。例如，如果代码使用了 Truck 对象，但作为 MotorVehicle 传递，将会发生错误，因为 Truck 是 MotorVehicle，但 MotorVehicle 不是 Truck。由于这些语言是强类型的，从一种类型转换为另一种类型需要显式转换，如下代码所示：

```cpp
mv = (MotorVehicle) t
```

`Truck` 被显式转换为基类对象——显式是因为语句特地指定了变量 `t` 所属的类（`MotorVehicle`）。这种类型的转换是向上转换，因为你正在转换为类层次结构中更高的对象，就像 `Truck` 向上转换为 `MotorVehicle` 一样。

你也可以反转转换并将代码改为：

```cpp
t = (Truck) mv
```

这是一个向下转换的示例，因为你正在将一个对象转换为类层次结构中较低的另一个对象——`MotorVehicle` 转换为 `Truck`。

# 向下转换可能的问题是什么？

假设 `MotorVehicle` 类没有与 `Truck` 完全相同的成员变量。例如，`Truck` 可能有两个额外的成员变量来指定货床的长度和宽度。在这种情况下，向下转换会产生错误，这就是它危险的原因。

## 17.3 虚函数

### 预见定制化 (17.3.1, 17.3.2, 17.3.3)

如果你查看了经销商商店的代码，你可能会发现并没有所谓的“通用汽车（generic Car）”。汽车不应该实现某些方法，因为它的行为取决于正在使用的是哪种类型的汽车。例如，假设 `Car` 类实现了一个名为 `calculate_fuel_cost()` 的方法，该方法返回行驶给定数英里所需的估计费用。

这种价格计算取决于 `Car` 是汽油汽车（`GasCar`）、混合动力汽车（`HybridCar`）还是电动汽车（`ElectricCar`）。`GasCar` 根据汽车的平均燃油效率（MPG）计算价格，`HybridCar` 使用汽车的燃油效率和估计的电池使用量计算价格，而 `ElectricCar` 则根据行驶该距离所需的电计算价格。见图 17-6。

![](img/7921c83706ea2c639325e413353f7951_335_0.png)

由于 `Car` 并不是一种特定的车辆类型，因此要求每种 `Car` 说明它将如何实现 `calculate_fuel_cost()` 是合理的。你可以使用纯虚方法（pure virtual method）来指定派生类将定义继承自基类的方法。

纯虚方法不在基类中定义，因为任何派生自基类的类都必须定义它们自己的方法版本。`Car` 没有定义 `calculate_fuel_cost()` 的行为。相反，任何派生自 `Car` 的对象（`GasCar`、`HybridCar` 或 `ElectricCar`）都会创建该方法的自己的实现。

在方法定义中使用 `void` 关键字来表示该方法的实现。基类声明中该方法的伪代码如下：

```cpp
public virtual void Car::calculate_fuel_cost() = 0
```

你定义纯虚方法的方式与定义任何其他方法相同。纯虚方法没有实现，因此不能在基类中被调用。相反，纯虚方法必须在方法声明的末尾使用 `=` 语法进行定义，以表示它没有在基类中定义。如果一个类没有实现该方法，代码将无法编译。定义和使用纯虚方法的方法见图 17-7。

`Car` 类继承自 `MotorVehicle` 类

```cpp
class Car : public MotorVehicle {
  public:
    virtual double calculate_fuel_cost(int miles) = 0;
    string fuel_type;
}
```

`= 0` 语法意味着该方法在 `Car` 类中没有定义，而 `Car` 是 `GasCar`、`HybridCar` 和 `ElectricCar` 类的基类。

```cpp
class GasCar : public Car {
  public:
    double calculate_fuel_cost(int miles);
    int fuel_level;
}
```

```cpp
class HybridCar : public Car {
  public:
    double calculate_fuel_cost(int miles);
    int fuel_level;
    int battery_percentage;
}
```

`Car` 的每个子类都创建它们自己的 `calculate_fuel_cost()` 方法实现

```cpp
class ElectricCar : public Car {
  public:
    double calculate_fuel_cost(int miles);
    int battery_percentage;
}
```

图 17-7 纯虚方法

### 抽象类 (17.3.4, 17.3.5)

当你创建一个虚方法时，你也就创建了一个抽象类（abstract class），即具有一个或多个虚方法的类。如果一个类拥有虚方法，它就无法被实例化，因此你不能创建一个 `Car` 类型的变量。经销商商店中代表 `Car` 的必须是 `GasCar`、`HybridCar` 或 `ElectricCar`。抽象类通常用于表示类层次结构中的通用概念（例如 `Car`），而不是某个特定的对象（例如 `HybridCar`）。

根据经验法则，如果你有紧密相关的类需要实现同一方法的多个版本（如各种类型的汽车），就应该使用抽象类。如果你想使用继承但又不想创建一个与基类相同类型的对象，那么抽象类是一个很好的编程选择。抽象类表示一种抽象的想法，在程序的上下文中，对其进行实例化是没有意义的。例如，`Car` 是一个抽象概念，它必须定义为 `GasCar`、`HybridCar` 或 `ElectricCar` 在程序中才有意义。对于通用汽车，`MotorVehicle` 类会是抽象类的良好候选者吗？

从表面上看，`MotorVehicle` 是一个通用概念，你不会预见到它的对象。然而，经销商商店有一个 `MotorVehicle` 数组，这被算作 `MotorVehicle` 类的实例化。将 `MotorVehicle` 变为抽象类会破坏这部分代码。此外，你将 `MotorVehicle` 对象传递给许多方法，将 `MotorVehicle` 对象作为参数会引发错误。

## 总结

- 多态（Polymorphism）是面向对象编程中的一个概念，对象可以许多类型。继承是多态的主要驱动力，派生自另一个类的类可以被视为基类。

- 多态意味着父类对象可以用于引用它的任何后代。继承和多态有助于避免相关对象之间的重复代码。
