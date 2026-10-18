

Truck 类应包含一个字段，用于记录卡车行驶的公里数。Plane 类应包含一个字段，用于记录飞机飞行的小时数。Truck 和 Plane 类都应具有构造函数，用于设置各个字段，包括其最大容量（提示：将最大容量存储为 FreightContainer 类中的 protected 字段）。编写一个方法，将 FreightContainer 对象添加到 TransportVehicle 类中。此方法应检查添加的容器是否超过车辆的容量。如果超过，则不应添加，并应返回 false。否则，应添加容器并返回 true。编写一个简单的驱动程序来测试你的类。

2. 创建一个驱动程序，其中包含指向 TransportVehicle 对象的指针向量。创建一个函数，打印出每个 TransportVehicle 对象的注册号和年龄，以及当前使用的总容量的百分比。在函数结束时，打印车队的整体容量和当前使用量。提示：根据需要向 TransportVehicle 类添加适当的方法。

3. 下面列出了使用继承定义的两个类的定义、其实现代码以及一个 main 函数。将代码放入适当的文件中，并加上必要的 include 语句和预处理器语句，以便程序编译并运行。它应输出“Circle has radius 2 and area 12.5664”。

```
class Shape
{
public:
    Shape();
    Shape(string name);
    string getName();
    void setName(string newName);
    virtual double getArea() = 0;
private:
    string name;
};
Shape::Shape()
{
    name="";
}
Shape::Shape(string name)
{
    this->name = name;
}
```

```
}
string Shape::getName()
{
    return this->name;
}
void Shape::setName(string newName)
{
    this->name = newName;
}
class Circle : public Shape
{
public:
    Circle();
    Circle(int theRadius);
    void setRadius(int newRadius);
    double getRadius();
    virtual double getArea();
private:
    int radius;
};
Circle::Circle() : Shape("Circle"), radius(0)
{ }
Circle::Circle(int theRadius) : Shape("Circle"),
    radius(theRadius)
{ }
void Circle::setRadius(int newRadius)
{
    this->radius = newRadius;
}
double Circle::getRadius()
{
    return radius;
}
double Circle::getArea()
{
    return 3.14159 * radius * radius;
}
int main()
{
    Circle c(2);
    cout << c.getName() << " has radius " <<
        c.getRadius() << " and area " <<
        c.getArea() << endl;
    return 0;
}
```

添加另一个类 Rectangle，它也派生自 Shape 类。适当修改 Rectangle 类，使其具有私有 width 和 height 变量、允许用户设置 width 和 height 的构造函数、检索 width 和 height 的函数，以及适当定义的 getArea 函数，用于计算矩形的面积。

将以下代码添加到 main 中应输出 "Rectangle has width 3 has height 4 and area 12.0"。

```
Rectangle r(3,4);
cout << r.getName() << " has width " <<
    r.getWidth() << " has height " <<
    r.getHeight() << " and area " <<
    r.getArea() << endl;
```

## PROGRAMMING PROJECTS

编程项目比练习程序需要更多的解决问题能力，并且通常可以用多种不同的方式解决。访问 www.myprogramminglab.com 在线完成这些编程项目并获得即时反馈。

- 1. 给出一个名为 Doctor 的类的定义，其对象是诊所医生的记录。此类将是 SalariedEmployee 类的派生类，该类在 Display 15.5 中给出。Doctor 记录具有医生的专业（例如 "Pediatrician," "Obstetrician," "General Practitioner," 等，因此使用类型 string）和门诊费用（使用类型 double）。确保你的类具有合理的构造函数、访问器和变异器成员函数、重载的赋值运算符和拷贝构造函数。编写一个驱动程序来测试所有你的函数。

- 2. 航空公司预订系统存储有关售给乘客的机票的信息。编写一个名为 BasicTicket 的类，存储乘客的姓名、出发城市、到达城市、航班号和票价。编写一个构造函数来设置字段，并包含一个名为 getPrice() 的方法，返回票价。

编写一个名为 PremiumTicket 的派生类，继承 BasicTicket 的所有详细信息，但还存储乘客的座位号。编写一个构造函数，设置所有 BasicTicket 信息和座位号。PremiumTicket 的价格比 BasicTicket 的价格高 10%。编写一个函数，在 PremiumTicket 中重新定义 getPrice() 方法，通过调用 BasicTicket 的 getPrice() 方法并将结果乘以 10% 来返回 PremiumTicket 的价格。

编写一个驱动程序，创建一个 BasicTicket 对象和一个 PremiumTicket 对象，并打印出两者的价格。

3. 编写一个驱动程序，其中包含指向 BasicTicket 对象的指针向量。创建一些 BasicTicket 和 PremiumTicket 对象并将它们添加到向量中。编写一个简单的函数来计算向量中所有机票的费用。手动计算并确保你的函数返回的总和是正确的。如果不正确，请检查是否在 BasicTicket 类中正确使用了 virtual 关键字。

4. 给出两个类的定义，Patient 和 Billing，其对象是诊所的记录。Patient 将派生自 Programming Project 2 中给出的 Person 类。Patient 记录具有患者的姓名（从 Person 类继承）和主治医生，其类型为 Programming Project 2 中定义的 Doctor。Billing 对象将包含一个 Patient 对象、一个 Doctor 对象和一个金额为 double 的应付金额。确保你的类具有合理的构造函数、访问器和变异器成员函数、重载的赋值运算符和拷贝构造函数。首先编写一个驱动程序来测试所有成员函数，然后编写一个测试程序，创建至少两个患者、至少两个医生和至少两条 Billing 记录，然后打印出 Billing 记录的总收入。

5. 考虑一个图形系统，具有各种图形的类——矩形、正方形、三角形、圆形等。例如，矩形可能具有高度、宽度和中心点的成员数据，而正方形和圆形可能只有中心点和边长或半径，分别。在一个设计良好的系统中，这些将派生自一个公共类 Figure。你需要实现这样一个系统。

类 Figure 是基类。你应仅添加派生自 Figure 的 Rectangle 和 Triangle 类。每个类都有 erase 和 draw 成员函数的存根。每个这些成员函数输出一条消息，说明调用了什么函数以及调用对象的类是什么。由于这些只是存根，它们除了输出此消息外什么也不做。成员函数 center 调用 erase 和 draw 函数以擦除并重绘中心处的图形。由于你只有 erase 和 draw 的存根，center 不会做任何“居中”操作，但会调用成员函数 erase 和 draw。还添加一条输出消息到成员函数 center，宣布 center 正在被调用。成员函数不应带参数。

本项目有三个部分：

- a. 编写类定义，不使用虚函数。编译并测试。
- b. 使基类成员函数变为虚函数。编译并测试。
- c. 解释结果的差异。

be virtual. 编写一个 main 程序，创建三个账户（每个类一个）并测试 transfer 函数。

对于类，创建一个名为 `BankAccount` 的基类，具有账户所有者的姓名（字符串）和账户余额（`double`）作为数据成员。包括成员函数 deposit 和 withdraw（每个都带有一个 `double` 的金额作为参数）以及访问器函数 getName 和 getBalance。Deposit 将把金额添加到余额中（假设金额为非负），withdraw 将从余额中减去金额（假设金额为非负且小于或等于余额）。还创建一个名为 `MoneyMarketAccount` 的类，派生自 `BankAccount`。在 `MoneyMarketAccount` 中，用户在给定时间内可获得两次免费取款（不必担心此问题的时间）。在免费取款用完后，每次取款将从余额中扣除 $1.50 的取款费。因此，该类必须具有一个数据成员来跟踪取款次数。它还必须重写 withdraw 定义。最后，创建一个派生自 `BankAccount` 的 `CDAccount` 类（用于建模定期存款），除了具有姓名和余额外，还具有利率。CD 在提前取款时会产生罚款。假设取款（任何金额）会产生相当于账户年利息收入 25% 的罚款。假设取款金额加上罚款从账户余额中扣除。同样，withdraw 函数必须重写基类中的函数。对于所有三个类，withdraw 函数应返回一个整数，表示状态（要么 ok，要么资金不足，无法进行取款）。为本次练习的目的，不必担心这些账户的其他功能和属性（例如何时以及如何支付利息）。

+ 8. 无线射频识别 RFID 芯片是可放置在产品上的小型标签。它们的行为类似于无线条形码，可以无线广播识别号码给接收器。RFID 芯片的一种应用是用于帮助货物运输的物流。考虑一个装满物品的集装箱。在没有 RFID 芯片的情况下，人类必须手动盘点集装箱内的所有物品以验证内容物。有了附着在集装箱上的 RFID 芯片，RFID 芯片可以电子方式向人类广播集装箱的确切内容，而无需人工干预。

为了模拟此应用，编写一个名为 `ShippingContainer` 的基类，具有作为整数的集装箱 ID 号。包括设置和访问 ID 号的成员函数。添加一个名为 `getManifest` 的虚函数，返回空字符串。此函数的目的是返回集装箱的内容。

