
```cpp
{
    rectangleType temp = *this;   //use this pointer to copy
                                  //the value of the object

    //increment the length and width
    length++;
    width++;

    return temp;   //return the old value of the object
}
```

### 将后置自增运算符 ++ 重载为成员函数的通用语法

下面描述将后置自增运算符 ++ 重载为成员函数的通用语法。

**函数原型**（应包含在类定义中）：

```cpp
className operator++(int);
```

**函数定义：**

```cpp
className className::operator++(int u)
{
    className temp = *this;    //use this pointer to copy
                               //the value of the object

    //increment the object

    return temp;  //return the old value of the object
}
```

后置自增运算符也可以重载为类的非成员函数。在这种情况下，运算符函数 `operator++` 有两个参数。将类 `rectangleType` 的后置自增运算符重载为非成员函数的函数定义如下：

```cpp
rectangleType operator++(rectangleType& rectangle, int u)
{
    rectangleType temp = rectangle; //copy rectangle into temp

    //increment the length and width of rectangle
    (rectangle.length)++;
    (rectangle.width)++;

    return temp;    //return the old value of the object
}
```

### 将后置自增运算符 ++ 重载为非成员函数的通用语法

下面描述将后置自增运算符 ++ 重载为非成员函数的通用语法。

### 函数原型（应包含在类定义中）：

```cpp
friend className operator++(className&, int);
```

### 函数定义：

```cpp
className operator++(className& incObj, int u)
{
    className temp = incObj; //copy incObj into temp

    //increment incObj

    return temp;    //return the old value of the object
}
```

自减运算符可以用类似的方式重载，具体细节留作练习。

现在让我们编写类 rectangleType 的定义，并展示运算符函数在类定义中的呈现方式。由于某些运算符既可以重载为成员函数，也可以重载为非成员函数，我们给出类 rectangleType 的两个等价定义。在第一个定义中，自增、自减、算术和关系运算符被重载为成员函数。在第二个定义中，自增、自减、算术和关系运算符被重载为非成员函数。

类 rectangleType 的定义如下：

```cpp
//Definition of the class rectangleType
//The increment, decrement, arithmetic, and relational
//operator functions are members of the class.

#include <iostream>

using namespace std;

class rectangleType
{
    //Overload the stream insertion and extraction operators
    friend ostream& operator<<(ostream&, const rectangleType &);
    friend istream& operator>>(istream&, rectangleType &);

public:
    void setDimension(double l, double w);
    double getLength() const;
    double getWidth() const;
    double area() const;
    double perimeter() const;

    //Overload the arithmetic operators
    rectangleType operator+(const rectangleType &) const;
    rectangleType operator-(const rectangleType &) const;

    //Overload the increment and decrement operators
    friend rectangleType operator++(rectangleType&);
    //pre-increment
    friend rectangleType operator++(rectangleType&, int);
    //post-increment
    friend rectangleType operator--(rectangleType&);
    //pre-decrement
    friend rectangleType operator--(rectangleType&, int);
    //post-decrement

    //Overload the relational operators
    friend bool operator==(const rectangleType&,
                           const rectangleType&);
    friend bool operator!=(const rectangleType&,
                           const rectangleType&);
    friend bool operator<=(const rectangleType&,
                           const rectangleType&);
    friend bool operator>=(const rectangleType&,
                           const rectangleType&);
    friend bool operator<(const rectangleType&,
                          const rectangleType&);
    friend bool operator>(const rectangleType&,
                          const rectangleType&);

public:
    void setDimension(double l, double w);
    double getLength() const;
    double getWidth() const;
    double area() const;
    double perimeter() const;

    //Constructors
    rectangleType();
    rectangleType(double l, double w);

private:
    double length;
    double width;
};
```

为类 `rectangleType` 重载这些运算符的函数定义留作练习。（参见本章末尾的编程练习 1 和 2。）

## 运算符重载：成员函数与非成员函数

前面几节讨论并说明了如何重载运算符。某些运算符必须重载为类的成员函数，而有些必须重载为非成员（友元）函数。那么，对于那些既可以重载为成员函数、也可以重载为非成员函数的运算符，又该如何呢？例如，二元算术运算符 + 既可以重载为成员函数，也可以重载为非成员函数。如果将 + 重载为成员函数，那么运算符 + 可以直接访问其中一个对象的成员变量，并且只需要将一个对象作为参数传递。另一方面，如果将 + 重载为非成员函数，那么必须将两个对象都作为参数传递。当两个对象都作为参数传递时，代码可能会变得更清晰一些。因此，除了要遵守运算符重载的限制之外，将 + 重载为成员函数还是非成员函数只是个人偏好问题。在本章余下部分，如果我们将某个运算符重载为成员函数，那么将其重载为非成员函数将留作练习。

## 类和指针成员变量（再探）

第 12 章介绍了带指针成员变量的类的特殊性。既然我们已经讨论了如何重载各种运算符，为了完整起见，让我们回顾一下带指针成员变量的类的特殊性，以及如何避免这些问题。

回想一下，类上唯一的内置操作是赋值和成员选择。赋值运算符提供数据的逐成员复制。也就是说，一个对象的成员变量被复制到同一类型的另一个对象的对应成员变量中。我们已经看到，这种逐成员复制对于带指针成员变量的类并不适用。带指针成员变量的类可能出现的其他问题，涉及对象离开作用域时释放动态内存，以及按值将类对象作为参数传递。要解决这些问题，带指针成员变量的类必须：

- 1. 显式重载赋值运算符
- 2. 包含复制构造函数
- 3. 包含析构函数

## 运算符重载：最后一点说明

接下来，我们看三个说明运算符重载的示例。在深入这些示例之前，你必须记住以下内容：假设某个运算符 op 为某个类（比如 rectangleType）进行了重载。每当我们对 rectangleType 类型的对象使用运算符 op 时，为类 rectangleType 重载运算符 op 的函数体就会执行。因此，你在该函数体中放入的任何代码都会执行。

## **编程示例：** `ClockType`

![](img/d0be7fc6d804b63484835c6c8bc67a07_994_0.png)

第 10 章定义了一个类 `ClockType`，用于在程序中实现一天中的时间。我们使用函数实现了打印时间、递增时间以及比较两个时间是否相等的操作。本示例重新定义了类 `ClockType`。它还重载了流插入和提取运算符以便于输入和输出，重载了用于比较的关系运算符，以及用于使时间增加一秒的自增运算符。使用类 `ClockType` 的程序要求用户以 `hr:min:sec` 的形式输入时间。
