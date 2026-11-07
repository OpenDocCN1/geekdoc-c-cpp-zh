
确定 `class first` 的哪些成员在 `class fifth` 中是私有、受保护和公有的。

- **16.** 下面的代码有什么问题？

```cpp
class classA
{
protected:
    void setX(int a);                         //Line 1
        //Postcondition: x = a;               //Line 2
private:                                      //Line 3
    int x;                                    //Line 4
};
.
.
.
int main()
{
    classA aObject;                          //Line 5

    aObject.setX(4);                         //Line 6
    return 0;                                 //Line 7
}
```

- **17.** 考虑以下代码：

```cpp
class one
{
public:
    void print() const;
        //Output the values of x and y
protected:
    void setData(int u, int v);
        //Postcondition: x = u; y = v;
private:
    int x;
    int y;
};

class two: public one
{
public:
    void setData(int a, int b, int c);
        //Postcondition: x = a; y = b; z = c;
    void print() const;
        //Output the values of x, y, and z
private:
    int z;
};
```

  - a. 写出 `class two` 中函数 `setData` 的定义。

  - b. 写出 `class two` 中函数 `print` 的定义。

- **18.** 以下 C++ 程序的输出是什么？

```cpp
#include <iostream>
#include <string>

using namespace std;

class baseClass
{
public:
    void print() const;

    baseClass(string s = "", int a = 0);
        //Postcondition: str = s; x = a;

protected:
    int x;

private:
    string str;
};

class derivedClass: public baseClass
{
public:
    void print() const;

    derivedClass(string s = "", int a = 0, int b = 0);
        //Postcondition: str = s; x = a; y = b;

private:
    int y;
};

int main()
{
    baseClass baseObject("This is the base class", 2);
    derivedClass derivedObject("DDDDDD", 3, 7);

    baseObject.print();
    derivedObject.print();

    return 0;
}

void baseClass::print() const
{
    cout << x << " " << str << endl;
}

baseClass::baseClass(string s, int a)
{
    str = s;
    x = a;
}

void derivedClass::print() const
{
    cout << "Derived class: " << y << endl;
    baseClass::print();
}

derivedClass::derivedClass(string s, int a, int b)
    : baseClass("Hello Base", a + b)
{
    y = b;
}
```

- **19.** 考虑以下类定义：

```cpp
class baseClass
{
public:
    void print() const;
    int getX() const;
    baseClass(int a = 0);

protected:
    int x;
};

class derivedClass : public baseClass
{
public:
    void print() const;
    int getResult() const;
    derivedClass(int a = 0, int b = 0);

private:
    int y;
};
```

假设这些类的成员函数定义如下：

```cpp
void baseClass::print() const
{
    cout << "In base: x = " << x << endl;
}

baseClass::baseClass(int a)
{
    x = a;
}

int baseClass::getX() const
{
    return x;
}

void derivedClass::print() const
{
    cout << "In derived: x = " << x << ", y = " << y
         << "; x + y = " << x + y << endl;
}

int derivedClass::getResult() const
{
    return x + y;
}

derivedClass::derivedClass(int a, int b)
                 : baseClass(a)
{
    y = b;
}
```

以下 main 函数的输出是什么？

```cpp
int main()
{
    baseClass baseObject(7);
    derivedClass derivedObject(3, 8);

    baseObject.print();
    derivedObject.print();

    cout << "***** " << baseObject.getX() << endl;
    cout << "***** " << derivedObject.getResult() << endl;

    return 0;
}
```

## 编程练习

- **1.** 在第 11 章中，类 `clockType` 被设计用于实现程序中的一天中的时间。某些应用除了小时、分钟和秒之外，可能还要求存储时区。通过添加一个成员变量来存储时区，从类 `clockType` 派生类 `extClockType`。添加必要的成员函数和构造函数，使该类具备相应功能。同时，写出成员函数和构造函数的定义。最后，编写一个测试程序来测试你的类。

- **2.** 在本章中，类 `dateType` 被设计用于实现程序中的日期，但成员函数 setDate 和构造函数在将日期存储到成员变量之前没有检查日期是否有效。重写函数 `setDate` 和构造函数的定义，以便在将日期存储到成员变量之前检查月、日、年的值。添加一个成员函数 `isLeapYear`，用于检查某一年是否为闰年。此外，编写一个测试程序来测试你的类。

- **3.** *x-y* 平面中的一个点由其 *x* 坐标和 *y* 坐标表示。设计一个类 `pointType`，它可以存储并处理 *x-y* 平面中的一个点。然后，你应该对该点执行操作，例如设置点的坐标、打印点的坐标、返回 *x* 坐标以及返回 *y* 坐标。同时，编写一个程序来测试对该点的各种操作。

- **4.** 每个圆都有一个圆心和一个半径。给定半径，我们可以确定圆的面积和周长。给定圆心，我们可以确定其在 *x-y* 平面中的位置。圆的圆心是 *x-y* 平面中的一个点。设计一个类 `circleType`，它可以存储圆的半径和圆心。由于圆心是 *x-y* 平面中的一个点，并且你在编程练习 3 中设计了类来捕获点的属性，因此你必须从类 `pointType` 派生类 `circleType`。你应该能够对圆执行常规操作，例如设置半径、打印半径、计算并打印面积和周长，以及对圆心执行常规操作。同时，编写一个程序来测试对圆的各种操作。

- **5.** 每个圆柱都有一个底面和一个高，其中底面是一个圆。设计一个类 `cylinderType`，它可以捕获圆柱的属性并对圆柱执行常规操作。从编程练习 4 中设计的类 `circleType` 派生这个类。可以对圆柱执行的部分操作如下：计算并打印体积、计算并打印表面积、设置高、设置底面半径以及设置底面圆心。同时，编写一个程序来测试对圆柱的各种操作。

- **6.** 使用类设计一个在线通讯录，用于记录家庭成员、密友和某些业务伙伴的姓名、地址、电话号码和出生日期。你的程序应能够处理最多 500 个条目。

  - a. 定义一个类 `addressType`，它可以存储街道地址、城市、州和邮政编码。使用适当的函数打印和存储地址。同时，使用构造函数自动初始化成员变量。

  - b. 使用类 `personType`（如第 11 章示例 11–9 中所定义）、类 `dateType`（如本章编程练习 2 中所设计）和类 `addressType` 定义类 `extPersonType`。向该类添加一个成员变量，用于将此人分类为家庭成员、朋友或业务伙伴。同时，添加一个成员变量来存储电话号码。添加（或重写）函数以打印和存储相应的信息。使用构造函数自动初始化成员变量。

  - c. 使用先前定义的类定义 `class addressBookType`。类型为 addressBookType 的对象应能够处理最多 500 个条目。

程序应执行以下操作：

  - i. 从磁盘将数据加载到通讯录中。

  - ii. 按姓氏对通讯录进行排序。

  - iii. 按姓氏搜索某个人。

  - iv. 打印给定人员的地址、电话号码和出生日期（如果存在）。

  - v. 打印生日在给定月份的人员姓名。

  - vi. 打印姓氏位于两个姓氏之间的所有人员姓名。

  - vii. 根据用户的请求，打印所有家庭成员、朋友或业务伙伴的姓名。

- **7.** 在编程练习 2 中，设计并实现了 `class dateType` 来记录日期，但它的操作非常有限。重新定义 `class dateType`，使其除了已定义的操作外，还能对日期执行以下操作：

  - a. 设置月份。

  - b. 设置日。

  - c. 设置年份。

  - d. 返回月份。

  - e. 返回日。

  - f. 返回年份。

  - g. 测试该年是否为闰年。

  - h. 返回该月中的天数。例如，如果日期是 3-12-2013，则应返回的天数为 31，因为三月有 31 天。

  - i. 返回该年中已经过去的天数。例如，如果日期是 3-18-2013，则该年中已经过去的天数为 77。注意，返回的天数还包括当天。

  - j. 返回该年中剩余的天数。例如，如果日期是 3-18-2013，则该年中剩余的天数为 288。

  - k. 通过向日期加上固定天数来计算新日期。例如，如果日期是 3-18-2013，并且要加上的天数为 25，则新日期是 4-12-2013。

