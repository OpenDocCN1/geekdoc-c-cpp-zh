
# 第9章

## 类与多态项目

- 4. 请查看以下关于问题领域的描述：
银行向客户提供以下类型的账户：储蓄账户、支票账户和货币市场账户。客户允许向账户存款（从而增加其余额）、从账户中取款（减少其余额）以及赚取利息。每个账户都有一个利率。
假设你正在编写一个程序，用于计算银行账户赚取的利息。
a. 识别问题领域中潜在的类。
b. 精炼列表，只包含此问题所需的类或多个类。
c. 识别该类或这些类的职责。

## 编程题

- 1. `Pet`（宠物）类

创建一个名为 `Pet` 的类（类似于本章讨论的类），它具有以下属性：
* `Name`（名称）—`Name` 属性持有宠物的名字。
* `Type`（类型）—`Type` 属性持有宠物的动物类型。示例值为“Dog”、“Cat”和“Bird”。
* `Age`（年龄）—`Age` 属性持有宠物的年龄。

在一个应用程序中演示该类，该程序创建该类的对象，并允许用户输入其宠物的名称、类型和年龄。这些数据应存储在对象中。检索宠物的 `Name`、`Type` 和 `Age` 属性并将其值显示在屏幕上。

- 2. `Car`（汽车）类

创建一个名为 `Car` 的类，它具有以下属性：
* `Year`（年份）—`Year` 属性持有汽车的型号年份。
* `Make`（品牌）—`Make` 属性持有汽车的品牌。
* `Speed`（速度）—`Speed` 属性持有汽车的当前速度。
此外，该类还应具有以下构造函数和其他方法。

* `Constructor`（构造函数）—构造函数接受汽车的年份和型号作为参数。这些值应赋值给汽车 `Year` 和 `Make` 属性的备用字段。构造函数还应将 `Speed` 属性的备用字段赋值为 0。
* `Accelerate`（加速）—`Accelerate` 方法每次调用时都应在 `Speed` 属性的备用字段上加 5。
* `Brake`（刹车）—`Brake` 方法每次调用时都应从 `Speed` 属性的备用字段中减 5。

在一个应用程序中演示该类，程序包含一个 `Accelerate` 按钮，每次点击时都会调用 `Accelerate` 方法，然后显示汽车的当前速度。应用程序的表单还应该有一个 `Brake` 按钮，每次点击时都会调用 `Brake` 方法，然后显示汽车的当前速度。

- 3. Personal Information（个人信息）类

创建一个持有以下个人数据的类：姓名、地址、年龄和电话号码。在一个应用程序中演示该类，该程序创建该类的三个实例。一个实例应持有你的信息，另外两个应持有你朋友家人的信息。在应用程序的表单上显示每个对象的属性。

![](img/8a88e1d8c69a687988c05f162ce32cac_606_0.png)

- 4. `Employee`（员工）类

编写一个 `Employee` 类，具有以下属性：
- `Name`（姓名）—属性持有员工姓名。
- `IdNumber`（编号）—属性持有员工的 ID号。
- `Department`（部门）—属性持有员工工作的部门名称。
- `Position`（职位）—属性持有员工的职位名称。

- 该类应具有以下重载构造函数：
- 一个接受以下值作为参数并将其赋值给相应属性的构造函数：员工姓名、员工编号、部门和职位。
- 一个接受以下值作为参数并将其赋值给相应属性的构造函数：员工姓名和编号。`Department` 和 `Position` 属性应被赋值为空字符串 (`""`)。
- 一个无参数构造函数，将 `Name`、`Department` 和 `Position` 赋值为空字符串 (`""`)，并将 `IdNumber` 属性赋值为 0。

在应用程序中，创建三个 `Employee` 对象来持有以下数据：

| Name (姓名) | ID Number (编号) | Department (部门) | Position (职位) |
|---|---|---|---|
| Susan Meyers | 47899 | Accounting | 副总裁 |
| Mark Jones | 39119 | IT | 程序员 |
| Joy Rogers | 81774 | Manufacturing | 工程师 |

应用程序应将这些数据存储在三个对象中，并在屏幕上显示每个员工的数据。

- 5. `RetailItem`（零售商品）类

编写一个 编写一个 `RetailItem` 类，持有有关零售商店中商品的数据。该类应具有以下属性：
- `Description`（描述）—属性应持有该商品的简要描述。
- `UnitsOnHand`（库存数量）—`UnitsOnHand` 属性应持有当前库存的单位数量。
- `Price`（价格）—属性应持有商品的价格。

编写一个接受属性参数的构造函数。应用程序应创建一个包含三个 `RetailItem` 对象的数组，包含以下数据：

| Description (描述) | Units on Hand (库存数量) | Price (价格) |
|---|---|---|
| Item 1 | 外夹 | 12 | 59.95 |
| Item 2 | 牛仔裤 | 40 | 34.95 |
| Item 3 | 衬衫 | 20 | 24.95 |

应用程序应该有一个循环来遍历数组，显示每个元素的属性。

- 6. Dorm and Meal Calculator（宿舍与餐食计算器）

某大学有以下宿舍：

| Name (名称) | Cost (费用) |
|---|---|
| Allen Hall | 每学 $500 |
| Pike Hall | 每学 $600 |
| Farthing Hall | 每学 $800 |
| University Suites | 每学 $2500 |

该大学还提供以下餐计划：

| Plan (计划) | Cost (费用) |
|---|---|
| 每周7餐 | 每学 $600 |
| 每周14餐 | 每学 $1200 |
| 无限餐 | 每学 $700 |

创建一个具有两个表单的应用程序。主表单允许选择宿舍和餐计划。第二个表单应显示 `AddressEntry` 的姓名、地址和电话号码。

- 7. Address Book（电话簿）

创建一个名为 `AddressEntry` 类。`AddressEntry` 类应持有姓名、地址和电话号码。在一个应用程序中演示该类，该程序创建多个 `AddressEntry` 实例。在应用程序的表单上显示每个对象的属性。

# 继承与多态

## TOPICS (主题)
| 10.1 继承 | 10.3 类 |
| 10.2 多态 | |

## 10.1 继承

> 概念：继承允许一个类扩展另一个类。新类继承它所扩展的类的成员。

## 一般化与特化

在现实世界中，你可以发现许多其他对象的特化版本。例如，“昆虫” 描述了一个非常通用的类型，具有许多特征。由于蚂蚱和蜜蜂是昆虫，它们拥有通用的特征。如图 10-1 所示。

## 继承与“是……”关系

当对象之间存在“是……” 关系时，意味着特化对象具有通用对象的所有特征，再加上使其特殊的额外特征。在面向对象的编程中，继承用于创建类之间的“是……”关系。这里是一些“是……” 关系的例子：
* 贵宾是狗。
* 汽车是车辆。
* 花是植物。
* 矩形是形状。
* 足球运动员是运动员。

继承涉及一个基类和一个派生类。**基类**是通用类，**派生类**是特化类。你可以将派生类类为基类的扩展版本。派生类继承基类的字段、属性和方法，而无需重写。可以在派生类中添加新的字段、属性和方法，这就是它成为基类特化版本的原因。

> 注意：基类有时被称为超类（superclass），派生类有时被称为子类（subclass）。这两组术语都是正确的。为了保持一致，本文使用“基类”（base class）和“派生类”（derived class）术语。

# 第10章 继承与多态

对于 SUV，经销商还保留了以下额外数据：

- 载客人数（Passenger capacity）
- 一个 `Car` 类，包含品牌（make）、年份、里程数、价格和门数（doors）属性
- 一个 `Truck` 类，包含品牌（make）、年份、里程数、价格和驱动类型（drive type）属性
- 一个 `SportUtility` 类，包含品牌（make）、年份、里程数、价格和载客人数的人的属性

然而，这是一种低效的方法，因为这三个类具有许多共同属性。结果是，这些类将包含大量的重复代码。此外，如果我们以后发现需要添加更多共同属性，我们就必须修改所有的类。

更好的方法是编写一个 `Automobile`（汽车）基类来存储所有关于汽车的通用数据，然后为每种特定汽车编写派生类。以下代码显示了

```csharp
class Automobile
{
    // 字段
    private string _make;
    private string _model;
    private int _milage;
    private decimal _price;
    // 构造函数
    public Automobile()
    {
        _make = "";
        _model = "";
        _milage = 0;
        _price = 0;
    }
    // Make 属性
    public string Make
    {
        get { return _make; }
        set { _make = value; }
    }
    // Model 属性
    public string Model
    {
        get { return _model; }
        set { _model = value; }
    }
    // Mileage 属性
    public int Mileage
    {
        get { return _milage; }
        set { _milage = value; }
    }
    // Price 属性
    public decimal Price
{
41     get { return _price; }
42     set { _price = value; }
43 }
44
45
}
```

## 第 10 章 继承与多态

第 4–7 行声明了 `Make`、`Model`、`Mileage` 和 `Price` 属性的备用字段。第 10–16 行的无参数构造函数将 make 和 model 字段赋值为空字符串，并将 mileage 和 price 属性赋值为 0。`Make`、`Model`、`Mileage` 和 `Price` 属性的代码出现在第 19–44 行。

`Automobile` 类是一个完整的类，我们可以从它创建对象。`Automobile` 类只持有关于汽车的通用数据。它不包含经销商想要保留的关于汽车、皮卡车和 SUV 的任何特定数据。为了保存特定类型汽车的数据，我们编写了继承自 `Automobile` 类的类。以下代码显示了派生自 `Automobile` 类的 `Car` 类。

```csharp
1 class Car : Automobile
2 {
3     // 字段
4     private int _doors;
5 
6     // 构造函数
7     public Car()
8     {
9         _doors = 0;
10    }
11 
12    // Doors 属性
13    public int Doors
14    {
15        get { return _doors; }
16        set { _doors = value; }
17    }
18 }
```

查看第 1 行中的类类头：

`class Car : Automobile`

这行代码包含了一些新符号。在类名 `Car` 之后，出现了一个冒号，后面是另一个类名 `Automobile`。这行代码表示我们正在定义一个名为 `Car` 的类，它派生自 `Automobile` 类。`Car` 类是派生类，`Automobile` 类是基类。图 10-2 阐明了这种符号。我们要表达 `Car` 类和 `Automobile` 类之间的关系，我们可以说一个 `Car` 是一个 `Automobile`。

## 图 10-2 类头中的继承符号

![](img/8a88e1d8c69a687988c05f162ce32cac_612_0.png)

## 10.1 继承

由于 `Car` 类派生自 `Automobile` 类，因此 `Car` 继承了 `Automobile` 类的所有成员，构造函数除外。（基类的目的是创建基类的实例，因此派生类不继承基类的构造函数是合理的。）

> 注意：尽管派生类继承了基类的私有成员，但它无法直接访问它们。只有基类中的方法可以直接访问类的私有成员。

`Car` 类有一个出现在第 7–10 行的构造函数。在第 9 行中，构造函数将 `_doors` 字段赋值为 0。以下是创建 `Car` 类对象时发生情况的总结：

- 首先执行基构造函数。在这种情况下，它被调用并将 `_make` 和 `_model` 字段赋值为空字符串，并将 `_mileage` 和 `_price` 字段赋值为 0。
- 接下来执行派生构造函数。在这种情况下，`_doors` 字段被赋值为 0。

`Doors` 属性的代码出现在第 13–17 行。

在继续之前，让我们来看一个演示了 `Automobile` 和 `Car` 类的完整应用程序。在学生示例程序的 `Chap10` 文件夹中，我们将找到一个名为 `Car Demo` 的项目。该项目包含 `Automobile` 类和 `Car` 类。图 10-3 显示了 `Form1` 表单。

## 图 10-3 Car Demo 项目的 Form1 表单

![](img/8a88e1d8c69a687988c05f162ce32cac_613_0.png)

当你运行应用程序时，输入示例数据并点击按钮。应用程序将创建一个 `Car` 类的对象，并将文本框中的数据赋值给对象的属性。它将在 `makeLabel`、`modelLabel`、`mileageLabel` 和 `doorsLabel` 控件中显示对象的属性。图 10-4 显示了 `Form1.cs` 中的代码。

```csharp
1 using System;
2 using System.Collections.Generic;
3 using System.ComponentModel;
4 using System.Data;
5 using System.Drawing;
6 using System.Linq;
7 using System.Text;
8 using System.Tasks;
9 using System.Windows.Forms;

10
11 partial class Form1 : Form
12 {

13
14     public Form1()
15     {
16         InitializeComponent();
17     }

18
19     private void createButton_Click(object sender, EventArgs e)
20     {
21         // 创建对象。
22         Car myCar = new Car();

23
24         // 获取数据。
25         GetCarData(myCar);

26
27         // 显示数据。
28         makeLabel.Text = myCar.Make;
29         modelLabel.Text = myCar.Model;
30         mileageLabel.Text = myCar.Mileage.ToString();
31         doorsLabel.Text = myCar.Doors.ToString();
32     }

33
34     private void GetCarData(Car car)
35     {
36         // 获取数据。
37         if (int.TryParse(mileageTextBox.Text, out int mileage))
38         {
39             car.Mileage = mileage;
40         }
41         else
42         {
43             MessageBox.Show("Invalid mileage");
44         }

45
46         if (decimal.TryParse(priceTextBox.Text, out decimal price))
47         {
48             car.Price = price;
49         }
50         else
51         {
52             MessageBox.Show("Invalid price");
53         }

54
55         if (int.TryParse(doorsTextBox.Text, out int doors))
56         {
57             car.Doors = doors;
58         }
59         else
60         {
61             MessageBox.Show("Invalid doors");
62         }
63     }

64
65     private void exitButton_Click(object sender, EventArgs e)
66     {
67         // 关闭表单。
68         this.Close();
69     }
70 }
```
