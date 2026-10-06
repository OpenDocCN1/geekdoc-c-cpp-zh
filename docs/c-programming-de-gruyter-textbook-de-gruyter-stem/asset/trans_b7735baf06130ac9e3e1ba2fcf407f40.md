

## 5.3 类的静态成员 — 169

| 点 |
| :--- |
| - X : int |
| - Y : int |
| - countP : int = 0 |
| + Point(xx : int = 0, yy : int = 0) |
| + GetX() : int |
| + GetY() : int |
| + Point(p : int &) |
| <<static>> + GetC() : void |

![](img/5618306d085ac1bac8275d6c4c5bbf2a_186_0.png)

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

## 5 数据共享与保护

与示例 5.4 相比，我们只在类的定义中将 `GetC()` 更改为静态成员函数。然后，我们可以在 `main` 函数中同时使用类名和对象名来调用 `GetC()`。

该程序的结果与示例 5.4 相同。与示例 5.4 相比，静态成员函数的优势是它是独立于对象的，因此我们可以直接访问静态数据。注意使用静态数据成员：如果你想通过非静态函数访问静态数据，则应该使用非静态函数，且非静态函数的定义应该与静态成员的初始化在同一个源文件中。我们为什么要这样做？这是因为静态数据在被访问之前必须初始化，而编译器只能保证在调用同一源文件中定义的任何非静态函数之前初始化类的静态成员。在这种情况下，我们将看到一个由多个源文件组成项目中，静态成员的初始化会导致意想不到的错误。

## 5.4 类友元（Friend of Class）

将数据和函数封装成类可以实现面向对象程序设计的巨大优势。但封装并不是无所不能的。现在考虑一个我们熟悉的 `Point` 类简单示例，其中每个对象代表一个“点”。如果我们想计算任意两个点之间的距离，应该如何设计这个函数？

如果我们把距离计算器设计为类外的普通函数，我们就无法反映函数与“点”之间的关系，而且类外的函数无法直接引用“点”的私有成员，这使得计算变得不方便。从语法角度来看，这很难实现，因为距离是两个点之间的关系，它不属于任何类。换句话说，将函数设计为非静态成员或静态成员将始终影响程序的可读性。我们在第 4 章中使用了类的组合，两个 `Point` 类对象组合成一个 `Line`（线段），而 `Line` 类具有计算线段长度的函数。然而，`Line` 类是线段的抽象。如果我们面临的问题是需要频繁计算任意两点之间的距离，那么每次计算距离时都必须创建一个 `line` 对象。这是不方便的并且会影响程序的可读性。

因此，我们需要一个与 `Point` 类有特殊关系的函数类。请看以下代码：

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

