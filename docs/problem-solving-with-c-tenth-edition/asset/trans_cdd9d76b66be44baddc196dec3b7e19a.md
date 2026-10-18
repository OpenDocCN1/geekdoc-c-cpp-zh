

- 14. 类 `Money` 的修改后定义如下所示。颜色部分为新增内容。我们省略了一些注释以节省空间，但 Display 11.5 中显示的所有注释都应包含在此定义中。我们已将本次练习中的更改包含在此答案中，因为在重载 `<=` 运算符的定义中使用重载的 `<` 运算符是自然的。

```cpp
class Money
{
public:
    friend Money operator +(const Money& amount1,
                            const Money& amount2);
    friend bool operator ==(const Money& amount1,
                            const Money& amount2);
    friend bool operator <(const Money& amount1,
                           const Money& amount2);
    //Precondition: amount1 and amount2 have been given values.
    //Returns true if amount1 is less than amount2;
    //otherwise, returns false.
    friend bool operator <=(const Money& amount1,
                            const Money& amount2);
    //Precondition: amount1 and amount2 have been given values.
    //Returns true if amount1 is less than or equal to amount2; otherwise, returns false.
    Money(long dollars, int cents);
    Money(long dollars);
    Money();
    double getValue() const;
    void input(istream& ins);
    void output(ostream& outs) const;
private:
    long allCents;
};
```

你还必须添加以下重载 `operator <=` 的定义（以及上一练习中给出的重载 `operator <` 的定义）：

```cpp
bool operator <=(const Money& amount1,
                 const Money& amount2)
{
    return ((amount1.allCents < amount2.allCents)
            || (amount1.allCents == amount2.allCents));
}
```

- 15. 在重载运算符时，运算符的参数中至少有一个必须是类类型。这可以防止改变整数的 `+` 的行为。实际上，这一要求可以防止改变任何内置类型上任何运算符的效果。

- 16.

```cpp
//Uses math (for floor):
Money::Money(double amount)
{
    allCents = floor(amount * 100);
}
```

此定义只是丢弃小于一美分的任何金额。例如，它将 12.34999 转换为整数 1234，表示金额 $12.34。可以定义构造函数来对任何分的分数做其他处理。

- 17.

```cpp
istream& operator >>(istream& ins, Pairs& second)
{
    char ch;
    ins >> ch;        //discard initial '('
    ins >> second.f;
    ins >> ch;        //discard comma ','
    ins >> second.s;
    ins >> ch;        //discard final ')'
    return ins;
}

ostream& operator <<(ostream& outs, const Pairs& second)
{
    outs << '(';
    outs << second.f;
    outs << ','; //You might prefer ","
                //to get an extra space
    outs << second.s;
    outs << ')';
    return outs;
}
```

- 18.

```cpp
//Uses iostream:
istream& operator >>(istream& ins, Percent& theObject)
{
    char percentSign;
    ins >> theObject.value;
    ins >> percentSign; //Discards the % sign.
    return ins;
}

//Uses iostream:
ostream& operator <<(ostream& outs,
    const Percent& aPercent)
{
    outs << aPercent.value << '%';
    return outs;
}
```

- 19.

```cpp
struct Score
{
    int homeTeam;
    int opponent;
};
Score game[10];
```

- 20.

```cpp
//Reads in 5 amounts of money, doubles each amount,
//and outputs the results.
#include <iostream>

<The definitions for the Money class go here.>

int main()
{
    using namespace std;
    Money amount[5];
    int i;
    cout << "Enter 5 amounts of money:\n";
    for (i = 0; i < 5; i++)
        cin >> amount[i];
    for (i = 0; i < 5; i++)
        amount[i] = amount[i] + amount[i];
    cout << "After doubling, the amounts are:\n";
    for (i = 0; i < 5; i++)
        cout << amount[i] << " ";
    cout << endl;
    return 0;
}
```

（你不能使用 `2 * amount[i]`，因为 `*` 对于类型为 `Money` 的操作数尚未被重载。）

- 21. 见答案 22。

- 22. 本答案结合了本练习和前一个自测练习的答案。类定义将更改为如下所示。（我们已从 Display 11.10 中删除了一些注释以节省空间，但你应在答案中包含它们。）

```cpp
class TemperatureList
{
public:
    TemperatureList();

    int getSize() const;
    //Returns the number of temperatures on the list.

    void addTemperature(double temperature);

    double getTemperature(int position) const;
    //Precondition: 0 <= position < getSize().
    //Returns the temperature that was added in position
    //specified. The first temperature that was added is
    //in position 0.

    bool full() const;

    friend ostream& operator <<(ostream& outs,
        const TemperatureList& theObject);
private:
    double list[MAX_LIST_SIZE]; //of temperatures in
                                //Fahrenheit
    int size; //number of array positions filled
};
```

你还需要添加以下成员函数定义：

```cpp
int TemperatureList::getSize() const
{
    return size;
}

//Uses iostream and cstdlib:
double TemperatureList::getTemperature (int position) const
{
    if ((position >= size) || (position < 0))
    {
        cout << "Error:"
             << " reading an empty list position.\n";
        exit(1);
    }
    else
        return (list[position]);
}
```

- 23. *构造函数* 的名称为 `MyClass`，与类名相同。*析构函数* 的名称为 `~MyClass`。

- 24. 对话将更改为如下所示：

![](img/88b1f375f11336dbd9dac8b1675d0698_728_0.png)

- 25. `::` 之前的 `StringVar` 是类的名称。`::` 右侧的 `StringVar` 是成员函数的名称。（记住，构造函数是与类同名的成员函数。）括号内的 `StringVar` 是参数 `stringObject` 的类型。

- 26.
  - a. 析构函数是类的成员函数。析构函数的名称总是以波浪号 `~` 开头，后跟类名。
  - b. 当类对象超出作用域时，会调用析构函数。
  - c. 析构函数实际上执行类作者为其编程的任何操作！
  - d. 析构函数应删除由构造函数为该类分配的动态变量。析构函数还可能执行其他清理任务。

- 27. 对于赋值运算符 `=` 和拷贝构造函数，如果数据只有内置类型，则默认的拷贝机制正是你想要的，因此默认值效果很好。对于析构函数，不进行动态内存分配（没有指针），因此默认的无操作行为也是你想要的。

## PRACTICE PROGRAMS

练习程序通常可以用一个简短的程序来解决，该程序直接应用本章介绍的编程原理。

- 1. 修改 Display 11.8 中显示的类 `Money` 的定义，以便添加以下所有内容：
  - a. 运算符 `<`、`<=`、`>` 和 `>=` 已分别重载以适用于类型 `Money`。（提示：参见自测练习 13。）
  - b. 以下成员函数已添加到类定义中。（我们以其在类定义中应出现的函数声明形式显示该函数。函数的定义本身将包含限定符 `Money::`。）

    ```cpp
    Money percent(int percentFigure) const;
    //Returns a percentage of the money amount in the
    //calling object. For example, if percentFigure is 10,
    //then the value returned is 10% of the amount of
    //money represented by the calling object.
    ```

    例如，如果 `purse` 是类型为 `Money` 的对象，其值表示金额 $100.10，则调用

    ```cpp
    purse.percent(10);
    ```

    返回 $100.10 的 10%；即返回类型为 `Money` 的值，表示金额 $10.01。

- 2. 自测练习 17 要求你为类 `Pairs` 重载运算符 `>>` 和运算符 `<<`。完成并测试此练习。实现默认构造函数以及一个和两个 `int` 参数的构造函数。单参数构造函数应初始化对的第一个成员；对的第二个成员应为 0。

重载二元运算符 `+` 以按规则添加对  
`(a, b) + (c, d) = (a + c, b + d)`

类似地重载运算符 `-`。

在 `Pairs` 和 `int` 上重载运算符 `*`，规则为  
`(a, b) * c = (a * c, b * c)`

编写程序测试类定义中的所有成员函数和重载运算符。

- 3. 定义一个类 `DegreeAngle`，其中包含一个表示角度的整数字段。此类型可保存的值范围为 0-359，你的代码应确保该范围不会被超出。实现默认构造函数和一个带一个整数参数的构造函数。重载 `+` 和 `-` 运算符以允许 `DegreeAngle` 对象的加法和减法。重载 `<<` 和 `>>` 运算符以实现从输入流读取和写入数据。编写驱动程序测试你的类及其功能。

## PROGRAMMING PROJECTS

编程项目比练习程序需要更多的解题能力，通常可以用多种不同方式解决。访问 www.myprogramminglab.com 在线完成这些编程项目并获得即时反馈。

- 1. 在第 8 章中我们讨论了向量，它们就像可以增长大小的数组。假设 C++ 中未定义向量。定义一个名为 `VectorDouble` 的类，它类似于 `double` 基类型的向量类。你的类 `VectorDouble` 将有一个私有成员变量用于 `double` 的动态数组。它还将有两个 `int` 类型的成员变量；一个名为 `maxCount` 用于 `double` 动态数组的大小；一个名为 `count` 用于当前持有值的数组位置数。(`maxCount` 与向量的容量相同；`count` 与向量的大小相同。)

如果尝试向 `VectorDouble` 类的向量对象添加一个元素（`double` 类型的值）而没有更多空间，则会创建一个具有两倍旧动态数组容量的新动态数组，并将旧动态数组的值复制到新动态数组中。

