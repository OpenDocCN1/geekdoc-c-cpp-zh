
回顾一下，如果形参是值参数，实参的值会被复制到形参中。因此，如果形参是`class`类型，实际对象的成员变量会被复制到形参对应的成员变量中。

假设我们有上述这些类——即`petType`和`dogType`。考虑下面的函数定义：

```cpp
void callPrint(petType p)   // p is a value parameter
{
    p.print();
}
```

进一步假设我们有以下声明：

```cpp
dogType dog;
```

对象`dog`有两个成员变量：`name`和`breed`。其中成员变量`name`继承自基类。考虑下面的函数调用：

```cpp
callPrint(dog);
```

在这个语句中，由于形参`p`是值参数，`dog`的成员变量会被复制到`p`的成员变量中。然而，由于`p`是`petType`类型的对象，它只有一个成员变量。因此，`dog`中只有成员变量`name`会被复制到`p`的成员变量`name`中。此外，由于函数体中的语句

```cpp
p.print();
```

将`print`绑定到`petType`对象`p`上，所以执行的是`class` `petType`的成员函数`print`。

下面程序的输出进一步说明了这一概念。（和之前一样，我们假设`class` `petType`的定义位于头文件`petType.h`中，`class` `dogType`的定义位于头文件`dogType.h`中。）

```cpp
//Chapter 12: Virtual Functions and value parameters

#include <iostream>
#include "petType.h"
#include "dogType.h"

using namespace std;

void callPrint(petType p);

int main()
{
    petType pet("Lucky");                 //Line 1
    dogType dog("Tommy", "German Shepherd"); //Line 2

    pet.print();                          //Line 5
    cout << endl;                         //Line 6
    dog.print();                          //Line 7
    cout << "*** Calling the function callPrint ***"    //Line 8
         << endl;                                      //Line 9
    callPrint(pet);                                    //Line 10
    cout << endl;                                      //Line 11
    callPrint(dog);                                    //Line 12
    cout << endl;                                      //Line 13

    return 0;                                          //Line 14
}

void callPrint(petType p)    // p is a value parameter
{
    p.print();
}
```

### 示例输出：

```text
Name: Lucky
Name: Tommy, Breed: German Shepherd
*** Calling the function callPrint ***
Name: Lucky
Name: Tommy
```

仔细观察第9行和第11行中语句的输出（即输出的最后两行）。在第11行中，由于形参`p`是值参数，`dog`的成员变量会被复制到`p`对应的成员变量中。然而，由于`p`是基类型`petType`的对象，它只有唯一的成员变量`name`。因此，`dog`中只有成员变量`name`会被复制到`p`的成员变量`name`中。此外，函数`callPrint`中的语句`p.print()`执行的是基类`petType`的`print`函数，而不是派生类`dogType`的`print`函数。因此，输出的最后一行只显示了`name`的值（即`dog`的成员变量）。

> **注意** 基类对象不能传递给派生类类型的形参，因为它缺少派生类的“部分”。

在结束本节之前，我们来讨论另一个与虚函数相关的问题。

假设`class` `petType`的定义与之前相同，而`class` `dogType`的定义稍微修改如下：

```cpp
class dogType: public petType
{
public:
    void print() const;
    void setBreed(string b = "");
    dogType(string n = "", string b = "");

private:
    string breed;
};
```

考虑下面的语句：

```cpp
petType pet("Lucky");
dogType dog("Tommy", "German Shepherd");
```

```cpp
pet = dog;
```

C++ 允许这种赋值，即派生类对象的值可以复制到基类对象中。（注意，反向语句，即`dog = pet;`是不允许的。）现在，由于对象`pet`只有一个数据成员（`name`），`dog`中只有数据成员`name`的值会被复制到`pet`的数据成员`name`中。这称为**切片问题**。下面的语句将导致编译时错误。

```cpp
pet.setBreed("Siberian Husky");
```

C++ 提供指针作为一种方式，可以将`dogType`对象当作`petType`对象处理，同时不会丢失`class` `dogType`的额外属性。

例如，假设你有以下语句：

```cpp
petType *pet;
dogType *dog;

dog = new dogType("Tommy", "German Shepherd");
dog->setBreed("Siberian Husky");

pet = dog;
```

最后一条语句将`dog`的值（即对对象`dog`的引用）复制到`pet`中。于是指针`pet`指向对象`dog`。因此，语句`pet->print();`的输出为：

```text
Name: Tommy, Breed: Siberian Husky
```

## 类与虚析构函数

对于带有指针成员变量的类，推荐的做法之一是这些类应具有析构函数。当类对象超出作用域时，析构函数会自动执行。因此，如果对象创建了动态内存空间，析构函数可以被设计为释放该内存空间。如果派生类对象被传递给基类类型的形参，无论派生类对象是按引用传递还是按值传递，基类的析构函数都会执行。然而，从逻辑上讲，当派生类对象超出作用域时，应该执行派生类的析构函数。

为了纠正这个问题，基类的析构函数必须是虚的。基类的**虚析构函数**会自动使派生类的析构函数成为虚函数。当派生类对象被传递给基类类型的形参时，当对象超出作用域时，派生类的析构函数会执行。派生类析构函数执行完毕后，基类的析构函数会执行。因此，当派生类对象被销毁时，派生类对象中的基类部分（即从基类继承的成员）也会被销毁。

如果基类包含虚函数，请将基类的析构函数设为虚函数。

## 抽象类与纯虚函数

前面的章节讨论了虚函数。除了强制实现函数的运行时绑定之外，虚函数还有另一个用途，本节将对此进行讨论。第11章讨论了面向对象设计（OOD）的第二条原则——继承。通过继承，我们可以派生新类，而无需从头设计它们。派生类除了继承基类的现有成员外，还可以添加自己的成员，也可以重新定义或覆盖基类的公有和受保护成员函数。基类可以包含我们希望每个派生类都实现的函数。在很多场景下，让一个类充当多个派生类的基类是可取的；然而，派生类可能包含一些在基类中没有有意义的定义的函数。

让我们考虑第11章中给出的`shape`类。正如该章所指出的，你可以从`shape`类派生其他类，例如矩形、圆形、椭圆等。每种形状都共有的一些特性包括：它的中心、使用中心将形状移动到不同位置，以及绘制形状。我们可以将这些特性包含在`shape`类中。例如，`shape`类的定义可以类似于以下形式：

```cpp
class shape
{
public:
    virtual void draw();
        //Function to draw the shape.

    virtual void move(double x, double y);
        //Function to move the shape at the position (x, y).

    .
    .
    .
};
```

由于函数`draw`和`move`的定义是针对特定形状的，每个派生类都可以为这些函数提供适当的定义。请注意，我们将函数`draw`和`move`设置为虚函数，以强制这些函数的运行时绑定。

这种`shape`类的定义要求你编写函数`draw`和`move`的定义。然而，此时并没有要绘制或移动的形状。因此，这些函数体没有代码。一种处理方法是让这些函数体为空。这种方案可行，但有一个缺点。一旦我们编写了`shape`类函数的定义，就可以创建该类的对象并调用空的`draw`和`move`函数。由于没有可操作的形状，我们希望阻止用户创建`shape`类的对象。由此可见，我们希望做到以下两件事——不包含函数`draw`和`move`的定义，并阻止用户创建`shape`类的对象。
