
## 第二部

### 第6章：使用设计模式构建

```cpp
void AirConditioner::TurnOn()
{
    ChangedBy = 100 - Level;
    Level = 100;
    Changed();
}

void AirConditioner::TurnOff()
{
    ChangedBy = 0 - Level;
    Level = 0;
    Changed();
}

void AirConditioner::SetLevel(int newLevel)
{
    Level = newLevel;
    ChangedBy = newLevel - Level;
    Changed();
}

void Road::ClimbDescend(int angle)
{
    ClimbAngle = angle;
    Changed();
}

void Road::Bump(int height, int which)
{
    BumpHeight = height;
    BumpWhichTire = which;
    Changed();
}
```

现在，在清单 6-5 中，你可以看到中介者（mediator）源代码以及 CarControls 类的源代码。

### 魔法词：高内聚、低耦合

在软件工程领域，两个流行术语是内聚和耦合。

*内聚*指的是将职责相似的函数组合在一起的过程。如果你创建了良好的类，这应该不成问题。涉及车轮的函数应该放在 Wheels 类中——而不是，例如，Engine 类中。

*耦合*则稍微复杂一些。它指的是将类绑定在一起，使它们无法独立运作的过程。实际上，这些类被耦合了。在良好的面向对象编程中，大量耦合并不好。

你希望你的类尽可能独立；你希望*低耦合*。中介者模式对实现低耦合目标有很大帮助。在 CarParts 示例中，如果我们改为让 Electric 类持有指向 Engine 实例和 Radio 实例等的指针，我们就会迫使所有这些类独立工作。实际上，我们就会把它们耦合起来。但通过使用 Mediator 实例，每个类只与 Mediator 交互。我们实现了低耦合。因此，你应该努力设计*高内聚*和*低耦合*。这是好事！

### 清单 6-5：使用 carparts.cpp 文件

```cpp
#include <iostream>
#include "mediator.h"
#include "carparts.h"

using namespace std;

Mediator::Mediator()
{
    MyEngine = new Engine(this);
    MyElectric = new Electric(this);
    MyRadio = new Radio(this);
    MyWheels = new Wheels(this);
    MyBrakes = new Brakes(this);
    MyHeadlights = new Headlights(this);
    MyAirConditioner = new AirConditioner(this);
    MyRoad = new Road(this);
}

void Mediator::PartChanged(CarPart *part)
{
    if (part == MyEngine)
    {
        if (MyEngine->RPM == 0)
        {
            MyWheels->Speed = 0;
            return;
        }

        if (MyEngine->Revamount == 0)
        {
            return;
        }

        // If engine increases, increase the electric output
        MyElectric->ChangeOutputBy
            (MyEngine->Revamount / 10);

        if (MyEngine->Revamount > 0)
        {
            MyWheels->Accelerate(
                MyEngine->Revamount / 50);
        }
    }
    else if (part == MyElectric)
    {
        // Dim or brighten the headlights
        if (MyHeadlights->Brightness > 0)
            MyHeadlights->Adjust(MyElectric->ChangedBy / 20);

        if (MyRadio->Volume > 0)
            MyRadio->AdjustVolume(MyElectric->ChangedBy / 30);
    }
    else if (part == MyBrakes)
    {
        MyWheels->Decelerate(MyBrakes->Pressure / 5);
    }
}
```

### 清单 6-5（续）

```cpp
void CarControls::TurnOnHeadlights()
{
    MyHeadlights->TurnOn();
}

void CarControls::TurnOffHeadlights()
{
    MyHeadlights->TurnOff();
}

void CarControls::ClimbHill(int angle)
{
    MyRoad->ClimbDescend(angle);
}

void CarControls::DescendHill(int angle)
{
    MyRoad->ClimbDescend( 0 - angle );
}

int CarControls::GetSpeed()
{
    return MyWheels->Speed;
}

void CarControls::TurnOnAC()
{
    MyAirConditioner->TurnOn();
}

void CarControls::TurnOffAC()
{
    MyAirConditioner->TurnOff();
}

void CarControls::AdjustAC(int amount)
{
    MyAirConditioner->SetLevel(amount);
}

int main()
{
    // Create a new car.
    Mediator *MyCar = new Mediator();

    // Start the engine.
    MyCar->MyEngine->Start();
    cout << "Engine Started!" << endl;

    // Accelerate.
    MyCar->MyWheels->Accelerate(20);
    cout << "The car is going: " << MyCar->MyWheels->GetSpeed() << endl;

    // Apply the brakes.
    MyCar->MyBrakes->Apply(20);
    cout << "Applying the brakes." << endl;
    cout << "The car is going: " << MyCar->MyWheels->GetSpeed() << endl;

    // Stop the car.
    MyCar->MyBrakes->Apply(80);
    cout << "Applying the brakes." << endl;
    cout << "The car is going: " << MyCar->MyWheels->GetSpeed() << endl;

    // Shut off the engine.
    MyCar->MyEngine->Stop();
    cout << "Engine Stopped" << endl;

    return 0;
}
```

CarControls 部分运行起来有点长，但它很方便，因为它提供了一个中央接口，通过它你可以操作汽车。不过，这个模式的主力位于 Mediator 类中。它是一组 if 语句，检查发生的更改，然后调用其他类来修改其他类的对象。这就是中介者模式的全部目标：它有一个 Mediator 类，其中包含一个通用函数，该函数查找更改，然后更改其他类。

如果你回看清单 6-4，可以看到在每次更改之后，我们都会调用 Changed() 函数。这个函数位于基类中，它会调用 Mediator 的 PartChanged() 函数，后者完成所有繁重的工作。另请注意，在某些汽车部件类中，Mediator 不会响应它们的更改（例如 Wheel 类）；然而，我们仍然在该类的成员函数中调用 Changed()。原因是我们可能会添加功能，让 Mediator 响应这些更改。这样我们就不必检查是否包含了 Changed() 方法；它已经在那里了。这有助于避免这样的问题：当代码忘记调用 Changed() 时，人们会纳闷为什么 Mediator 没有做它应该做的事。

### 为你的工作编写文档

设想其他人将使用你这套汽车类。你已经将头文件和源文件，以及包含编译后代码的静态库，保存在网络驱动器上。你的同事开始查看你的头文件，看到一大堆类。那个人知道如何使用这些类吗？这位同事知道要使用名为 CarControls 的主外观（Facade）类吗？还是那个人不得不埋头钻研代码，弄清楚该用哪些类、不该用哪些类？

答案是否定的。相反，要清楚地记录你的类。在某个地方整理一份简单的文档（不超过一两页），说明如何使用你的类库。请为其他程序员编写这份文档，并让它可读！并明确说明程序员应通过 CarControls 类与系统交互。然后，你应该描述 CarControls 类的公有成员函数（接口），并提供具体示例。你还可以为想要理解整体运作方式的高级程序员加入一个参考部分。无论你做什么，都不要只是把类交出去，却期望别人在没有足够文档的情况下理解它们！

## 第三部

### 修复问题

![](img/6ba99460b0feb3585671a4612ff5fabb_390_0.png)

![](img/6ba99460b0feb3585671a4612ff5fabb_390_1.png)

你可以在 http://www.dummies.com/extras/cplusplusa.io 找到一个分步幻灯片，演示如何附加到现有进程。在某些情况下，调试应用程序时你会附加到进程，因为你需要立即查看应用程序在没有调试器介入时如何工作。许多读者写信告诉我们，这类幻灯片让他们的工作轻松了很多。尽管该幻灯片依赖 Windows，但该过程在 Mac 和 Linux 系统上类似。

### 内容速览

-   第1章：处理缺陷 ..............................................................375
    -   这不是缺陷，这是特性！ ...............................................................375
    -   让你的应用程序特性看起来像特性 ........................................377
    -   预见（几乎）一切 ................................................................378
    -   避免错误，简单明了 ..............................................................385
-   第2章：调试应用程序 .......................................................387
    -   使用调试器编程 ................................................................387
    -   使用不同工具调试 .................................................................397
    -   使用命令行参数调试 Code::Blocks 应用程序 ............398
-   第3章：停止并检查你的代码 ...........................................399
    -   设置和禁用断点 .............................................................400
    -   监视、检查和核对变量 ...............................................404
-   第4章：在栈中漫游 ........................................................411
    -   将数据入栈 .................................................................................411
    -   使用高级功能调试 ...............................................................416
