
# 5 数据共享与保护

## 5.3 类的静态成员

虽然每个对象的属性值可能不同。这种属性在面向对象的方法中被称为“实例属性”，在 C++ 程序中由类的非静态数据成员表示。例如，在上面的对象中 `employee` 类的 `EmpNo`、`ID` 和 `name` 都是由非静态数据成员表示的实例属性。非静态数据成员在类的每个对象中都有一个拷贝，使得对象与同类的其他对象有所不同。如果在面向对象的方法中存在“类属性”的概念，即属于整个类而不属于任何特定对象的属性，那么我们可以使用 `static` 关键字将其声明为静态成员。静态成员在类中只有一个拷贝，它被该类的所有对象保护和使用，以实现同类不同对象之间的数据共享。类属性是表示某一类中所有对象共同特征的数据项。它的属性值对于所有对象实例来说都是相同的。简而言之，如果我们把一个“类”比作工厂，把工厂制造的产品比作产品，那么静态成员将存储在工厂中并属于工厂，而不属于每个产品。

静态数据成员具有静态生命周期。因为静态数据不属于任何对象，我们只能通过类名来访问它，通用方法是“类名::标识符”。我们只在静态数据成员的定义中对其进行引用声明，而定义声明必须在文件作用域的某处使用类名限定来完成，初始化也可以在定义期间完成。UML 语言用下划线表示数据成员表示静态数据成员。我们可以在下面的示例找到静态数据成员的使用。

### 示例 5.4：带有静态数据成员的 Point 类

该程序修改自第 4 章中的 `Point` 类。它引入了一个静态数据成员 `countP` 用来统计 `Point` 对象的数量。包含静态数据成员 `countP` 的 `Point` 类 UML 图如图 5.2 所示。

| Point |
| :--- |
| - X : int |
| Y : int |
| - countP : int = 0 |
| +Point(xx : int = 0, yy : int = 0) |
| + GetX() : int |
| + GetY() : int |
| + Point(p : Point &) |
| + GetC() : void |

> 图 5.2：包含静态数据成员的 Point 类 UML 图。

```cpp
//5_4.cpp
#include <iostream>
using namespace std;

class Point                        //Point 类的定义
{
    public:
        //外部接口
        Point(int xx=0, int yy=0){ X=xx; Y=yy; countP++; } //构造函数
        Point(Point &p);                    //拷贝构造函数
        ~Point(Point &p){ countP--; }
        int getX() { return X; }
        int getY() { return Y; }
        void getC(){ cout<<countP<<endl; } //输出静态
        //数据成员
    private:
        //私有数据成员
        int X,Y;
        static int countP;                 //静态数据的引用声明
        //成员，用于记录点的数量
};

Point::Point(Point &p) {
    X=p.X;
    Y=p.Y; //在构造函数中累加 countP，所有对象
    //保持相同的 countP
}
int Point::countP=0;                //静态数据成员的定义声明和初始化
//并用类名限定

int main() {
    //主函数
    Point A(4,5);                       //定义对象 A，它的构造函数将使
    //countP 加 1
    cout<<"A:"<<A.getX()<<endl; 
    Point B(A);                         //定义对象 B，它的构造函数将使
    //countP 加 1
    cout<<"B:"<<B.getX()<<endl;
    A.getC();                           //输出静态
    B.getC();                           //输出静态
}
```

在上面的示例中，静态成员 `countP` 是私有的，我们只能通过类名来访问它，通用方法是“类名::标识符”。我们只在静态数据成员的定义中对其进行引用声明，而定义声明必须在文件作用域的某处使用类名限定来完成，初始化也可以在定义期间完成。

## 5.3 类的静态成员 — 169

```cpp
public:
//外部接口
Point(int xx=0, int yy=0) {X=xx;Y=yy;countP++;} //构造函数
Point(Point &); //拷贝构造函数
~Point() { count--; }
int GetX() { return X; }
int GetY() { return Y; }
static void GetC() {cout << "Object id=" << countP << endl; }
//静态函数成员
private:
//私有数据成员
int X,Y;
static int countP; //静态数据成员的
引用声明
;
Point::Point(Point &p)
{
X=p.X;
Y=p.Y;
countP++;
}
int Point::countP=0;
//静态数据成员的
定义声明
//静态数据成员
//初始化，使用类名限定符
int main()
{
//主函数
Point A(4,5);//定义对象 A
cout<<"Point A," <<A.GetX() << "," << A.GetY()";//输出对象的编号，
A.GetC();//对象名引用
Point B(A);//定义对象 B
cout<<"Point B," <<B.GetX() << "," << B.GetY()";//输出对象的数量，
Point::GetC();
//类名引用
}
```

与示例 5.4 相比，我们只在类的定义中将 `GetC()` 更改为静态成员函数。然后，我们可以在 `main` 函数中同时使用类名和对象名来调用 `GetC()`。

该程序的结果与示例 5.4 相同。与示例 5.4 相比，静态成员函数的优势是它是独立于对象的，因此我们可以直接访问静态数据。注意使用静态数据成员：如果你想通过非静态函数访问静态数据，则应该使用非静态函数，且非静态函数的定义应该与静态成员的初始化在同一个源文件中。我们为什么要这样做？这是因为静态数据在被访问之前必须初始化，而编译器只能保证在调用同一源文件中定义的任何非静态函数之前初始化类的静态成员。在这种情况下，我们将看到一个由多个源文件组成项目中，静态成员的初始化会导致意想不到的错误。

## 5.4 类友元（Friend of Class）

将数据和函数封装成类可以实现面向对象程序设计的巨大优势。但封装并不是无所不能的。现在考虑一个我们熟悉的 `Point` 类简单示例，其中每个对象代表一个“点”。如果我们想计算任意两个点之间的距离，应该如何设计这个函数？

如果我们把距离计算器设计为类外的普通函数，我们就无法反映函数与“点”之间的关系，而且类外的函数无法直接引用“点”的私有成员，这使得计算变得不方便。从语法角度来看，这很难实现，因为距离是两个点之间的关系，它不属于任何类。换句话说，将函数设计为非静态成员或静态成员将始终影响程序的可读性。我们在第 4 章中使用了类的组合，两个 `Point` 类对象组合成一个 `Line`（线段），而 `Line` 类具有计算线段长度的函数。然而，`Line` 类是线段的抽象。如果我们面临的问题是需要频繁计算任意两点之间的距离，那么每次计算距离时都必须创建一个 `line` 对象。这是不方便的并且会影响程序的可读性。

因此，我们需要一个与 `Point` 类有特殊关系的函数类。

```cpp
class A
{
public:
    void Display(){cout<<x<<endl;}
    int x(){return x; }
private:
    int x;
};

class B
{
public:
    void Set(int i);
    void Display();
private:
    A a;
};
```

在这种情况下，`B` 类的成员无法访问 `A` 的私有成员 `x`。为了解决这个问题，我们可以让 `A` 成为 `B` 的友元：

```cpp
class A
{
public:
    void Display(){cout<<x<<endl;}
    int x(){return x; }
private:
    int x;
};

class B
{
public:
    void Set(int i);
    void Display();
    friend class A; // 声明 A 是 B 的友元
    A a;
};
```

由于 `A` 是 `B` 的友元，`A` 的成员就可以访问 `B` 的私有成员 `x`：

```cpp
void B::Set(int i) { a.x=i; }
void B::Display() { a.Display(); }
```

或者，我们可以将 `B` 声明为 `A` 的友元：

```cpp
class B
{
public:
    void Set(int i);
    void Display();
private:
    int x;
};

friend class B; // 声明 B 是 A 的友元

class A
{
public:
    void Display(){cout<<x<<endl; }
    int x(){return x; }
private:
    int x;
};
```

这样，`B` 的成员就可以访问 `A` 的私有成员 `x`：

```cpp
void B::Set(int i) { x=i; }
void A::Display() { cout<<x<<endl; }
```

### 5.4.2 友类 (Friend Class)

通过友函数，一个类可以将另一个类声明为它的友。如果类 A 是类 B 的友类，那么类 A 的所有成员函数都是类 B 的友函数，它们可以访问类 B 的私有（private）和保护（protected）成员。友类的声明语法如下：

```cpp
class B
{
  ...
  //类 B 的成员声明
  friend class A; //声明 A 为 B 的友类
  ...
};
```

声明友类是关联类并实现类间数据共享的方法。UML 语言使用 <<friend>> 标识来表示类之间的友谊关系。现在，将本节开头的程序段修改为：类 B 是类 A 的友类，那么 B 的成员函数可以直接访问 A 的私有成员 x。图 5.5 显示了如何使用 UML 图描述类 A 和类 B 之间的友关系：
