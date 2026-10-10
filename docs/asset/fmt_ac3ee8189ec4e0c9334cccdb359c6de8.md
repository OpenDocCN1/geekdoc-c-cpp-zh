
`XYZ(int i, int j) : b(i), a(b * j) { }`

请注意，这种定义不会产生任何编译错误。事实上，成员 `b` 将被准确地赋值；成员 `a` 将被初始化为垃圾值，因为 `b` 的值对要被初始化的 `a` 不可用。

以下语句也是有效的：

```
XYZ(int i, int j) : a(i) { b = j };
XYZ(int i, int j) { a = i; b = j; };
```

如果不需要，我们可以省略任一部分。程序 8.8 展示了在基类和派生类构造函数中使用初始化列表。

## 程序 8.8 构造函数中的初始化列表

```
#include <iostream>
using namespace std;
class alpha {
    int x;
public:
    alpha(int i)
    {
        x = i;
        cout << "\n alpha constructed\n";
    }
    void show_alpha(void)
    {
        cout << " x = " << x << "\n";
    }
};
class beta {
    float p, q;
public:
    beta(float a, float b) : p(a), q(b+b)
    {
        cout << "\n beta constructed\n";
    }
    void show_beta(void)
    {
        cout << " p = " << p << "\n";
        cout << " q = " << q << "\n";
    }
};
class gamma : public beta, public alpha {
    int u, v;
public:
    gamma(int a, int b, float c)
    : alpha(a*2), beta(b,c), u(a)
    {
        v = b; cout << "\n gamma constructed\n";
    }
    void show_gamma(void)
    {
        cout << " u = " << u << "\n";
        cout << " v = " << v << "\n";
    }
};
```

```
int main() {
    gamma g(2, 4, 2.5);
    cout << "\nDisplay member values " << "\n\n";
    g.show_alpha();
    g.show_beta();
    g.show_gamma();
    return 0;
}
```

程序 8.8 的输出将为：

- beta constructed
- alpha constructed
- gamma constructed
Display member values
- x = 4
- p = 2.5
- q = 5
- u = 2
- v = 4

> 派生构造函数 `gamma` 的参数列表仅包含三个参数 `a`、`b` 和 `c`，它们用于初始化三个类中包含的五个数据成员。

### 8.12 成员类：类的嵌套

继承是将一个类的某些属性派生到另一个类的机制。我们已经详细了解了如何使用派生类的概念来实现这一点。C++ 还支持将一个类的属性继承到另一个类的另一种方式。这种方法认为一个对象可以是许多其他对象的集合。也就是说，一个类可以包含其他类的对象作为其成员，如下所示：

```
class alpha {....};
class beta {....};
class gamma {
    alpha a; // a 是 alpha 类的对象
    beta b; // b 是 beta 类的对象
    ....
};
```

`gamma` 类的所有对象都将包含对象 `a` 和 `b`。这种关系称为包含或嵌套。创建包含另一个对象的对象与创建独立对象非常不同。

## 233

## 继承：扩展类

独立对象在声明时带参数，其构造函数创建它。另一方面，嵌套对象是分两个阶段创建的。首先，使用各自的构造函数创建成员对象，然后创建其他成员。这意味着所有成员对象的构造函数都应在自己的构造函数体执行之前被调用。这是通过在嵌套类的构造函数中使用初始化列表来实现的。

示例：

```
class gamma
{
    alpha a; // a 是 alpha 的对象
    beta b; // b 是 beta 的对象
public:
    gamma(arglist1): a(arglist1), b(arglist2)
    {
        // 构造函数体
    }
};
```

`arglist` 是在定义 `gamma` 对象时要提供的参数列表。这些参数用于初始化 `gamma` 的成员。`arglist1` 是 `a` 的构造函数的参数列表，`arglist2` 是 `b` 的构造函数的参数列表。`arglist1` 和 `arglist2` 可能会或可能不会使用来自 `arglist` 的参数。记住，`a(arglist1)` 和 `b(arglist2)` 是函数调用，因此参数不包含数据类型。它们只是变量或常量。

示例：

```
gamma(int x, int y, float z) : a(x), b(x, z)
{
    Assignment section(for ordinary other members)
}
```

我们可以在一个类中使用任意多的成员对象。对于每个成员对象，我们在初始化器列表中添加一个构造函数调用。成员对象的构造函数是按照它们在嵌套类中声明的顺序调用的。

## 摘要

- 从旧类派生新类的机制是继承。继承提供了可重用的概念。C++ 类可以通过继承被重用。
- 派生类继承基类的一些或全部属性。
- 只有一个基类的派生类称为单继承。
- 一个类可以从多个类继承属性，这称为多继承。
- 一个类可以从另一个派生类派生，这称为多级继承。
- 当一个类的属性被多个类继承时，这称为层次继承。
- 一个类的私有成员不能在公有模式或私有模式下被继承。
- 在公有模式下继承的受保护成员变为受保护，而在私有模式下继承则在派生类中变为私有。
- 在公有模式下继承的公有成员变为公有，而在私有模式下继承则在派生类中变为私有。
- 友元函数和友元类的成员函数可以直接访问私有和受保护的数据。
- 派生类的成员函数只能直接访问受保护和公有数据。然而，它们可以通过基类的成员函数访问私有数据。
- 多路径继承可能导致从“祖父”基类继承的成员重复。这可以通过将公共基类设为虚基类来避免。
- 在多继承中，基类是按照它们在派生类声明中出现的顺序构造的。
- 在多级继承中，构造函数是按照继承顺序执行的。
- 一个类可以包含其他类的对象。这称为组合或嵌套。

## 关键词

`abstract class` | `access control` | `access mechanism` | `ancestor class` | `assignment section` | `base class` | `base constructor` | `child class` | `common base class` | `containment` | `derivation` | `derived class` | `derived constructor` | `direct base class` | `dot operator` | `duplicate members` | `father class` | `friend` | `grandfather class` | `grandparent class` | `hierarchical inheritance` | `hybrid inheritance` | `indirect base class` | `inheritance` | `inheritance path` | `initialization list` | `initialization section` | `intermediate base` | `member classes` | `multilevel inheritance` | `multiple inheritance` | `nesting` | `private` | `private derivation` | `private members` | `privately derived` | `protected` | `protected members` | `public` | `public derivation` | `public members` | `publicly derived` | `reusability` | `single inheritance` | `subclass` | `virtual base class` | `visibility mode` | `visibility modifier`

## 复习问题

### 认知领域

- 8.1 说明 C++ 中继承的含义。
- 8.2 列出继承的不同形式；并为每种形式提供合适的示例。
- 8.3 描述 C++ 中单继承的语法。
- 8.4 我们知道基类的私有成员是不可继承的。给出派生类对象访问基类私有成员的可能方法。在论证你的答案时，基类不能被修改。
- 8.5 区分以下两个派生类的属性：
  + (a) `class D1: private B{/...};`
  + (b) `class D2: public B{/...};`
- 8.6 指出何时对类的成员使用 `protected` 可见性限定符。
- 8.7 描述多重继承的语法；同时简要说明这种继承的可用性。
- 8.8 表达一个虚基类。
- 8.9 解释何时使一个类变为虚类。
- 8.10 讨论关于抽象类。
- 8.11 分解在创建派生类对象时类构造函数的调用顺序。
- 8.12 类 `D` 派生自类 `B`。类 `D` 不包含自身的数据成员。论证类 `D` 是否需要构造函数并给出适当的解释。
- 8.13 概述包含关系并将其与继承区分开来。
- 8.14 演示构造一个包含其他类对象的类的对象。

### Psychomotor Domain

8.15 显示以下两个定义的含义：
+ (a) `class A: public B, public C{/...};`
+ (b) `class A: public C, public B{/...};`

### Affective Domain

8.16 为以下陈述的正确性辩护：
+ (a) 继承有助于将一个通用类变为更具体的类。
+ (b) 继承有助于数据隐藏。
+ (c) 继承的一个优点是它提供了一个概念框架。
+ (d) 继承促进了类库的创建。
+ (e) 定义派生类需要在基类中进行一些更改。
+ (f) 基类永远不会被用来创建对象。
+ (g) 合法地让一个类的对象作为另一个类的成员。
+ (h) 我们可以通过在派生类的定义中使基类变为虚类来阻止基类所有成员的继承。

Legend Precision Valuing/Responding/Organizing Applying Remembering Understanding

## DEBUGGING EXERCISES

8.1 找出以下程序中的错误。

```
#include <iostream>
using namespace std;
class faculty
{
private:
    int fid;
    char name[20];
    void getdata()
    {
        cout<<"Enter faculty id :- - \t";
        cin>>fid;
        cout<<"Enter Name :- - \t";
        cin>>name;
    }
}
class details : faculty
{
public:
    int age, exp;
    void getdetails()
    {
        getdata();
        cout<<"Enter age :- \t";
        cin>>age;
        cout<<"Enter year of exp. :- - \t";
        cin>>exp;
    }
    void display()
    {
        cout<<"\n\n"<<"faculty id \t"<<fid<<endl;
        cout<<"Name of faculty \t"<<name<<endl;
        cout<<"Faculty age \t"<<age<< endl;
        cout<<"faculty year of exp \t"<<exp<<endl;
    }
}
int main()
{
    details m;
    m.getdetails();
    m.display();
    return 0;
}
```

8.2 找出以下程序中的错误。

```
#include <iostream>
using namespace std;
class four_seater
{
public: void Property()
{
  cout << "It has space for four persons" << endl;
}
class four_wheeler
{
  public: void Property()
  {
    cout << "It runs on four tyres" << endl;
  }
};
class Car: public four_seater, public four_wheeler
{
};};
int main()
{
  Car C1;
  C1.four_seater;
  C1.four_wheeler;
  return 0;
}
```

## 8.3 找出以下程序中的错误。

```
#include<iostream>
using namespace std;
class p
{
  public:
    int i;
};
class q : virtual public p
{
  public:
    int j;
};
class r: virtual public p
{
  public:
    int k;
};
class s: public p, public q, public r
{
  public:
    int mul;
};
int main()
{
  s obj1;
  obj1.i = 10;
  obj1.j = 20;
  obj1.k = 30;
```

238
Object-Oriented Programming with C++

```
int obj1_mul = obj1.mul * obj2.mul;
cout << "Mul is : " << obj1.mul << "\n";
return 0;
```

## DRY-RUN EXERCISES

8.1 当运行以下程序时会发生什么？

```
#include<iostream>
using namespace std;
int a,b,c,d,e;
class A
{
    protected:
    public:
    void value_a_b()
    {
        a=2; b=2;
    }
};
class B:public A
{
    protected:
    public:
    void value_c()
    {
        d=2;
    }
};
class C
{
    protected:
    public:
    void value_d()
    {
        e=3;
    }
};
class D:public B, public C
{
    protected:
    public:
    void result()
    {
        value_a_b();
        value_c();
    }
}
```

```
value_d();
e=a*b*c*d;
cout<<"\n Multiplication is :":<<e";
}
int main()
{
 D d1;
d1.result();
return 0;
}
```

## 8.2 当运行以下程序时会发生什么？

```
#include<iostream>
using namespace std;
class B
{
 int x;
public:
 B() { cout << "1\t"; }
};
class D : public B
{
 int y;
public:
D() { cout << "2\t";
D(int i) { cout << "3\t"; }
};
int main()
{
 B b;
D d1;
D d2(1);
}
```

## 8.3 当运行以下程序时会发生什么？

```
#include <iostream>
using namespace std;
class A
{
 int a;
public:
A() { }
A(int d)
{ a = d; }
~A()
{
 cout << endl << "Object A being destroyed";
}
 void show()
{
cout << a << endl;
}
;
class B : public A
{
    int b;
public:
    B() : A()
{}
    B(int d, int d1) : A(d)
{
        b = di;
    }
    ~B()
{
```
