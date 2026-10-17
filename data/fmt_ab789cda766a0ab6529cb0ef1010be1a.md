
17

18 `Demo` `demoObj`; // 定义一个 Demo 对象

19

20     `cout` << "This is displayed after the object is created.\n";

21     return 0;

22 }

```

### 程序输出

This is displayed before the object is created.
Now the constructor is running.
This is displayed after the object is created.

> 程序 7-4 中，我们将构造函数定义为类声明内部内联函数。然而，像任何其他类成员一样，我们也可以仅将其原型放在类声明中，然后在类外部定义它。在这种情况下，我们需要在函数名中使用作用域解析运算符 `::` 添加该函数所属的类名。但由于构造函数的名称与类名相同，因此该名称将出现两次。如果我们在类外部定义 `Demo` 构造函数，其函数头看起来将如下所示。

```
Demo::Demo()                    // 构造函数

{

    cout << "Now the constructor is running.\n";

}
```

程序 7-5 修改了程序 7-2，包含了一个用于初始化对象成员数据的构造函数。该构造函数定义在类外部。

## 7.6 构造函数

## 程序 7-5

```
// 此程序使用构造函数初始化成员变量。
#include <iostream>
#include <cmath>
using namespace std;

// Circle 类成员声明
class Circle
{ private:
    double radius;

   public:      // 成员函数原型
   Circle();
   void setRadius(double);
   double calcArea();
};

// Circle 成员函数实现部分
/*************************************************
*             Circle::Circle
*    * 这是构造函数。它初始化
*    * radius 类成员变量。
***************************************************/
Circle::Circle()
    radius = 1.0;
}

/***************************************************
*             Circle::setRadius
*    * 此函数在将值赋给 radius
*    * 成员变量之前，对其传递的值进行验证。
*    *
***************************************************/
void Circle::setRadius(double r)
    if (r >= 0.0)
        radius = r;
    else // 保持其原有值
}

/***************************************************
*             Circle::calcArea
*    * 此函数计算并返回
*    * Circle 对象的面积。它不需要任何
*    * 参数，因为它可以直接访问
*    * 成员变量。
***************************************************/
double Circle::calcArea()
    return 3.14 * pow(radius, 2);
}
```

（程序继续）

## 程序 7-5（续）

```
/*************************************
 * main 函数创建并使用了 *
 * 2 个 Circle 对象。
 **************************************/
int main() {
    // 定义一个 Circle 对象。由于从未为它调用
    // 调用 setRadius 函数，它将保留由构造函数
    // 设置的值。
    Circle circle1;
    // 定义第二个 Circle 对象并将其半径设置为 2.5
    Circle circle2;
    circle2.setRadius(2.5);
    // 获取并显示每个圆的面积
    cout << "The area of circle1 is " << circle1.calcArea() << endl;
    cout << "The area of circle2 is " << circle2.calcArea() << endl;
    return 0;
}
```

程序输出
The area of circle1 is 3.14
The area of circle2 is 19.625

## 构造函数重载

回想第 6 章，当两个或多个函数共享相同的名称时，该函数名称被称为“重载”。在 C++ 程序中，可以存在多个同名的函数，只要它们的参数列表不同。

任何类成员函数都可以被重载，包括构造函数。例如，一个构造函数可以接受一个整数，而另一个构造函数接受一个双精度浮。可能有第三个接受两个整数的构造函数。只要每个构造函数都有不同的参数列表，编译器就能区分它们。

程序 7-6 声明并使用了一个名为 `Sale` 的类，该类有两个构造函数。第一个包含一个接受销售率的参数。第二个构造函数用于免税销售，它没有带参数。它将税率设置为 0。

## 程序 7-6

```
// 此程序演示了重载构造函数的用法。
#include <iostream>
#include <iomanip>
using namespace std;

// Sale 类成员声明
class Sale
{ private:
    double taxRate;

   public:      // 成员函数原型
   Sale();
   Sale(double);
   double calcTotal(double);
};

// Sale 成员函数实现部分
/*************************************************
*             Sale::Sale
*    * 这是默认构造函数。它初始化
*    * taxRate 为 0。
***************************************************/
Sale::Sale()
    taxRate = 0;
}

/***************************************************
*             Sale::Sale
*    * 这是带参数的构造函数。它将
*    * tax 设置为传递的值。
***************************************************/
Sale::Sale(double r)
    taxRate = r;
}

/***************************************************
*             Sale::calcTotal
*    * 此函数计算并返回
*    * 包含税费的总价。
***************************************************/
double Sale::calcTotal(double cost)
    return cost + (cost * taxRate);
}

int main() {
    // 使用默认构造函数创建一个 Sale 对象
    Sale sale1;
    // 使用带参数的构造函数创建一个 Sale 对象
    Sale sale2(0.06);

    // 显示每个对象的总价
    cout << fixed << setprecision(2);
    cout << "The total for sale1 is $" << sale1.calcTotal(100.0) << endl;
    cout << "The total for sale2 is $" << sale2.calcTotal(100.0) << endl;

    return 0;
}
```

如你所见，第一个构造函数没有参数。第二个构造函数有一个参数，但它有一个默认参数。如果定义对象时没有提供参数列表，编译器将无法判断执行哪一个构造函数。

## 7.7 析构函数

**概念：**析构函数是一个在对象销毁时自动调用的成员函数。

析构函数是公共成员函数，名称与类名相同，但前面有一个波浪号 `~`。例如，`Rectangle()` 的析构函数为 `~Rectangle()`。

当对象销毁时，析构函数会被自动调用。就像构造函数用于在对象创建时进行设置一样，析构函数用于在对象不再存在时执行清理程序。这种情况发生在，例如当带有对象的程序停止，或者当你从一个创建对象的函数返回时。

> 注意：关于如何在 UML 中表示析构函数的信息，可以在该书配套的配套网站 `pearsonhighered.com/gaddis` 的附录 F 中找到。

程序 7-7 显示了一个带有构造函数和析构函数的简单类。它说明了在程序执行期间它们各自何时被调用。

## 程序 7-7

```
// 此程序演示了析构函数。
#include <iostream>
using namespace std;

class Demo
{
public:
Demo();              // 构造函数原型
~Demo();             // 析构函数原型
};
Demo::Demo()        // 构造函数函数定义
{ cout << "An object has just been defined, so the constructor"
<< " is running.\n";
}

Demo::~Demo()      // 析构函数函数定义
{ cout << "Now the destructor is running.\n";
}
```

（程序继续）

```
int main()
{
    DemoObj obj; // 声明一个 Demo 对象；

    cout << "The object now exists, but is about to be destroyed.\n";
    return 0;
}
```

程序输出：
An object has just been defined, so the constructor is running.
The object now exists, but is about to be destroyed.
Now the destructor is running.

除了析构函数在对象销毁时会自动调用外，还应注意以下几点：

- 与构造函数一样，析构函数没有返回值。
- 析构函数不能接受参数，因此它们永远没有参数列表。
- 因为析构函数不能接受参数，所以只能有一个析构函数。

析构函数在处理动态分配的对象时最有用。你将在第 10 章中学习到这些。

## 检查点

- 7.5 简述构造函数的作用。
- 7.6 构造函数的名称与以下哪个相同
  A) 类
  B) 实例
  C) 程序
  D) 以上均不是
- 7.7 不需要参数的构造函数被称为
  A) 默认构造函数
  B) 内联构造函数
  C) 空空构造函数
  D) 以上均不是

- 7.8 假设以下是一个构造函数：
```
ClassAct::ClassAct(int x)
{
    item = x;
}
```
定义一个名为 `sally` 的 `ClassAct` 对象，向构造函数传递值 25。

- 7.9 正确或错误：与任何 C++ 函数一样，构造函数可以重载，前提是每个构造函数都有唯一的参数列表。

- 7.10 正确或错误：一个类可以有一个没有参数列表的构造函数，以及一个参数都带有默认参数的重载构造函数。

- 7.11 析构函数名称始终以开头
  A) 数字
  B) 波浪号 (~)
  C) 数据类型名称
  D) 类名

- 7.12 正确或错误：就像类可以有多个构造函数一样，它也可以有多个析构函数。

```
7.13 下面程序代码将在屏幕上显示什么？
class Tank {
private:
  int gallons;
public:
  Tank()
    { gallons = 50; }
  Tank(int gal)
    { gallons = gal; }
  int getGallons()
    { return gallons; }
  };
int main() {
  Tank storage1, storage2, storage3(20);
  cout << storage1.getGallons() << endl;
  cout << storage2.getGallons() << endl;
  cout << storage3.getGallons() << endl;
  return 0;
}
```

```
7.14 下面程序代码将在屏幕上显示什么？
class Package {
private:
  int value;
public:
  Package()
    { value = 7; cout << value << endl; }
  Package(int v)
    { value = v; cout << value << endl; }
  ~Package()
    { cout << "goodbye" << endl; }
  };
int main() {
  Package obj1(4);
  Package obj2;
  return 0;
}
```

## 私有成员函数

**概念：** 私有成员函数只能从同一类的成员函数中调用。

到目前为止，你见过的所有类函数都是公共函数。这意味着它们可以被类外部的代码调用。然而，类需要用于内部处理的函数，这些函数不应该被类外部调用。这些函数应该是私有的。

程序 7-8 显示了一个带有私有类的示例。`SimpleStat` 类设计用于从一组非负整数查找并报告信息，例如平均值和最大值。然而，一旦数字被接收并累加到总和，它就不会被保留。因此，该类无法通过检查读取的每个数字是否是否大于之前读取的任何数字来确定哪个数字是最大的。私有函数 `Largest` 就是为此设计的。

> 注意：关于如何在 UML 中声明私有和公共成员的信息，可以在该书配套的配套网站 `pearsonhighered.com/gaddis` 的附录 F 中找到。

## 程序 7-8

```
// 此程序使用一个带有私有函数的类，该函数判断
// 发给它的新值是否是迄为止的最大值。
#include <iostream>
using namespace std;
class SimpleStat
{
    private:
    int largest;       // 迄收到的最大数字
    int sum;            // 接收到的数字和
    int count;          // 接收了多少个数字
    bool isLargest(int num); // 这是一个私有函数
    public:
    SimpleStat();      // 默认构造函数
    void addNumber(int num);
    double calcAverage();
    int getLargest()
    {
        return largest;
    }
    int getCount()
    {
        return count;
    }
};
```

## 程序 7-8（继续）

// SimpleStat 实现
/**
 * SimpleStat 默认构造函数
 */
SimpleStat::SimpleStat()
{
    largest = sum = count = 0;
}

/**
 * SimpleStat::addNumber
 */
void SimpleStat::addNumber(int num)
{
    bool goodNum = true; // 如果有效
    if (num >= 0) {
        sum += num;            // 累加
        count++;               // 计数
        if(isLargest(num))   // 判断是否是新的最大
