

## 列表 2.10 对类成员执行强制限制

```
d1.setFeet(1);
d1.setInches(9.5);
d2.setFeet(2);
d2.setInches(5.5);
d3=d1.add(d2);
```

那么 d3.fInches 的值将变为 3（而不是 15），而 d3.iFeet 的值将变为 4（而不是 3）。
之前已经提到，现实世界中的对象永远不会避免无效状态。它们初始时也不会处于无效状态。那么 C++ 是否允许库程序员在类对象中实现这一功能呢？
让我们继续之前的示例——`Distance` 类。记住，库程序员的意图是确保 `Distance` 类中没有任何一个对象的 `fInches` 属性的值都不应超过 12。现在，让我们考虑列表 2.11。

## 列表 2.11 使用不当值创建的对象

```cpp
/*Beginning of DistJunk.cpp*/
#include<iostream>
#include "Distance.h"
void main()
{
    Distance d1;
    cout<<d1.getFeet<<" "<<d1.getInches()endl;
}
/*End of DistJunk.cpp*/
```

# 输出
29 34.56

如你所见，“d1”的 `fInches` 值大于 12！这种现象发生是因为当 ‘d1’ 分配内存时，`iFeet` 和 `fInches` 的值都自动变成了垃圾值，而对于 `d1.fInches` 来说，垃圾值大于 12。因此，库程序员保持 `fInches` 值小于 12 的目标没有实现。
期望应用程序程序员显式地初始化每一个声明的对象是不现实的。

```cpp
Distance d1; //初始化
d1.setFeet(0.0); //初始化
```

显然，库程序员希望在 `Distance` 类中添加一个函数，该函数在对象创建时被自动调用，并设置对象成员属性的值。这样的函数就是*构造函数*。构造函数的概念以及相关的函数——*析构函数*，将在后面的章节中讨论。
但可能会有人说，即使 `Distance` 是一个普通的结构体，且 `setInches()` 函数像 C 语言中一样是非成员函数，数据抽象依然存在。尽管如此，在 C 的情况下，库程序员无法强制只调用他未定义的函数。类与对象 47

数据抽象对于数据隐藏是有效的（回想之前讨论过的投影仪系统案例）。

硬币的反面，在 C 语言中，应用程序程序员的生活会变得艰难。如果结构体的某个成员获取了无效或错误的值，他/她必须搜索整个源代码来检测错误。随着代码长度的增加，这个问题的重要性迅速凸显。在实际实践中，拥有超过 25,000 行的代码是很常见的。

现在让我们进行如下总结：
-   由于数据隐藏，成员函数的完美定义保证了其目标的实现。

这就是面向对象编程系统的精髓。现实世界的对象不仅有工作部分，还有通往这些内部工作部分的排他接口。完美的接口由于其排他性被保证能够正常工作。

## 2.1.8 显式地址操作

应用程序程序员可以通过显式地址操作来操纵任何对象的成员数据。列表 2.12 说明了这一点。

## 列表 2.12 显式地址操作

```cpp
/*Beginning of AddrManip.cpp*/
#include<Distance.h>
#include<iostream.h>

void main()
{
    Distance d1;
    d1.setFeet(256);
    d1.setInches(2.2);
    char * p=(char *)&d1; //显式地址操作
    *p=1; //不希望发生但无法避免
    cout<<d1.getFeet<<" "<<d1.getInches()endl;
}
/*End of AddrManip.cpp*/
```

输出
257 2.2

然而，应用程序程序员这种显式地址操作是无法防止的。这留给读者作为一个练习，以解释上述段落（列表 2.12）的输出。

## 2.1.9 箭头运算符

可以通过指向对象的指针调用对象的成员函数。箭头运算符 (->) 实现了这一点。列表 2.13 展示了一个说明性示例。

## 列表 2.13 通过指针访问成员

```cpp
/*Beginning of PointerMember.cpp*/
#include<iostream.h>
#include"Distance.h"

void main() {
    Distance d1;           //对象
    Distance * dPtr;      //指针
    dPtr=&d1;               //指针初始化
    /*相当于 d1.setFeet(1.1) 和 d1.getInches(1.1)*/
    dPtr->setFeet(1);      //调用成员函数
    dPtr->setFeet(1.1);    //通过指针
    /*相当于 d1.getInches() << d1.getInches()*/
    cout<<dPtr->getInches<<" "<<dPtr->getInches()endl;
}
/*End of PointerToMember.cpp*/
```

# 输出
11.1

有趣的是，点 (. ) 运算符和箭头 (->) 运算符的定义在 C++ 中得到了扩展。它在 C++ 中不仅接收右侧的数据成员，还将成员函数作为其右侧的操作数。如果右侧的操作数是数据成员，则箭头的行为与 C 语言中相同。然而，如果它是一个类的成员函数，且其左侧的操作数是相同类型，那么编译器简单地将指针的值作为隐式的起始参数传递给函数调用。因此，语句

```
dPtr->setFeet(1);
```

在转换后变为

```cpp
setFeet(dPtr,1);
```

现在，dPtr 的值被拷贝到该指针。因此，该指针也指向 dPtr 所指向的同一个对象。

## 2.1.10 从另一个函数调用成员函数

可以从另一个函数调用成员函数。列表 2.14 展示了一个说明性示例。

| 列表 2.14 | 从另一个函数调用成员函数 |
| :--- | :--- |

```cpp
/*Beginning of NestedCall.cpp*/
class A
{
    int x;
public:
    void setindirect(int q);
    void setx(int p);
};

void A::setindirect(int q)
{
    x=q;
}
void A::setx(int p)
{
    setindirect(p);
}
void main()
{
    A A1;
    A1.setindirect(1);
    A1.setx(2);
}
/*end of NestedCall.cpp*/
```

