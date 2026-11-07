

```cpp
q->print();
cout << endl;                    //Line 5
r->print();                      //Line 6
                                 //Line 7
cout << "*** Calling the function callPrint ***"
     << endl;                    //Line 8
callPrint(q);                    //Line 9
cout << endl;                    //Line 10
callPrint(r);                    //Line 11
    return 0;
}

void callPrint(petType *p)
{
    p->print();
}
```

### 示例运行：

```text
Name: Lucky
Name: Tommy, Breed: German Shepherd
*** Calling the function callPrint ***
Name: Lucky
Name: Tommy, Breed: German Shepherd
```

前述示例表明，如果形参（比如类类型的 *p*）是引用参数或指针，并且 *p* 使用基类的虚函数，那么我们可以有效地将派生类对象作为实参传递给 *p*。

然而，如果 *p* 是 *值参数*，那么即使 *p* 使用虚函数，这种将派生类对象作为实参传递给 *p* 的机制也不起作用。回想一下，如果形参是 *值参数*，则实参的值会被复制到形参中。因此，如果形参是 *类类型*，则实际对象的成员变量会被复制到形参相应的成员变量中。

假设我们有上面的类——即 `petType` 和 `dogType`。考虑以下函数定义：

```cpp
void callPrint(petType p)  //p is a value parameter
{
    p.print();
}
```

进一步假设我们有以下声明：

```cpp
dogType dog;
```

对象 `dog` 有两个成员变量：`name` 和 `breed`。成员变量 `name` 继承自基类。考虑以下函数调用：

```cpp
callPrint(dog);
```

在此语句中，因为形参 `p` 是值参数，所以 `dog` 的成员变量会被复制到 `p` 的成员变量中。然而，因为 `p` 是 `petType` 类型的对象，所以它只有一个成员变量。因此，只有 `dog` 的成员变量 `name` 会被复制到 `p` 的成员变量 `name` 中。此外，语句：

`p.print();`

在函数体中，将导致执行 `class petType` 的成员函数 `print`。

以下程序的输出进一步说明了这一概念。（和之前一样，我们假设 `class petType` 的定义在头文件 `petType.h` 中，`class dogType` 的定义在头文件 `dogType.h` 中。）

```cpp
//Chapter 14: Virtual Functions and Value Parameters
#include <iostream>
#include "petType.h"
#include "dogType.h"

using namespace std;

void callPrint(petType p);

int main()
{
    petType pet("Lucky");                         //Line 1
    dogType dog("Tommy", "German Shepherd");     //Line 2

    pet.print();                                   //Line 3
    cout << endl;                                  //Line 4
    dog.print();                                   //Line 5

    cout << "*** Calling the function callPrint ***" //Line 6
         << endl;
    callPrint(pet);                                //Line 7
    cout << endl;                                  //Line 8
    callPrint(dog);                                //Line 9
    cout << endl;                                  //Line 10

    return 0;
}

void callPrint(petType p)  //p is a value parameter
{
    p.print();
}
```

### 示例运行：

```text
Name: Lucky
Name: Tommy, Breed: German Shepherd
*** Calling the function callPrint ***
Name: Lucky
Name: Tommy
```

仔细查看第7行和第9行语句的输出（输出的最后两行）。在第9行中，因为形参 `p` 是值参数，所以 `dog` 的成员变量会被复制到 `p` 相应的成员变量中。然而，因为 `p` 是 `petType` 类型的对象，所以它只有一个成员变量。因此，只有 `dog` 的成员变量 `name` 会被复制到 `p` 的成员变量 `name` 中。此外，函数 `callPrint` 中的语句 `p.print();` 执行的是 `class petType` 的函数 `print`，而不是 `class dogType` 的函数 `print`。因此，输出的最后一行只显示 `name`（`dog` 的成员变量）的值。

> **注意**
>
> 基类类型的对象不能传递给派生类类型的形参。

在结束本节之前，我们讨论另一个与虚函数相关的问题。

假设 `class petType` 的定义和之前一样，而 `class dogType` 的定义稍作修改如下：

```cpp
class dogType: public petType
{
public:
    void print();
    void setBreed(string b = "");
    dogType(string n = "", string b = "");

private:
    string breed;
};
```

考虑以下语句：

```cpp
petType pet("Lucky");
dogType dog("Tommy", "German Shepherd");
```

```cpp
pet = dog;
```

C++ 允许这种类型的赋值，即派生类对象的值可以被复制到基类对象中。（注意，反向语句，即 `dog = pet;` 是不允许的。）现在，因为对象 `pet` 只有一个数据成员（`name`），而对象 `dog` 有两个数据成员（`name` 和 `breed`），所以只有 `dog` 的数据成员 `name` 的值会被复制到 `pet` 的数据成员 `name` 中。这称为 **切片问题**。以下语句将导致编译时错误。

```cpp
pet.setBreed("Siberian Husky");
```

C++ 提供了一种方法，通过使用指针，将 `dogType` 对象当作 `petType` 对象处理，而不会丢失 `class dogType` 的额外属性。

例如，假设你有以下语句：

```cpp
petType *pet;
dogType *dog;

dog = new dogType("Tommy", "German Shepherd");
dog->setBreed("Siberian Husky");

pet = dog;
```

在这种情况下，语句 `pet->print();` 的输出是：

```text
Name: Tommy, Breed: Siberian Husky
```

## 类与虚析构函数

对于带有指针成员变量的类，建议这些类应具有析构函数。当类对象超出作用域时，析构函数会自动执行。因此，如果对象创建了动态内存空间，就可以设计析构函数来释放该内存空间。如果将派生类对象传递给基类类型的形参，则无论该派生类对象是按引用还是按值传递，基类的析构函数都会执行。然而，从逻辑上讲，当派生类对象超出作用域时，应执行派生类的析构函数。

为纠正此问题，基类的析构函数必须是虚函数。基类的 **虚析构函数** 会自动使派生类的析构函数成为虚函数。当派生类对象传递给基类类型的形参时，当该对象超出作用域时，会执行派生类的析构函数。执行完派生类的析构函数后，会执行基类的析构函数。因此，当派生类对象被销毁时，该派生类对象中属于基类的部分（即从基类继承的成员）也会被销毁。

如果基类包含虚函数，请将基类的析构函数设为虚函数。

## 抽象类与纯虚函数

前面几节讨论了虚函数。除了强制函数进行运行时绑定之外，虚函数还有另一种用途，本节将讨论这一点。第13章讨论了面向对象设计（OOD）的第二条原则——继承。通过继承，我们无需从头设计就能派生新类。派生类除了继承基类已有的成员外，还可以添加自己的成员，并重新定义或重写基类的公有和受保护成员函数。基类可以包含你希望每个派生类实现的函数。在许多场景中，我们希望某个类充当若干派生类的基类；然而，该基类可能包含某些在基类中没有有意义定义的函数。

让我们考虑第13章给出的 **类** shape。正如该章所述，从 **类** shape 可以派生其他 **类**，例如 rectangle、circle、ellipse，

