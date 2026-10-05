

```cpp
void A::setx(const int p)
{
    x=p;
}
```

```cpp
int A::getx() const
{
    return x;
}
```

```cpp
/*End of A.cpp*/
/*Beginning of B.h*/
#include "B.h"
```

```cpp
class B : public A
{
    int y;
public:
    B(const int q=0);
    void sety(const int q=0);
    int gety(const int);
};
```

```cpp
/*Beginning of B.cpp*/
#include "B.h"
```

```cpp
B::B(const int q)
{
    y=q;
}
```

```cpp
void B::sety(const int q)
{
    y=q;
}
```

```cpp
int B::gety() const
{
    return y;
}
```

```cpp
/*End of B.cpp*/
```

```cpp
/*Beginning of baseinit1.cpp*/
#include "B.h"
#include <iostream.h>
```

```cpp
void main()
{
    B B1(20);
    cout << B1.getx() << endl
         << B1.gety() << endl;
}
```

```cpp
/*End of baseinit1.cpp*/
```

# 输出

0
20

该输出可以通过简单的观察来解释，即语句 B1(20);

继承 131 

被转换为以下形式：

B1; //为对象分配内存
B1.A(); // 调用了基类构造函数
B1.B(20); // 调用了派生类构造函数

如所见，派生类对象的基类数据成员通过基类构造函数进行初始化，传递给它的是默认值。因此，'B1.y' 被初始化为 20（传递的值）。但 'B1.x' 被初始化为 0（默认值）。在创建派生类对象时，我们希望显式地向基构造函数传递一个值。因此，在列表 5.15 中，类 B 的构造函数不应该接收一个参数，而是两个。其中一个应该传递给 'y'，而另一个应该用于初始化 'x'。为此，类 B 构造函数的原型和定义应该如列表 5.16 所示进行修改。

## 列表 5.16 修改派生类构造函数以确保基类成员成功初始化

```cpp
/*Beginning of B.h*/
#include "A.h"
class B : public A
{
public:
    B(const int p=0, const int q=0);
    /*
    类 B 的其余部分
    */
};
/*End of B.h*/

/*Beginning of B.cpp*/
#include "B.h"
B::B(const int p, const int q) : A(p) // 将值传递给基类
//类构造函数
{
    y=q;
}
/*
    类 B 剩余成员函数的定义
*/
/*End of B.cpp*/
```

可以通过向构造函数传递两个参数来声明类 B 对象。其中一个赋值给 'x'，另一个赋值给 'y'。

## 列表 5.17 基类初始化

```cpp
/*Beginning of baseinit02.cpp*/
#include <iostream.h>
void main()
{
    B B1(10,20);
    cout << B1.getx() << endl << B1.gety() << endl;
```

# C++ 面向对象编程

```cpp
}
/*End of baseinit02.cpp*/
```

# 输出
10
20

再次，列表 5.17 的输出可以解释为由于类 B 构造函数的定义修改，语句

```cpp
B B1(10,20);
```

被转换为

```cpp
B B1;                               //为对象分配内存
B1.A(10);                              //调用基类构造函数
B1.B(20);                               //调用派生类构造函数
```

根据列表 5.17 中派生类构造函数的定义，传递给它的第一个参数转而传递给了基类构造函数。但这不是必要的。传递给派生类构造函数的任何参数都可以传递给基类构造函数。

## 5.5 保护访问修符

除了 public（公共）和 private（私有）访问修符外，C++ 中第三种访问修符称为 protected（保护）。保护成员对成员函数不可用。然而，它们所属类的成员函数以及派生类的成员函数是可以访问的。列表 5.18 及其注释说明了这一点。

- 列表 5.18 访问保护成员

```cpp
/*Beginning of A.h*/
class A
{
private:
int x;
protected:
int y;
public:
int z;
};
/*End of A.h*/
```

```cpp
/*Beginning of B.h*/
#include "A.h"
class B : public A                               //派生类
{
public:
void xyz();
}
/*End of B.h*/
/*Beginning of B.cpp*/
#include "B.h"
void B::xyz()                                     //派生类的成员函数
```

```cpp
{
  x=1; //错误：基类的私有成员
  y=2; // 正常：基类的保护成员
  z=3; // 正常：基类的公共成员
}
```

```cpp
/*Beginning of protected.cpp*/
#include "A.h"
void main() {
  A * Aptr;
  Aptr->x=10; //错误：私有成员
  Aptr->y=20; //错误：保护成员
  Aptr->z=30; // 正常：公共成员
}
/*End of protected.cpp*/
```

## 5.6 通过不同的访问修符派生

### 5.6.1 通过公共访问修符派生

通过 public 访问修符派生保留了基类成员的访问级别。

**私有成员：** 派生类的成员函数无法访问。后续派生类的成员函数无法访问它们。成员函数无法访问它们。

**保护成员：** 派生类的成员函数可以访问它们。后续派生类的成员函数也可以访问它们。成员函数无法访问它们。

**公共成员：** 派生类的成员函数可以访问它们。后续派生类的成员函数也可以访问它们。成员函数也可以访问它们。

编译列表 5.19 时遇到的错误说明了这一点。

- **列表 5.19** 访问通过公共访问修符派生的对象的继承成员

```cpp
/*Beginning of publicInheritance.cpp*/
class A {
  private:
  int x;
  protected:
  int y;
  public:
  int z;
}
class B : public A //B 是 A 的公共派生类
{
  public:

# 134 C++ 面向对象编程

```cpp
void f1()
{
    x=1;
    y=2;
    z=2;
    //错误：私有成员仍为私有
    // 正常：保护成员仍为保护
    // 正常：公共成员仍为公共
}
```

```cpp
class C : public B
{
    public:
    void f2()
    {
        x=1; //错误：私有成员仍为私有
        y=2; // 正常：保护成员仍为保护
        z=2; // 正常：公共成员仍为公共
    }
}
```

可以通过向构造函数传递两个参数来声明类 B 对象。其中一个赋值给 'x'，另一个赋值给 'y'。

## 列表 5.17 基类初始化

```cpp
/*Beginning of baseinit02.cpp*/
#include <iostream.h>
void main()
{
    B B1(10,20);
    cout << B1.getx() << endl << B1.gety() << endl;
}
/*End of baseinit02.cpp*/
```

再次，列表 5.17 的输出可以解释为由于类 B 构造函数的定义修改，语句

```cpp
B B1(10,20);
```

被转换为

```cpp
B B1;                               //为对象分配内存
B1.A(10);                              //调用基类构造函数
B1.B(20);                               //调用派生类构造函数
```

根据列表 5.17 中派生类构造函数的定义，传递给它的第一个参数转而传递给了基类构造函数。但这不是必要的。传递给派生类构造函数的任何参数都可以传递给基类构造函数。

## 5.5 保护访问修符

除了 public（公共）和 private（私有）访问修符外，C++ 中还有第三种访问修符称为 protected（保护）。保护成员对成员函数不可用。然而，它们所属类的成员函数以及派生类的成员函数是可以访问的。列表 5.18 及其注释说明了这一切。

- 列表 5.18 访问保护成员

```cpp
/*Beginning of A.h*/
class A
{
private:
int x;
protected:
int y;
public:
int z;
};
/*End of A.h*/
```

```cpp
/*Beginning of B.h*/
#include "A.h"
class B : public A                               //派生类
{
public:
void xyz();
}
/*End of B.h*/
/*Beginning of B.cpp*/
#include "B.h"
void B::xyz()                                     //派生类的成员函数
```

```cpp
{
  x=1; //错误：基类的私有成员
  y=2; // 正常：基类的保护成员
  z=3; // 正常：基类的公共成员
}
```

```cpp
/*Beginning of protected.cpp*/
#include "A.h"
void main() {
  A * Aptr;
  Aptr->x=10; //错误：私有成员
  Aptr->y=20; //错误：保护成员
  Aptr->z=30; // 正常：公共成员
}
/*End of protected.cpp*/
```

## 5.6 通过不同的访问修符派生

### 5.6.1 通过公共访问修符派生

通过 public 访问修符派生保留了基类成员的访问级别。

**私有成员：** 派生类的成员函数无法访问。后续派生类的成员函数无法访问它们。成员函数无法访问它们。

**保护成员：** 派生类的成员函数可以访问它们。后续派生类的成员函数也可以访问它们。成员函数无法访问它们。

**公共成员：** 派生类的成员函数可以访问它们。后续派生类的成员函数也可以访问它们。成员函数也可以访问它们。

编译列表 5.19 时遇到的错误说明了这一点。

- **列表 5.19** 访问通过公共访问修符派生的对象的继承成员

```cpp
/*Beginning of publicInheritance.cpp*/
class A {
  private:
  int x;
  protected:
  int y;
  public:
  int z;
}
class B : public A //B 是 A 的公共派生类
{
  public:

# 134 C++ 面向对象编程

```cpp
void f1()
{
    x=1;
    y=2;
    z=2;
    //错误：私有成员仍为私有
    // 正常：保护成员仍为保护
    // 正常：公共成员仍为公共
}
```

```cpp
class C : public B
{
    public:
    void f2()
    {
        x=1; //错误：私有成员仍为私有
        y=2; // 正常：保护成员仍为保护
        z=2; // 正常：公共成员仍为公共
    }
}
```

## 5.6.2 通过保护访问修符派生

通过 protected 访问修符派生将基类公共成员的访问级别降低为保护，而基类保护和私有成员的访问级别保持不变。

**私有成员：** 派生类的成员函数无法访问。后续派生类的成员函数无法访问它们。成员函数无法访问它们。

**保护成员：** 派生类的成员函数可以访问它们。后续派生类的成员函数也可以访问它们。成员函数无法访问它们。

**公共成员：** 派生类的成员函数可以访问它们（但它们在派生类中变为保护）。

编译列表 5.21 时遇到的错误说明了这一点。

- **列表 5.21** 访问通过保护访问修符派生的对象的继承成员

```cpp
/*Beginning of publicInheritance.cpp*/
class A {
  private:
  int x;
  protected:
  int y;
  public:
  int z;
};
class B : public A //B 是 A 的公共派生类
{
  public:
void f1()
{
    x=1; //错误：私有成员仍为私有
    y=2; // 正常：保护成员仍为保护
    z=2; // 正常：公共成员仍为公共
}
}
class C : public B
{
    public:
    void f2()
    {
        x=1; //错误：私有成员仍为私有
        y=2; // 正常：保护成员仍为保护
        z=2; // 正常：公共成员仍为公共
    }
}
```

