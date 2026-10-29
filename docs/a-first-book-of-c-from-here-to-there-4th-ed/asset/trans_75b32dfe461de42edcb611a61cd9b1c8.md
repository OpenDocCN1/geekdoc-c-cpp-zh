

// 类声明部分
class RoomType
{
    private:
        double length; // 将 length 声明为 double 类型变量
        double width;  // 将 width 声明为 double 类型变量
    public:
        RoomType(double = 0.0, double = 0.0); // 构造函数
        void showRoomValues();  // 访问器方法
        void setNewRoomValues(); // 修改器方法
        double calculateRoomArea(); // 计算方法
};

这段代码声明了两个数据成员 length 和 width，以及四个类方法。数据成员 length 和 width 存储房间的长度和宽度。作为私有类数据成员，它们只能通过类的成员方法进行访问。这些成员方法用于定义每个 RoomType 对象可用的外部服务。具体来说，RoomType() 方法与其类同名，成为构造函数，在创建 RoomType 类型的对象时自动调用。你可以使用此方法初始化房间的长度和宽度值。showRoomValues() 方法被编写为访问器方法，用于显示房间对象的长度和宽度值；setNewRoomValues() 方法被编写为修改器方法，用于更改房间的长度和宽度值；calculateRoomArea() 方法被编写用于计算并显示房间的占地面积。

为了执行这些服务，以下类实现部分是合适的：

```
// 类实现部分
RoomType::RoomType(double l, double w) // 这是一个构造函数
{
    length = l;
    width = w;
    cout << "使用默认构造函数创建了一个新的房间对象。\n\n";
}
void RoomType::showRoomValues()  // 这是一个访问器
{
    cout << "  长度 = " << length
         << "\n   宽度 = " << width << endl;
}
void RoomType::setNewRoomValues(double l, double w) // 这是一个修改器
{
    length = l;
    width = w;
}
double RoomType::calculateRoomArea() // 这是一个计算方法
{
    return (length * width);
}
```

这些方法都很直观。当声明一个房间对象时，除非在声明中提供了特定值，否则它会以长度和宽度为 0 进行初始化。访问器方法显示存储在 length 和 width 中的值，修改器方法允许在房间对象创建后重新赋值。最后，计算方法通过将长度乘以宽度来显示房间的面积。程序 10.5 在一个可运行的程序中包含了这个类。

## 程序 10.5

```
#include <iostream>
using namespace std;

// 类声明部分
class RoomType
{
    private:
        double length; // 将 length 声明为 double 类型变量
        double width;  // 将 width 声明为 double 类型变量

    public:
        RoomType(double = 0.0, double = 0.0); // 构造函数的声明
        void showRoomValues();
        void setNewRoomValues(double, double);
        double calculateRoomArea();
};

// 类实现部分
RoomType::RoomType(double l, double w)  // 这是一个构造函数
{
    length = l;
    width = w;
    cout << "使用默认构造函数创建了一个新的房间对象。\n\n";
}
void RoomType::showRoomValues()  // 这是一个访问器
{
    cout << "  长度 = " << length
         << "\n  宽度 = " << width << endl;
}

void RoomType::setNewRoomValues(double l, double w)  // 这是一个修改器
{
    length = l;
    width = w;
}
```

即使像程序 10.5 这样简单的程序，面向对象编程的基本要求也显而易见。在编写 `main()` 函数之前，必须构建一个有用的类，这是使用对象的程序的典型特征。对于这些程序，设计过程前置了仔细考虑类（其声明和实现）的要求。实现部分中的代码有效地移除了原本属于 `main()` 职责的代码。因此，任何使用该对象的程序都不必在其 `main()` 函数中重复实现细节。相反，`main()` 函数以及由 `main()` 调用的任何函数只关心调用类方法以正确激活它们。对象如何响应消息以及对象的状态如何保留并不在 `main()` 的关注范围内——这些细节隐藏在类构造中。

## 示例 2：构建电梯对象

在此示例中，你将看到如何模拟电梯的运行。所需输出描述了电梯当前所在或经过的楼层。此外，你应提供一个内部电梯按钮，按下该按钮作为移动到另一楼层的请求。电梯通过编号进行标识，例如 1 号电梯（以便在需要时允许投入更多电梯运行），并且它可以在其所处建筑的 1 层到 15 层之间运行。

**解决方案** 对于此应用，所考虑的对象是电梯。三个感兴趣的属性是电梯的编号、当前位置以及它能到达的最高楼层。唯一请求的服务是能够请求改变电梯的位置（其状态）。此外，当新电梯投入使用时，你必须能够建立初始楼层位置。

电梯的位置（对应其当前楼层位置）可以用一个整型成员变量表示，其值介于 1 和它能到达的最高楼层之间。该变量的值（名为 currentFloor）表示电梯的当前状态。改变电梯状态的服务包括：一个构造函数，用于在新电梯投入使用时设置初始楼层位置和最高楼层；以及一个请求方法，用于将电梯的位置（状态）更改为新楼层。将电梯投入使用是通过声明一个类实例（声明一个 Elevator 类型的对象）来完成的，而请求新的楼层位置相当于按下电梯按钮。为了执行这些服务，以下类声明是合适的：

```
// 类声明部分
class Elevator
{
    private:
        int elNum;
        int currentFloor;
        int highestFloor;
    public:
        Elevator(int = 1, int = 1, int = 15);   // 构造函数
        void request(int);
};
```

这段代码声明了三个数据成员（elNum、currentFloor 和 highestFloor）以及两个类方法。第一个数据成员 elNum 用于存储电梯的编号。第二个数据成员 currentFloor 用于存储电梯的当前楼层位置，最后一个数据成员 highestFloor 用于存储电梯能到达的最高楼层。作为私有数据成员，它们只能通过成员方法进行访问。两个声明的公共成员方法 Elevator() 和 request() 用于定义每个 Elevator 对象提供的外部服务。Elevator() 方法与其类同名，成为构造函数方法，在创建 Elevator 类型的对象时自动调用。你可以使用此方法初始化电梯的编号、起始楼层位置和最高楼层。request() 方法用于改变电梯的位置。为了执行这些服务，以下类实现部分是合适的：

```
// 类实现部分
Elevator::Elevator(int idnum, int cfloor, int maxfloor)  // 构造函数
{
    int elNum = idnum;
    currentFloor = cfloor;
    highestFloor = maxfloor;
}

void Elevator::request(int newfloor)  // 访问器
{
    if (newfloor < 1||newfloor > highestFloor||newfloor == currentFloor)
        ; // 不执行任何操作
    else if (newfloor > currentFloor)  // 电梯向上移动
    {
        cout << "\n从 " << currentFloor << " 层开始" << endl;
        while (newfloor > currentFloor)
        {
            currentFloor++;  // 当前楼层加一
            cout << " 正在上行 - 现在位于 " << currentFloor << " 层" << endl;
        }
        cout << "在 " << currentFloor << " 层停止" << endl;
    }
    else // 电梯向下移动
    {
        cout << "\n从 " << currentFloor << " 层开始" << endl;
        while (newfloor < currentFloor)
        {
            currentFloor--;  // 当前楼层减一
            cout << " 正在下行 - 现在位于 " << currentFloor << " 层" << endl;
        }
        cout << "在 " << currentFloor << " 层停止" << endl;
    }

    return;
}
```

