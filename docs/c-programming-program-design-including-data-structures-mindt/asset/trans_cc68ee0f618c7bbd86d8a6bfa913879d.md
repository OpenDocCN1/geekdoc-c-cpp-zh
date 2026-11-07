

```cpp
    rectangleType& setWidth(double w);
        //Function to set the width.
        //Postcondition: width = w
        //    After setting the width, a reference to the object,
        //    that is, the address of the object, is returned.

    rectangleType(double l = 0.0, double w = 0.0);

    private:
        double length;
        double width;
    };
```

注意，类 `rectangleType` 的定义与第 11 章给出的相同，不同之处在于，这里在类 `rectangleType` 的定义中，我们添加了函数 `setLength` 和 `setWidth`，以分别设置矩形的长度和宽度，然后返回整个对象。我们还用带默认参数的构造函数替换了原来的构造函数。

函数 `print`、`setDimension`、`getLength`、`getWidth`、`area` 和 `perimeter` 的定义与之前相同。带默认参数的构造函数的定义与带参数的构造函数的定义相同。函数 `setLength` 和 `setWidth` 的定义如下：

```cpp
    rectangleType& rectangleType::setLength(double l)
    {
        length = l;
        return *this;
    }

    rectangleType& rectangleType::setWidth(double w)
    {
        width = w;
        return *this;
    }
```

下面的程序展示了如何使用类 `rectangleType`。（我们假设类 `rectangleType` 的定义在文件 `rectangleType.h` 中。）

```cpp
    //Test Program: class rectangleType

    #include <iostream>                                      //Line 1
    #include <iomanip>                                       //Line 2
    #include "rectangleType.h"                               //Line 3

    using namespace std;                                     //Line 4

    int main()                                               //Line 5
    {                                                        //Line 6
        rectangleType myRectangle;                           //Line 7
        rectangleType yourRectangle;                         //Line 8

        cout << fixed << showpoint << setprecision(2);       //Line 9
```

## 类的友元函数

类的**友元函数**是该类的非成员函数，但可以访问该类的所有成员（公有或非公有）。要使一个函数成为某个类的友元，保留字 `friend` 应位于函数原型之前（在类定义中）。单词 `friend` 只出现在类定义中的函数原型里，而不出现在 `friend` 函数的定义中。换句话说，友元关系总是由类授予的，而不是由函数取得的。

考虑以下语句：

```cpp
class classIllusFriend
{
    friend void two(/*parameters*/);
    .
    .
    .
};
```

在类 `classIllusFriend` 的定义中，`two` 被声明为类 `classIllusFriend` 的友元。也就是说，它是类 `classIllusFriend` 的非成员函数。当你编写函数 `two` 的定义时，任何类型为 `classIllusFriend` 的对象——只要该对象在函数 `two` 的定义中作为 `two` 的局部变量或 `two` 的形参出现——都可以在函数 `two` 的定义中访问其私有成员。（示例 13-4 说明了这一概念。）此外，由于友元函数不是类的成员，其声明可以放在类的私有、受保护或公有部分中。不过，这类声明通常放在任何成员函数声明之前。

### `friend` 函数的定义

编写 `friend` 函数的定义时，类名和作用域解析运算符不会出现在函数头中 `friend` 函数名之前，因为它不是类的成员函数。另外，请记住，单词 `friend` 不会出现在 `friend` 函数定义的头中。因此，前面 `class classIllusFriend` 中函数 `two` 的定义为：

```cpp
void two(/*parameters*/)
{
    .
    .
    .
}
```

当然，我们会将 `friend` 函数的定义放在实现文件中。

下一节将说明，当我们为特定类重载某些运算符时，成员函数与非成员函数（`friend` 函数）之间的区别。

下面的示例展示了 `friend` 函数如何访问类的 `private` 成员。

### 示例 13-4

在这个示例中，我们使用类 `rectangleType` 来说明 `friend` 函数如何工作。在下面的定义中，我们不对函数进行文档说明。该类的完整定义可在本书附带的网站上获取。

```cpp
class rectangleType
{
    friend void rectangleFriend(rectangleType recObject);
public:
    void setDimensions(double l, double w);
    double getLength() const;
    double getWidth() const;
    double area() const;
    double perimeter() const;
    void print() const;

    rectangleType();
    rectangleType(double l, double w);

private:
    double length;
    double width;
};
```

在类 `rectangleType` 的定义中，`rectangleFriend` 被声明为 `friend` 函数。假设函数 `rectangleFriend` 的定义为：

```cpp
void rectangleFriend(rectangleType recFriendObject)
{
    cout << "recFriendObject area: " << recFriendObject.area()
         << endl;

    recFriendObject.length = recFriendObject.length + 5;
    recFriendObject.width = recFriendObject.width + 5;

    cout << "After increasing length and width by 5 units "
         << " each, \n    recFriendObject area: "
         << recFriendObject.area() << endl;
}
```

函数 `rectangleFriend` 包含一个类型为 `rectangleType` 的（值）形参 `recFriendObject`。（注意，由于 `rectangleType` 是值参数，它会复制其实际参数的值。）第一条语句输出对象 `recFriendObject` 的面积。接下来的两条语句将 `recFriendObject` 的长度和宽度增加 5 个单位。下一条语句输出由新的长度和宽度得到的对象 `recFriendObject` 的面积。注意，`rectangleFriend` 访问其 `private` 成员变量 `length` 和 `width`，并将它们的值增加 5 个单位。如果 `rectangleFriend` 没有被声明为类 `rectangleType` 的 `friend` 函数，那么这条语句将导致语法错误，因为对象不能直接访问其 `private` 成员。

类 `rectangleType` 其余函数和构造函数的定义如第 11 章所述。

现在考虑以下函数 `main` 的定义：

```cpp
#include <iostream> //Line 1
#include <iomanip> //Line 2
#include "rectangleType.h" //Line 3

using namespace std; //Line 4

int main() //Line 5
{ //Line 6
    rectangleType myYard(25, 18); //Line 7

    cout << fixed << showpoint << setprecision(2); //Line 8

    cout << "myYard area: " << myYard.area()
         << endl; //Line 9

    cout << "Passing object myYard to the friend "
         << "function rectangleFriend." << endl; //Line 10

    rectangleFriend(myYard); //Line 11

    return 0; //Line 12
} //Line 13
```

### 示例运行

```text
myYard area: 450.00
Passing object myYard to the friend function rectangleFriend.
recFriendObject area: 450.00
After increasing length and width by 5 units each,
    recFriendObject area: 690.00
```

大部分输出不言自明。第 9 行的语句输出 `myYard` 的面积。第 11 行的语句调用函数 `rectangleFriend`（类 `rectangleType` 的 `friend` 函数），并将对象 `myYard` 作为实际参数传递。注意，函数 `rectangleFriend` 生成输出的最后三行。

在本章后面，你将了解到，对于某个类，流插入运算符和流提取运算符只能重载为 `friend` 函数。

## 运算符函数作为成员函数和非成员函数

本章开头指出，在类定义中包含运算符函数时必须遵循某些规则。本节介绍这些规则。

大多数运算符函数既可以是成员函数，也可以是非成员函数——即类的友元函数。要使运算符函数成为类的成员函数或非成员函数，请记住以下事项：

- 1. 为某个类重载运算符 `()`、`[]`、`->` 或 `=` 中任一运算符的函数，必须声明为该类的成员。
- 2. 假设为某个类——比如 `opOverClass`——重载了运算符 `op`。（这里，`op` 表示可以重载的运算符，例如 `+` 或 `>>`。）
  - a. 如果 `op` 的最左操作数是不同类型的对象（即不是 `opOverClass` 类型），那么为 `opOverClass` 重载运算符 `op` 的函数必须是非成员函数——即类 `opOverClass` 的友元。
  - b. 如果为类 `opOverClass` 重载运算符 `op` 的运算符函数是类 `opOverClass` 的成员，那么在对 `opOverClass` 类型的对象应用 `op` 时，`op` 的最左操作数必须是 `opOverClass` 类型。

在类定义中包含运算符函数时，必须遵循这些规则。

你将在本章后面看到，为某个类重载插入运算符 `<<` 和提取运算符 `>>` 的函数必须是非成员函数——即该类的 `friend` 函数。

除前面提到的某些运算符外，运算符既可以重载为成员函数，也可以重载为非成员函数。下面的讨论展示了这两类函数之间的区别。

为便于讨论运算符重载，我们将使用下面给出的类 `rectangleType`。（尽管第 11 章定义了这个类，但第 11 章并不是本章的先修内容。为便于参考，我们重现该类的定义以及成员函数的定义。）

```cpp
class rectangleType
{
public:
    void setDimension(double l, double w);
        //Function to set the length and width of the rectangle.
        //Postcondition: length = l; width = w;

    double getLength() const;
        //Function to return the length of the rectangle.
        //Postcondition: The value of length is returned.
```

