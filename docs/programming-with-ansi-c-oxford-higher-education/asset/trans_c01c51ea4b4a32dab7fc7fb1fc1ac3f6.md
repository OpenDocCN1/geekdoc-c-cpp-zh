

> 不可能存在虚构造函数，而虚析构函数是可能的。

使用指向基类的指针或对基类的引用。这意味着这些函数必须同时是基类和派生类的成员。

7. 多态只能通过指向基类的指针（或引用）来实现，使用对象不可能实现。Ring.draw() 将始终调用 Ring 的 draw()，而不会调用 Shape 的 draw()，反之亦然。这称为虚函数的静态调用。

8. 虚构造函数是不可能的。构造派生类对象需要在内部专门构造基类子对象。显然，它们的构造函数不可能是虚的。（更确切地说，派生类对象的构造函数也会调用基类的构造函数）当一个对象被删除时，可以有一个虚析构函数来销毁它；因此，delete <pointer> 操作对于所指向的对象有效，无论指针类型如何。此时，允许在基类指针指向派生类对象时提供对整个派生类对象的删除（否则它只会删除派生类的基类子对象）。无论如何，使用虚析构函数以避免内存泄漏是一个好主意。

## 10.7.1 静态绑定与动态绑定

虚函数调用机制有时被称为动态绑定。链接是编译后将 main() 中调用的函数“连接”起来以创建可执行文件的过程。链接器是执行链接的实体。在链接时，当使用指向基类的指针调用虚函数时，链接器不知道该调用哪个函数。它在运行时通过查看指针的内容来决定。因此，虚函数调用直到被调用时才会被解析。这意味着这类函数在运行时才被链接。这也意味着使用虚函数的程序会运行得稍慢一些，因为它涉及两个步骤，即链接和执行。

如果没有使用虚函数，函数将在链接时（编译之后、创建可执行文件之前）被链接，并且它们的调用在那时被解析。这里没有动态绑定那样的运行时开销。这种绑定称为静态绑定。

> 静态绑定发生在编译时，而动态绑定发生在运行时。

```cpp
#include <iostream>
using namespace std;

class BaseClass
{
public:

// When called, the function tells which class it is part of
void testWhichClass()
{
cout << "BaseClass" << endl;
}
};

class DerivedClass : public BaseClass
{
public:

// When called, the function tells which class it is part of
void testWhichClass()
{
cout << "DerivedClass" << endl;
}
};

int main()
{
BaseClass *bptr;
DerivedClass d;
bptr = &d;
bptr->testWhichClass(); // This will call the function of DerivedClass because of polymorphism
return 0;
}
```

```cpp
public:
// The same function is also defined in the derived class
void testWhichClass()
{
    cout << "DerivedClass" << endl;
};
void findClass(BaseClass & SomeClass)
{
    /* Whenever some class reference is passed to this function,
    it is accepted as a base class reference */
    SomeClass.testWhichClass();
    /* This checks which class is the SomeClass passed to this function */
}
int main()
{
    DerivedClass D;
    findClass(D);
    getchar();
}
```

```text
Output
BaseClass
```

传递了一个派生类对象，但输出显示 BaseClass。如果将函数 testWhichClass() 改为 virtual，输出将是 DerivedClass。

> **注意：**对于非虚函数，当基类引用指向派生类对象时，它仍然调用基类函数。当函数被定义为 virtual 时，指向派生类的同一引用将调用派生类函数。

## 10.7.2 虚函数的默认参数

虚函数的默认参数并不会像预期的那样表现。考虑程序 10.3：

### 程序 10.3 默认参数在虚函数中表现不正常

```cpp
//DefArgs.cpp
#include <iostream>
using namespace std;
class Shape
{
    int LineStyle;
    int FillColour;
public:
    virtual int draw(int size = 100)
    /* It will not work as expected. The default argument value will always depend on the pointer type and not the content. */
    {
        cout << "Shape is drawn \n";
        return size;
    }
};

class Circle : public Shape
{
    int Radius;
    int CentrePointX;
    int CentrePointY;
public:
    int draw(int size = 200)
    {
    cout << "Circle is drawn \n";
    return size;
    }
};

int main()
{
    Shape SomeShape, *PtrShape;
    Circle Ring;
    SomeShape.draw();
    Ring.draw();
    PtrShape = &Ring;
    /* Base class pointer pointing to derived class object */
    int DrawSize = PtrShape->draw();
    // This draws a circle
    cout << "Draw size using base class pointer: " << DrawSize << "\n";
    /* This displays 100 instead of 200, as the pointer type is Base */
    Circle *PtrCircle = &Ring;
    DrawSize = PtrCircle->draw();
    /* Now, we are using a derived class pointer to
    point to a derived class object */
    cout << "Draw size using derived class pointer: " << DrawSize << "\n";
    /* This will display 200, as the pointer type is Derived */
}
```

```text
Output
Shape is drawn
Circle is drawn
Circle is drawn
Draw size using base class pointer: 100
Circle is drawn
Draw size using derived class pointer: 200
```

### 程序如何工作

当执行以下语句时

```cpp
int DrawSize = PtrShape->draw();
cout << "Draw size using base class pointer: " << DrawSize << "\n";
```

它显示 100 而不是 200。当执行以下语句时

```cpp
Circle *PtrCircle = &Ring;
DrawSize = PtrCircle->draw();
cout << "Draw size using derived class pointer: " << DrawSize << "\n";
```

它正确显示 200。

> 当我们使用基类指针指向派生类对象时，将采用基类函数的默认值。这里，被执行的函数是正确的，但使用的是基类的默认值。另一方面，当我们使用派生类指针时，将采用派生类函数的默认值。

### 占位默认参数的补救办法

程序 10.3 表明，默认参数不能像普通函数那样使用。这里的解决方案是提供一个在两个类中都初始化了的局部变量，然后使用默认参数。如果需要默认参数，可以将这些局部变量的值赋给它们，如程序 10.4 所示。

我们只需要检查用户是否提供了值，如果没有，则从局部变量而不是默认参数中获取信息。通过保留一个占位默认参数，可以轻松检查用户是否提供了值。如果参数等于占位值，则说明用户没有提供该参数，此时可以从局部变量中获取值。

### 程序 10.4 使用占位默认参数作为解决方案

```cpp
//SolutionDefArgs.cpp
#include <iostream>
using namespace std;
class Shape
{
    int LineStyle;
    int FillColour;
public:
    virtual int draw(int size = 1)
    /* The size parameter is dummy; it is there to check whether the default argument is provided */
    {
        cout << "Shape is drawn\n";
        int ShapeSize = 100;
        /* This is to check whether the default argument is provided with the given value 100 */
        if(size == 1)
            size = ShapeSize;
        return size;
    }
};
class Circle : public Shape
{
    int Radius;
    int CentrePointX;
    int CentrePointY;
public:
    int draw(int size = 1)
    {
        cout << "Circle is drawn\n";
        int CircleSize = 200;
        if(size == 1)
            size = CircleSize;
        return size;
    }
};
```

