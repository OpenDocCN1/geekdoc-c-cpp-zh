
## 将前置自增运算符 ++ 重载为非成员函数的一般语法

下面介绍将前置自增运算符 ++ 重载为非成员函数的一般语法。

### 函数原型（需包含在类定义中）：

```cpp
friend className operator++(className&);
```

### 函数定义：

```cpp
className operator++(className& incObj)
{
    //increment incObj by 1
    return incObj;
}
```

## 重载后置自增运算符

现在我们讨论如何重载后置自增运算符。与前置自增运算符的情况一样，我们先描述将该运算符重载为类的成员。

让我们为 rectangleType 类重载后置自增运算符。在前置自增和后置自增两种情况下，运算符函数的名称相同——operator++。为了区分前置和后置自增运算符重载，我们在运算符函数的函数头中使用一个哑参数（int 类型）。因此，rectangleType 类后置自增运算符的函数原型为：

```cpp
rectangleType operator++(int);
```

语句：

```cpp
myRectangle++;
```

会被编译器编译为语句：

```cpp
myRectangle.operator++(0);
```

于是带参数的 operator++ 函数被执行。参数 0 仅用于区分前置和后置自增运算符函数。

后置自增运算符先在表达式中使用对象的值，然后递增对象的值。因此，实现该函数所需的步骤如下：

- 1. 保存对象的值——例如保存在 temp 中。
- 2. 递增对象的值。
- 3. 返回保存在 temp 中的值。

rectangleType 类后置自增运算符的函数定义如下：

```cpp
rectangleType rectangleType::operator++(int u)
{
    rectangleType temp = *this;    //use this pointer to copy
                                  //the value of the object

    //increment the length and width
    length++;
    width++;

    return temp;   //return the old value of the object
}
```

## 将后置自增运算符 ++ 重载为成员函数的一般语法

下面介绍将后置自增运算符 ++ 重载为成员函数的一般语法。

### 函数原型（需包含在类定义中）：

```cpp
className operator++(int);
```

### 函数定义：

```cpp
className className::operator++(int u)
{
    className temp = *this;       //use this pointer to copy
                                  //the value of the object
    //increment the object

    return temp;  //return the old value of the object
}
```

后置自增运算符也可以重载为类的非成员函数。在这种情况下，运算符函数 operator++ 有两个参数。将 rectangleType 类的后置自增运算符重载为非成员函数的函数定义如下。

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

## 将后置自增运算符 ++ 重载为非成员函数的一般语法

下面介绍将后置自增运算符 ++ 重载为非成员函数的一般语法。

### 函数原型（需包含在类定义中）：

```cpp
friend className operator++(className&, int);
```

### 函数定义：

```cpp
className operator++(className& incObj, int u)
{
    className temp = incObj;  //copy incObj into temp

    //increment incObj

    return temp;  //return the old value of the object
}
```

自减运算符可以用类似方式重载，其细节留作练习。

现在我们来编写 rectangleType 类的定义，并展示运算符函数在类定义中的呈现方式。由于某些运算符既可以重载为成员函数，也可以重载为非成员函数，我们给出 rectangleType 类的两个等价定义。在第一个定义中，自增、自减、算术和关系运算符被重载为成员函数。在第二个定义中，自增、自减、算术和关系运算符被重载为非成员函数。

rectangleType 类的定义如下：

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
    rectangleType operator*(const rectangleType&) const;
    rectangleType operator/(const rectangleType&) const;

    //Overload the increment and decrement operators
    rectangleType operator++();                 //pre-increment
    rectangleType operator++(int);              //post-increment
    rectangleType operator--();                 //pre-decrement
    rectangleType operator--(int);              //post-decrement

    //Overload the relational operators
    bool operator==(const rectangleType&) const;
    bool operator!=(const rectangleType&) const;
    bool operator<=(const rectangleType&) const;
    bool operator<(const rectangleType&) const;
    bool operator>=(const rectangleType&) const;
    bool operator>(const rectangleType&) const;

    //Constructors
    rectangleType();
    rectangleType(double l, double w);

private:
    double length;
    double width;
};
```

下面是 rectangleType 类的定义，其中自增、自减、算术和关系运算符被重载为非成员函数。

```cpp
//Definition of the class rectangleType
//The increment, decrement, arithmetic, and relational
//operator functions are nonmembers of the class.

#include <iostream>

using namespace std;

class rectangleType
{
    //Overload the stream insertion and extraction operators
    friend ostream& operator<<(ostream&, const rectangleType&);
    friend istream& operator>>(istream&, rectangleType&);

    //Overload the arithmetic operators
    friend rectangleType operator+(const rectangleType&,
                                   const rectangleType&);
    friend rectangleType operator-(const rectangleType&,
                                   const rectangleType&);
    friend rectangleType operator*(const rectangleType&,
                                   const rectangleType&);
    friend rectangleType operator/(const rectangleType&,
                                   const rectangleType&);

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
    friend bool operator<(const rectangleType&,
                          const rectangleType&);
    friend bool operator>=(const rectangleType&,
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

为 rectangleType 类重载运算符的函数定义留作练习。（参见本章末尾的编程练习 1 和 2。）

## 运算符重载：成员函数与非成员函数

前面各节讨论并说明了如何重载运算符。某些运算符必须重载为类的成员函数，而有些必须重载为非成员（友元）函数。对于那些既可以重载为成员函数又可以重载为非成员函数的运算符，情况又如何呢？例如，二元算术运算符 + 可以重载为成员函数或非成员函数。如果将 + 重载为成员函数，那么运算符 + 可以直接访问其中一个对象的成员变量，并且你只需将一个对象作为
