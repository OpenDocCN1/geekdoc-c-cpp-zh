
```cpp
#include <iostream>
using namespace std;

//sum() definition1
int sum(int a, int b)
{
return(a+b);
}

//sum() definition2
float sum(float a, float b)
{
return(a+b);
}

int main() {
int x,y;
cout<<"Enter two integer numbers:"";
cin>>x>>y;
float u,v;
cout<<"Enter two float numbers:"";
cin>>u>>v;
//calling sum(int,int) function
cout<<endl<<"Sum of two integers:"<<sum(x,y);
//call sum(float,float) function
cout<<endl<<"Sum of two floating numbers:"<<sum(u,v);
return 0;
}
```

# 输出:

Enter two integer numbers: 4 5

Enter two float numbers: 13.5 12.4

Sum of two integers: 9

Sum of two floating numbers: 25.9

# 解释:

在这个程序中，`sum()` 函数通过两个定义进行了重载。因此，在 `main()` 函数中，如果用整数参数调用 `sum()`，则调用 `sum(int,int)`；否则，如果用浮点数参数调用 `sum()`，则调用 `sum(float,float)`。

- 3. 创建一个距离（Distance）类：

    - 脚（feet）和英寸（inches）作为数据成员

    - 输入距离的成员函数

    - 输出距离的成员函数

    - 相加两个距离对象的成员函数

编写一个程序来演示在相加对象距离时的函数重载。

```cpp
#include<iostream>
using namespace std;
class distance {

private:
    int feet,inch;
public:
    void input()
    {
        cout<<"Enter the feet and inch:";
        cin>>feet>>inch;

cout<<endl;
    }
void output()
{
    cout<<"The value of feet=""<<feet<<endl;
    cout<<"The value of inch=""<<inch<<endl;
}
// add() function definition-1
distance add(int f,int i)
{
    distance y;
    y.feet=feet+f;
    y.inch=inch+i;
    return y;
}
//add() function definition-2
distance add(distance x)
{
    distance y;
    y.feet=feet+x.feet;
    y.inch=inch+x.inch;
    return y;
};
int main()
{
    distance d1,d2,d3;
    d1.input();
    d2.input();
    d3=d2.add(d1);
    d1.output();
    d2.output();
    d3.output();
    d3=d2.add(4,2);
    d3.output();

    return 0;
}
```

# 输出:

Enter the feet and inch: 4 5

Enter the feet and inch: 3 2

The value of feet=4

The value of inch=5

The value of feet=3

The value of inch=2

The value of feet=7

The value of inch=4

# 解释:

在这个程序中，类中的成员函数被重载。在 `distance` 类中，`add()` 函数有两个定义。第一个定义接收两个整数输入，第二个定义接收 `distance` 对象作为参数。

- 4. 编写一个程序来重载一元运算符和二进制运算符作为成员函数和非成员函数。

(i) 作为成员函数的一元运算符

```cpp
#include<iostream>
using namespace std;
class ABC
{
    int a,b;
public:
void read()
{
  cout<<"enter a and b";
  cin>>a>>b;
}
void operator -()
{
  a=-a;
}
int main()
{
  ABC n1;
  n1.read();
  -n1;
  n1.show();
  return 0;
}
```

** 输出:**

enter a and b: 5 6

values=-5

# 解释:

在这个程序中，一元运算符 `'-'` 为类对象重载。这里使用了前置符号。

(i) 作为非成员函数的二进制运算符

```cpp
#include<iostream>
using namespace std;
class ABC
{
    int a,b;
    public:
    void read()
    {
        cout<<"enter a and b:";
        cin>>a>>b;
    }
    cout<<endl;
    void show()
    {
        cout<<endl<<"values="<<a<<b;
    }
};
friend ABC operator +(ABC x, ABC y)
{
    ABC t;
    t.a=x.a+y.a;
    t.b=x.b+y.b;
    return t;
}
int main()
{
    ABC n1,n2,n3;
    n1.read();
    n2.read();
    n1.show();
    n2.show();
    n3=n1+n2;
    n3.show();
    return 0;
}
```

# 输出:

enter a and b: 5 6

enter a and b: 3 2

values=56

values=32

# 解释:

对于二进制运算符重载，函数将接收两个参数，在这个程序中，重载函数是一个友函数。

## 5.9. 总结

在 C++ 中，静态多态通过函数重载和运算符重载实现。重载允许实体有多个定义。函数重载允许同名函数。像普通函数一样，成员函数也可以重载。运算符重载允许运算符有多个定义。`"operator'` 关键字用于运算符重载。一元运算符重载只接收一个参数，二进制运算符接收两个参数。

## 5.10. 练习

### 单选题

- 1. 哪个关键字用于运算符重载？

    (a) iterator

    (b) allocator

    (c) constructor

    (d) operator

    答案：(b)

- 2. 重载运算符函数应该是：

    1. 静态成员函数

    2. 非静态成员函数

    3. 友函数

    (a) 仅 2

    (b) 仅 1, 3

    (c) 仅 2, 3

    (d) 所有 1, 2, 3

    答案：(c)

- 3. 下列哪个运算符不能重载？

    (a) +

    (b) ++

    (c) :

    (d) ==

    答案：(e)

- 4. 重载函数 operator

    (a) 需要一个重载了运算符的类

    (b) 需要一个重载了 [] 运算符的类

    (c) 允许你创建语法上像函数的对象

    (d) 通常使用接收参数的构造函数。

    答案：(e)

- 5. 运算符的返回类型是

    (a) void

    (b) int

    (c) class

    (d) object

    答案：(e)

- 6. 前置增运算符重载的语法是

    (a) operator ++(int)

    (b) operator ++()

    (c) operator ()

    (d) operator (int)

    答案：(a)

- 7. 下标运算符是

    (a) ()

    (b) =

    (c) []

    (d) →

    答案：(c)

- 8. 可以通过运算符重载创建新运算符吗？

    (a) 可以

    (b) 不能

    (c) 可能

    (d) 可以

    答案：(b)

- 9. 重载函数将共享

    (a) 命名空间

    (b) 类

    (c) 以上 a 和 b

    (d) 都没有

    答案：(c)

- 10. 通过函数重载和运算符重载实现了以下哪个原则？

    (a) 封装

    (b) 多态

    (c) 继承

    (d) 抽象

    答案：(b)

### 答题

- 1. 什么是函数重载？为什么它在 OOP 中被称为函数多态。

- 2. 使用函数重载编写一个两个数字相加的程序。

- 3. 如何重载一元运算符？解释。

- 4. 什么是抽象类？我们何时对类成员使用保护可见性标识符？

- 5. 编写一个 C++ 程序重载两个增加运算符（前置和后置）。

- 6. 用示例解释运算符重载。

### 简答

- 1. 举出三个不能重载的运算符。

- 2. 如何通过私有继承保护数据？

- 3. 运算符重载和函数重载的区别是什么？

- 4. 什么是 operator ？

- 5. 列出重载函数的规则？

# 继承 - 第6章

继承将一个类的属性派生到另一个类。本章将讨论 C++ 中继承的实现方法。

## 6.1. 继承

继承是面向对象编程中最实用且核心的特征之一。通过继承，可以从现有类创建新类。现有类的属性简单地扩展到新类中。现有类被称为“基类”（base classes），新类被称为“派生类”（derived classes）。基类与派生类之间的关系被称为“一种关系”（kind of relationship）。

![](img/1ecdffe422a785b44c35b892c43c7da2_100_0.png)

图 6.1 继承示例

# 继承

派生类可以使用基类。因此，基类 A 的成员 x 被派生到类 B。所以，在类 B 中，两个成员（x 和 y）可用。派生类的语法为：

```
class derivedclassname : access-specifier baseclass
{
  members;
  member functions;
}
```

派生类也有它自己的一组成员和成员函数。访问修饰符（access specifiers）决定了基类的特征是以私有还是公开的方式派生的。默认访问修饰符是私有的（private）。

## 6.2. 重用性

重用意味着在派生类中重用基类的属性。重用是通过继承实现的。基类被称为超类（super class）、父类或祖类，派生类被称为子类（sub-class）、子类或后代。从先先派生的类再次派生一个类也是可能的。一个类可以从多个类派生。

示例：

```cpp
// 基类
class A
{
  ----------
}
// 派生类
class B : public A
{
  ----------
}
class C : private A
{
  ----------
}
```

### 6.2.1. 公有继承

当类被公地派生时，基类的所有公共成员都可以在派生类中直接访问。当类被私有地派生时，基类的所有私有成员只能通过基类的公共成员函数进行访问。

### 6.2.2. 私有继承

私有派生类的对象不能直接访问基类的公共成员。因此，使用成员函数来访问这些成员。

### 6.2.3. 私有继承中的受保护数据

`protected` 与 `private` ，但它允许派生类直接访问私有成员。

表 6.1 访问修饰符及其范围

| 基类访问模式 | 公有派生 | 私有派生 | 保护派生 |

| --- | --- | --- | --- |

| Public | 公有 | 私有 | 保护 |

| Private | 不继承 | 不继承 | 不继承 |

| protected | 保护 | 私有 | 私有（或保护） |

## 6.3. 继承的类型

### 6.3.1. 单继承

当只使用一个基类用于一个类的派生，且该派生类不被作为基类使用时，则称为单继承。

![](img/1ecdffe422a785b44c35b892c43c7da2_102_0.png)

示例：

```cpp
#include<iostream>
#include<constr>
using namespace std;
class base
{
protected:
int a,b;
};
class derived : public base
{
    public:
    void read()
    {
        cout<< "Enter Values:";
        cin>>a>>b;
    }
    void display()
    {
        cout<< "Values:"<<a<<b;
    }
};
int main()
{
    derived obj1;
    obj1.read();
    obj1.show();
    return 0;
}
```

输出：

Enter Values: 10 20

Values: 10 20

### 6.3.2. 多重继承

当使用两个或多个基类用于一个类的派生时，则归类为多重继承。

示例：

```cpp
#include<iostream>
#include<constr>
using namespace std;
class base1
{
protected:
    int a;
};
class base2
{
protected:
    int b;
};
class derived : public base1, base2
{
public:
    void read()
    {
        cout<<"Enter Values:"\n;
        cin>>a>>b;
    }
    void display()
{
        cout<<"Values:"<<a<<b;
    }
};
```

![](img/1ecdffe422a785b44c35b892c43c7da2_104_0.png)

```cpp
}
;int main()
{
  derived obj1;
  obj1.read();
  obj1.show();
  return 0;
}
```

# 输出：

Enter Values: 10 20

Values: 10 20

### 6.3.3. 多级继承

当一个类从另一个派生类派生出来时，则称为多级继承。派生类可以作为基类使用。

![](img/1ecdffe422a785b44c35b892c43c7da2_105_0.png)

示例：

```cpp
#include<iostream>
#include<constr>
using namespace std;
class base
{
public:
  int a;
};
class derived1 : public base
{
    int b;
};
class derived2 : public derived1
{
public:
    int c;
    void read()
    {
        cout<< "Enter Values:";
        cin>>a>>b>>c;
    }
    void display()
    {
        cout<< "Values:"<<a<<b<<c;
    }
};
int main()
{
    derived2 obj1;
    obj1.read();
    obj1.show();
    return 0;
}
```

# 输出:

Enter Values: 10 20 30

Values: 10 20 30

6.3.4. 层次继承

当一个基类用于两个或多个类的派生时，则称为层次继承。

![](img/1ecdffe422a785b44c35b892c43c7da2_107_0.png)

示例：

```cpp
#include<iostream>
#include<iostream>
using namespace std;
class base
{
protected:
    int a,b;
};
class derived1
{
public:
    void read()
    {
        cout<< "Enter Value of a:";
        cin>>a;
    }
    void display()
    {
        cout<< "Value of a:"<<a;
    }
};
class derived2
{
public:
    void read() {
        cout<< "Enter Value of b:";
        cin>>b;
    }
    void display() {
        cout<< "Value of b:"<<b;
    }
}
int main() {
    derived1 obj1;
    derived2 obj2;
    obj1.read();
    obj2.read();
    obj1.show();
    obj2.show();
    return 0;
}
```

# 输出：

Enter Value of a: 10
