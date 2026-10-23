
// Unbox using a safe cast
int j = safe_cast<int>(obj);                // 42
long k = safe_cast<long>(obj) + 10;         // 52

Console::WriteLine("Values: {0},{1}", j, k);

我们现在进入 C++/CLI 代码，创建一个类层次结构，创建派生类的实例，并在层次结构中进行类型转换。代码中记录了语法，主要亮点如下：

-   继承机制（默认是公有继承）。
-   静态构造函数、默认构造函数、复制构造函数以及其他构造函数。
-   静态成员数据。
-   终结器（看起来像 C++ 析构函数；托管类不需要）。
-   以标准方式设置和获取成员数据的属性语法。
-   抽象类和抽象（无函数体）方法的使用。
-   虚（多态）方法及其重写。

这个列表像是一门迷你课程，但读者理解代码应该没什么困难。作为示例，我们定义基类：

```
#pragma once                         // Prevent multiple inclusion

public ref class Shape abstract       // ref => on heap
{
public:
    Shape() { }                       // Default constructor

    Shape(Shape^ source) { }          // Copy constructor

    // Finaliser
    !Shape() { }

    // Return descriptive string
    virtual String^ ToString() override
    {
        return "Shape";
    }

    // The draw function is abstract because
    // Shape is not concrete. It can't be drawn.
    virtual void Draw() abstract;
};
```

派生类 Point 如下：

```
#pragma once   // Prevent multiple inclusion

#include "Shape.hpp"

public ref class Point: Shape                // Point class derived from
                                         // Shape
{
private:
    double x;                               // Space for x-coordinate
    double y;                               // Space for y-coordinate

    static int numPoints = 0;               // Number of points created
    static Point^ origin=gcnew Point(0.0, 0.0); // Origin point
    static int test;
public:

    /* Constructors */

    // Static constructor
    static Point()
    { // Ctor called prior to when the class is first initialised

        test = 42;
    }

    // Default constructor
    Point(): Shape(), x(0.0), y(0.0)
    {
        numPoints++;
    }

    // Copy constructor
    Point(Point^ source): Shape(source), x(source->x), y(source->y)
    {
        numPoints++;
    }

    // Constructor with coordinates
    Point(double x, double y): Shape(), x(x), y(y)
    {
        numPoints++;
    }

    // Finaliser invoked just before object is garbage collected
    !Point()
    {
        numPoints--;   // Decrease counter
    }

    // Return the number of created points
    // Note, in static members you can't use 'this'
    static int GetPoints()
    {
        return numPoints;
    }
}
```

```
/* Properties */

// Access the x-coordinate
property double X
{
    double get()
    {
        return x;
    }

    void set(double x)
    {
        this->x=x;
    }
}

// Access the y-coordinate
property double Y
{
    double get()
    {
        return y;
    }

    void set(double y)
    {
        this->y=y;
    }
}

// Read only property to access origin point
static property Point^ Origin
{
    Point^ get()
    {
        return origin;
    }
}

// Return descriptive string
virtual String^ ToString() override
{
    return Shape::ToString()
        + String::Format(": Point ({0}, {1})", x, y);
}

// Draw point, emulated with printing text
virtual void Draw() override
{
    System::Console::WriteLine("Draw Point ({0}, {1})", x, y);
}
};
```

测试程序如下：

```
using namespace System;

#include "Point.hpp"

int main()
{
    Point^ p=gcnew Point(1.0, 3.0);      // Create Point
    // Shape^ s=gcnew Shape();             // can't be created
    Shape^ sp=gcnew Point(4.5, 3.1);

    p->Draw();                            // Prints 'Draw Point(1.0, 3.0)'
    sp->Draw();                            // Prints 'Draw Point(4.5, 3.1)'

    // Casting
    Shape^ sp2 = gcnew Point(1.0, 2.0);
    try
    {
        Point^ pt = safe_cast<Point^>(sp2);
        Console::WriteLine(L"Coordinates: {0},{1} ", pt->X, pt->Y);
    }
    catch (System::InvalidCastException^ e)
    {
        Console::WriteLine("Cast failed");
    }

    return 0;
}
```

这段代码可供学习和运行，并可推广到其他问题。

## 27.3 类型

*公共类型系统*（CTS）是 *公共语言运行时*（CLR）中的关键组件。它允许开发人员创建多语言应用程序。具体而言，它具有以下功能：

-   a) 一个面向对象的数据模型，用于支持所有 .NET 编程语言的数据类型。
-   b) 一组约束条件，.NET 编程语言的数据类型必须满足这些约束，才能与其他 .NET 语言进行交互。
-   c) 一个框架，允许 .NET 语言相互操作并确保数据类型安全。

两种主要数据类型是值类型和引用类型。*值类型*（例如 int、float 和 double）以及用户定义的值类型存储为引用类型。*引用类型*（例如数组、类和句柄）作为对数据类型位置的引用存储在托管堆上。

C++/CLI 中的 CTS 类型与 C# 中的类型相似，但有一些新增：

-   表示整数、实数、布尔值和字符的内置值类型。
-   一维和多维数组。
-   引用类类型：这些是用户定义的类型。
-   委托：委托是一种保存对方法引用的类型。
-   接口类型：与抽象类类似，不同之处在于接口只能包含公共纯虚方法，并且不能包含数据。
-   句柄类型：这是对某个类型的引用，类似于原生 C++ 指针，但数据句柄不能进行操作，换句话说，与原生 C++ 指针相比，不能对句柄进行偏移量的加减。
-   用户定义的值类型：对标准（基本）值类型的用户定义扩展。
-   枚举：命名整数常量的列表。
-   装箱值类型：对值类型的临时引用，允许将其放置在托管堆上。

## 27.4 内存管理

开发人员对内存管理应该不会陌生。例如，.NET Framework 有一个垃圾回收器，负责从托管堆中移除对象。因此，当对象不再被使用时，开发人员无需担心将对象从 CLI（托管）堆中移除。原生 C++ 使用非托管运行时（CRT）堆，在这种情况下，程序员有责任显式地从堆内存中移除对象。换句话说，原生 C++ 使用（不安全的）指针，而 C++/CLI 同时支持不安全指针和句柄。句柄是对某个类型的引用。

.NET 垃圾回收由 CLR 自动处理。在某些情况下，可能需要修改垃圾回收的频率，为此我们可以使用 System::GC 类来触发垃圾回收过程。由于垃圾回收器仅处理托管内存，不感知非托管内存，它会低估调度垃圾回收的紧迫性，例如，一个托管对象分配了大量非托管内存时就是如此。因此，我们需要一种机制，在分配了非托管内存之后以及释放了这些非托管内存之后，通知垃圾回收器。为此，System::GC 类提供了以下静态方法：

-   GC::AddMemoryPressure()：通知运行时，在调度垃圾回收时，应考虑大块非托管内存的分配。
-   GC::RemoveMemoryPressure()：通知运行时，大块非托管内存已被释放，不再需要在垃圾回收时加以考虑。

使用示例如下：

```
// Allocate some unmanaged memory
long long N = 1e8;
double* darr = new double[N];
```
