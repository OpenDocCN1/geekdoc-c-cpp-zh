

## 程序清单 10.4 具有私有成员的类（第 2 部分，共 2 部分）

```
42     cin >> month;
43     cout << "Enter the day of the month: ";
44     cin >> day;
45     checkDate();
46 }
47
48 void DayOfYear::output()
    <The rest of the definition of DayOfYear::output is
     given in Display 10.3.>
49
50 void DayOfYear::set(int newMonth, int newDay)
51 {
52     month = newMonth;
53     day = newDay;
54     checkDate();
55 }
56
57 void DayOfYear::checkDate()
58 {
59     if ((month < 1) || (month > 12) || (day < 1) || (day > 31))
60     {
61         cout << "Illegal date. Aborting program.\n";
62         exit(1);
63     }
64 }
65
66 int DayOfYear::getMonth()
67 {
68     return month;
69 }
70
71 int DayOfYear::getDay()
72 {
73     return day;
74 }
```

私有成员可以在成员函数定义中使用（但不能在其他地方使用）。

成员函数 input 的更好定义会要求用户在输入错误日期时重新输入日期。

成员函数 checkDate 并不检查所有非法日期，但只需把它写得更长一些，就很容易使检查完整。参见自测练习 14。

函数 exit 将在第 6 章讨论。它会终止程序。

### 示例对话

```
Enter today's date:
Enter the month as a number: 3
Enter the day of the month: 21
Today's date is month = 3, day = 21
J. S. Bach's birthday is month = 3, day = 21
Happy Birthday Johann Sebastian!
```

```
//Postcondition: The date is reset according to the
//arguments.

int getMonth();
//Returns the month, 1 for January, 2 for February, etc.

int getDay();
//Returns the day of the month.
private:
    void checkDate();
    char firstLetter; //of month
    char secondLetter; //of month
    char thirdLetter; //of month
    int day;
};
```

这样一来，定义成员函数会稍微困难一些，但可以重新定义它们，使它们的行为与之前完全一样。例如，函数 getMonth 的定义可能如下所示：

```
int DayOfYear::getMonth()
{
    if (firstLetter == 'J' && secondLetter == 'a'
        && thirdLetter == 'n')
        return 1;
    if (firstLetter == 'F' && secondLetter == 'e'
        && thirdLetter == 'b')
        return 2;
    ...
```

这种方法相当繁琐，但并不困难。

还要注意，成员函数 DayOfYear::set 和 DayOfYear::input 会检查成员变量 month 和 day 是否被设置为合法的值。这是通过调用成员函数 DayOfYear::checkDate 来完成的。如果成员变量 month 和 day 是公有而不是私有，那么这些成员变量就可以被设置为任何值，包括非法值。通过将成员变量设为私有，并只通过成员函数来操作它们，我们可以确保成员变量永远不会被设置为非法或无意义的值。（在自测练习 14 中，要求你重新定义成员函数 DayOfYear::checkDate，以便对非法日期进行完整的检查。）

**封装**也称为**数据隐藏**。这是一种将类中的变量设为私有，并使其只能通过受控的公有或保护函数接口进行访问的技术。这使你可以修改内部变量和数据结构，而不会破坏使用你的类的代码。

也可以将成员函数设为私有。与私有成员变量一样，私有成员函数可以在任何其他成员函数的定义中使用，但不能在其他任何地方使用，例如在使用该类类型的程序的主函数部分中。例如，程序清单 10.4 中的成员函数 DayOfYear::checkDate 就是一个私有成员函数。通常的做法是，如果只期望将某个成员函数用作成员函数定义中的辅助函数，就将其设为私有成员函数。

关键字 public 用于表示公有成员，就像关键字 private 用于表示私有成员一样。例如，对于程序清单 10.4 中定义的类 DayOfYear，除 DayOfYear::checkDate 之外的所有成员函数都是公有成员（而所有成员变量都是私有成员）。公有成员可以在程序的主函数体中使用，也可以在任何函数的定义中使用，甚至可以在非成员函数中使用。

在一个类定义中，public 和 private 可以出现任意多次。每次插入标签 `public:`，成员列表就会从私有变为公有。每次插入标签 `private:`，成员列表就会重新变为私有成员。例如，下面结构定义中的成员函数 doSomethingElse 和成员变量 moreStuff 是私有成员，而其他四个成员都是公有成员：

```
class SampleClass
{
public:
    void doSomething();
    int stuff;
private:
    void doSomethingElse();
    char moreStuff;
public:
    double doYetAnotherThing();
    double evenMoreStuff;
};
```

如果在类定义的开头列出成员，并且在这些起始成员之前没有插入 public: 或 private:，那么它们将是私有成员。不过，最好始终明确地将每一组成员标记为 public 或 private。

![](img/88b1f375f11336dbd9dac8b1675d0698_601_0.png)

## 类与对象

**类**是一种类型，其变量就是**对象**。这些对象既可以有成员变量，也可以有成员函数。类定义的语法如下。

### 语法

```
class ClassName
{
public:
    MemberSpecification_1
    MemberSpecification_2
    .
    .
    MemberSpecification_n
private:
    MemberSpecification_n+1
    MemberSpecification_n+2
    .
    .
};
```

每个 *MemberSpecification_i* 要么是成员变量声明，要么是成员函数声明。（允许有额外的 *public* 和 *private* 部分。）

### 示例

```
class Bicycle
{
public:
    char getColor();
    int numberOfSpeeds();
    void set(int theSpeeds, char theColor);
private:
    int speeds;
    char color;
};
```

一旦定义了类，就可以像声明其他任何类型的变量一样来声明对象（对象只是类类型的变量）。例如，下面的语句声明了两个 Bicycle 类型的对象：

```
Bicycle myBike, yourBike;
```

允许你更改类的私有成员变量值的成员函数称为设置函数（mutator functions）。虽然 C++ 语言并未要求，但设置函数的名字通常包含 set。

在每个类定义中始终包含访问函数和设置函数是很重要的，这样你就可以更改对象中存储的数据。

## 自测练习

- 14. 程序清单 10.4 中的私有成员函数 DayOfYear::checkDate 会放过一些非法日期，例如 2 月 30 日。请重新定义成员函数 DayOfYear::checkDate，使它在发现任何非法日期时终止程序。允许 2 月有 29 天，以便考虑闰年。（提示：这有点繁琐，函数定义也稍长，但并不很难。）

- 15. 假设你的程序包含以下类定义：

```
class Automobile
{
public:
    void setPrice(double newPrice);
    void setProfit(double newProfit);
    double getPrice();
private:
    double price;
    double profit;
    double getProfit();
};
```

并假设程序的主函数部分包含以下声明，并且程序以某种方式将所有成员变量的值设置为某些值：

```
Automobile hyundai, jaguar;
```

那么，在程序的主函数部分中，下列哪些语句是允许的？

```
hyundai.price = 4999.99;
jaguar.setPrice(30000.97);
double aPrice, aProfit;
aPrice = jaguar.getPrice();
aProfit = jaguar.getProfit();
aProfit = hyundai.getProfit();
```

