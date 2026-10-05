

## 运算符重载、类型转换、新风格强制转换与 RTTI 225

```cpp
/*Beginning of A.cpp*/
#include"A.h"
A::A(int p)
{
    x = p;
}
nA::operator - ()
{
    return A(-x);
}
/*End of A.cpp*/
```

运算符也可以通过友元函数进行重载（如列表 8.16 所示）。

列表 8.16 通过友元函数重载一元减运算符

```cpp
/*Beginning of A.h*/
class A
{
    int x;
    A(int = 0);
    public:
        friend A operator - (const A&);
};
/*End of A.h*/
```

```cpp
/*Beginning of A.cpp*/
#include"A.h"
A::A(int p)
{
    x = p;
}
nA operator - (const A& Aobj)
{
    return A(-Aobj.x);
}
/*End of A.cpp*/
```

重载一元加运算符留给读者作为练习。

## 8.2.3 重载算术运算符

算术运算符是二元运算符。因此，通过成员函数重载它们的语法在列表 8.17 中所示。

列表 8.17 通过成员函数重载算术运算符的语法

```cpp
class <class_name>
{
    public:
        //原型
        <return_type> operator<arith_op_symbol>(<param_list>);
};
//定义
<return_type> <class_name>::operator<arith_op_symbol>(<param_list>
{
  //函数体
}
```

* 笔记本

# 使用 C++ 进行面向对象程序设计

存储算术运算符右侧操作数值的对象将出现在形式参数列表中。左侧操作数将隐式地传递给函数，该运算符重载函数将相对于该对象被调用。语句

```cpp
Obj3 = Obj1 <arith_op_symbol> Obj2;
```

将被解释为：

```cpp
Obj3 = Obj1.operator <arith_op_symbol> (Obj2);
```

如果通过友元函数重载算术运算符，则语法将如列表 8.18 所示。

+ 列表 8.18 通过友元函数重载算术运算符的语法

```cpp
class <class_name>
{
  public:
    //原型
    friend <return_type>operator<arith_op_symbol>(<param_list>);
    //定义
    <return_type> operator<arith_op_symbol>(<param_list>)
    //函数体
}
```

存储算术运算符左侧和右侧操作数值的对象将出现在形式参数列表中。语句

```cpp
Obj3 = Obj1 <arith_op_symbol> Obj2;
```

将被解释为：

```cpp
Obj3 = Obj1.operator <arith_op_symbol> (Obj2);
```

由于算术运算符已通过友元函数重载，最终的解释将是：

```cpp
Obj3 = Obj1.operator <arith_op_symbol> (Obj2);
```

现在让我们尝试一些示例。看看如何为我们已经熟悉的类重载加运算符。我们希望列表 8.19 给出的代码能够成功编译，其输出如下：

+ 列表 8.19 在对象上使用重载运算符

```cpp
Distance d1(5),d2(4),d3;
d3 = d1+d2;
cout<<d3.feet()<<d3.inches();
```

为了实现这一点，我们必须通过成员函数或友元函数为该类重载加运算符。让我们先看通过成员函数重载该类的加运算符。在这种情况下，语句

d3 = d1+d2;

显然是

列表 8.20 通过成员函数重载算术运算符

```cpp
/*Beginning of Distance.h*/
class Distance
{
    int ifet;
    float inches;
    public:
        Distance(int = 0);
        Distance operator+(const Distance&);
        int getFeet() const;
        float getInches() const;
};
/*End of Distance.h*/
```

```cpp
/*Beginning of Distance.cpp*/
#include "Distance.h"
Distance::Distance(int p)
{
    ifet = p;
    inches = 0;
}
Distance Distance::operator+(const Distance& obj)
{
    return Distance(ifet+obj.ifet, inches+obj.inches);
}
int Distance::getFeet() const
{
    return ifet;
}
float Distance::getInches() const
{
    return inches;
}
/*End of Distance.cpp*/
```

如果右侧是一个对象，则列表 8.20 有效。

+ 列表 8.21 通过友元函数重载算术运算符

```cpp
/*Beginning of Distance.h*/
class Distance
{
    int ifet;
    float inches;
    public:
        Distance(int = 0);
        friend Distance operator+(const Distance&);
        int getFeet() const;
        float getInches() const;
};
/*End of Distance.h*/
```

```cpp
/*Beginning of Distance.cpp*/
#include "Distance.h"
Distance::Distance(int p)
{
    ifet = p;
    inches = 0;
}
// 注意：此处原文 friend 关键字在函数体外可能有误，此处保留原样翻译
friend Distance operator+(const Distance& obj)
{
    return Distance(ifet+obj.ifet, inches+obj.inches);
}
int Distance::getFeet() const
{
    return ifet;
}
float Distance::getInches() const
{
    return inches;
}
/*End of Distance.cpp*/
```

然而，仍有一个条件需要解决。如果左侧是 float 类型怎么办？解决方案是提供一个从 float 转换为 Distance 的构造函数。

+ 列表 8.22 通过构造函数重载算术运算符

```cpp
/*Beginning of Distance.h*/
class Distance
{
    int ifet;
    float inches;
    public:
        Distance(int = 0);
        Distance(float);
        friend Distance operator+(const Distance&);
        int getFeet() const;
        float getInches() const;
};
/*End of Distance.h*/
```

```cpp
/*Beginning of Distance.cpp*/
#include "Distance.h"
Distance::Distance(int p)
{
    ifet = p;
    inches = 0;
}
Distance::Distance(float p)
{
    ifet = (int)p;
    inches = 0;
}
friend Distance operator+(const Distance& obj)
{
    return Distance(ifet+obj.ifet, inches+obj.inches);
}
int Distance::getFeet() const
{
    return ifet;
}
float Distance::getInches() const
{
    return inches;
}
/*End of Distance.cpp*/
```

