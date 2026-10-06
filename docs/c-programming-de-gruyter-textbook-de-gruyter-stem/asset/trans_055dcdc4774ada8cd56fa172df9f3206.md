

## 7.2 访问控制

派生类继承基类的所有数据成员和函数成员，但构造函数和析构函数除外。然而，这些继承成员的访问属性可以在继承过程中改变。继承的属性由派生类定义中指定的继承模式决定。

基类成员有三种访问属性：public（公共）、protected（保护）和private（私有）。基类的私有成员可以访问同类中的任何其他成员 member，而通过基类对象，我们只能访问该类的公共成员。

继承有三种模式：公有继承、保护继承和私有继承。不同的继承模式会导致基类成员在派生类中具有不同的属性。访问情况分为两种情况：第一种是派生类中的新成员访问继承自基类的成员；第二种是在派生类外部，通过派生类对象访问继承自基类的成员。我们将分别讨论这些不同的情况。

### 7.2.1 公有继承

如果继承模式为公有，那么在派生类中，从基类继承的公共和保护成员的访问属性不会改变，但从基类继承的私有成员无法被直接访问。也就是说，在公有继承中，从基类继承的公共和保护成员的访问属性不会改变——它们在派生类中仍然是公共和保护成员，派生类中的其他成员可以直接访问它们。在类族外部，我们只能通过派生类对象访问从基类继承的公共成员。派生类成员和派生类对象都无法直接访问基类的私有成员。

例 7.1 Point 类的公有继承。

Point 类在之前的章节中已经多次提到。在这个示例中，我们将从 Point 类派生出一个新的 Rectangle 类。矩形由一个点、一个宽度和一个长度指定。矩形点具有 Point 类的所有特征，但矩形有它自己的特征。这意味着我们在继承 Point 类时，应该添加新的成员。继承关系可以用 UML 描述，如图 7.3 所示。

让我们从头文件开始。

![](img/5618306d085ac1bac8275d6c4c5bbf2a_284_0.png)

图 7.3：Point 类与 Rectangle 类之间继承关系的 UML。

```cpp
//Rectangle.h
class Point             //基类 Point 的定义
{
public:
    //公共成员函数
    void InitP(float xx=0, float yy=0) { X=xx;Y=yy; }
    void Move(float xOff, float yOff) { X+=xOff;Y+=yOff; }
    float GetX() {return X; }
    float GetY() {return Y; }
private:
    //私有成员函数
    float X,Y;
};
class Rectangle: public Point     //派生类 Rectangle 的定义
{
public:
    //新的公共成员函数
    void InitR(float x, float y, float w, float h) {
        InitP(x,y);W=w;H=h;
        //调用基类的公共成员函数
    }
    float GetH() {return H; }
    float GetW() {return W; }
private: //新的私有数据
    float W,H;
};
//Rectangle.h结束
```

在这里，首先声明了基类 Point。派生类 Rectangle 继承了 Point 类所有的成员，构造函数和析构函数除外。派生类的成员是继承自基类的成员与新成员之和。继承模式是公有的，因此基类的公共成员在派生类中保留了它们的属性，并且可以被派生类的成员函数和对象访问（例如，派生类中的成员函数 InitR 可以调用基类的成员函数 InitP）。另一方面，基类的私有成员（例如基类中的 X 和 Y）无法被派生类的成员函数和对象访问。基类的原始外部接口（例如基类中的函数 GetX() 和 GetY()）现在变为了派生类外部接口的一部分。显然，派生类的新成员之间可以互相访问。

Rectangle 类继承了 Point 类的所有成员，实现了代码的复用。此外，通过添加新成员，Rectangle 类拥有了它自己的新特性，从而扩展了代码。

程序的 `main()` 函数如下所示：

```cpp
//7_1.cpp
#include <iostream>
#include <cmath>
#include "rectangle.h"
using namespace std;
int main()
{
    Rectangle rect; //声明一个 Rectangle 类的对象
    rect.InitR(2,3,20,10); //设置矩形的参数
    rect.Move(3,2); //移动矩形的位置
    cout << "The data of X,Y,W,H:" << endl;
    cout << rect.GetX() << ","; //输出继承自基类的成员
    cout << rect.GetY() << ",";
    cout << rect.GetW() << ",";
    cout << rect.GetH() << endl;
}
//7_1.cpp结束
```

首先创建了一个 Rectangle 类对象。派生类 Rectangle 继承了 Point 类所有的成员，构造函数和析构函数除外。派生类的成员是继承自基类的成员与新成员之和。由于继承模式是公有的，基类的公共成员在派生类中保留了它们的属性，并可以被派生类的成员函数和对象访问（例如，派生类中的成员函数 InitR 可以调用基类的成员函数 InitP）。基类的私有成员（例如基类中的 X 和 Y）无法被派生类的成员函数和对象访问。程序的运行结果如下：

```
The data of X,Y,W,H:
5,5,20,10
```

### 7.2.2 私有继承

如果继承模式为私有，那么在派生类中，从基类继承的公共和保护成员将变为私有成员，但从基类继承的私有成员无法被直接访问。也就是说，在私有继承中，从基类继承的公共和保护成员的访问属性发生了改变——它们在派生类中变为私有成员，派生类的其他成员可以直接访问它们。派生类成员和派生类对象都无法直接访问基类的私有成员。

例 7.2 Point 类的私有继承。

```cpp
//rectangle.h
class Point             //基类 Point 的定义
{
public:
    void InitP(float xx=0, float yy=0) { X=xx;Y=yy; }
    void Move(float xOff, float yOff) { X+=xOff;Y+=yOff; }
    float GetX() {return X; }
    float GetY() {return Y; }
private:
    float X,Y;
};

class Rectangle: private Point     //派生类 Rectangle 的定义
{
public:
    //新的公共成员函数
    void InitR(float x, float y, float w, float h) {
        InitP(x,y);W=w;H=h;
    }
    float GetH() {return H; }
    float GetW() {return W; }
    // 重新声明以允许访问
    void Move(float xOff, float yOff) { Point::Move(xOff,yOff); }
    float GetX() { return Point::GetX(); }
    float GetY() { return Point::GetY(); }
private: //新的私有数据
    float W,H;
};
```

首先创建了一个 Rectangle 类对象。派生类 Rectangle 继承了 Point 类所有的成员，构造函数和析构函数除外。派生类的成员是继承自基类的成员与新成员之和。由于继承模式是私有的，基类的公共成员在派生类中变为私有成员，无法在派生类外部通过派生类对象访问。

程序的运行结果如下：

```
The data of X,Y,W,H:
5,5,20,10
```

