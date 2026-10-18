

## 摘要

- 多态性（polymorphism）简单来说就是“一个名字，多种形式”。
- 多态有两种类型，即编译时多态和运行时多态。
- 函数重载和运算符重载是编译时多态的典型例子。重载成员函数的选择依据是参数的类型和个数。编译器在编译时就能知道这些信息，因此在编译时就能为特定的调用选择合适的函数。这被称为早期绑定（early binding）或静态绑定（static binding），也称作静态链接。这意味着对象在编译时就被绑定到其函数调用。
- 在运行时多态中，合适的成员函数是在程序运行过程中被选中的。C++ 借助虚函数支持运行时多态。这被称为晚期绑定或动态绑定，因为合适的函数是在运行时动态选定的。动态绑定需要使用对象指针，它是 C++ 的强大特性之一。
- 对象指针有助于在运行时创建对象。它可以与箭头运算符一起使用，访问对象的公有成员。
- **this** 指针指向当前正在调用成员函数的那个对象。例如，函数调用 **a.show()** 会将指针 `this` 设置为对象 `a` 的地址。
- 指向基类对象的指针与指向派生类对象的指针是兼容的。因此，我们可以用同一个指针变量来指向基类和派生类的对象。
- 当一个函数被声明为 virtual 时，C++ 在运行时根据基类指针所指向的对象的类型（而不是指针本身的类型）来决定调用哪个函数。通过让基类指针指向不同的对象，我们可以执行虚函数的不同版本。
- 运行时多态只能通过指向基类的指针来访问虚函数时才能实现。不能用对象名加点运算符来访问虚函数。
- 可以有虚析构函数，但不能有虚构造函数。
- 如果基类中定义了一个虚函数，在派生类中不一定要重新定义它。此时，对应的调用将调用基类的那个函数。
- 一个被赋值为 0 的虚函数称为纯虚函数。它是在基类中声明但在基类中没有定义的函数。包含这种纯虚函数的类称为抽象类。

## 关键术语

抽象基类 | “取地址”运算符 | 实参对象 | 指针数组 | 箭头运算符 | 基地址 | 基类对象 | 基类指针 | 回调函数 | 类层次结构 | 编译时 | 编译时多态 | 解引用运算符 | 派生类对象 | 空操作函数 | 点运算符 | 动态绑定 | 早期绑定 | 函数重载 | 函数指针 | 隐式参数 | 间接运算符 | 调用对象 | 晚期绑定 | new 运算符 | 空指针 | 对象指针 | 运算符重载 | 占位符 | 指针 | 指针算术 | 指向函数的指针 | 多态 | 纯虚函数 | 运行时 | 运行时多态 | 静态

## 复习题

- 9.1 在 C++ 语言中，多态（polymorphism）是什么意思？
- 9.2 多态是如何在（a）编译时和（b）运行时实现的？
- 9.3 讨论访问对象的公有成员函数的不同方式。
- 9.4 什么是函数指针？解释在什么情况下会使用这种概念。
- 9.5 举例说明如何使用指针为对象数组分配空间。
- 9.6 **this** 指针指向什么？
- 9.7 **this** 指针的应用有哪些？
- 9.8 基类类型的指针能否指向派生类的对象？请解释。
- 9.9 什么是虚函数？
- 9.10 为什么需要虚函数？
- 9.11 什么时候我们应该将虚函数设为“纯”虚函数？将一个函数设为纯虚函数会带来什么影响？
- 9.12 判断下列陈述是 TRUE 还是 FALSE。
  - (a) 虚函数用于创建指向基类的指针。
  - (b) 虚函数允许我们使用同一次函数调用来调用不同类对象的成员函数。
  - (c) 基类指针不能设置为指向派生类的对象。
  - (d) **this** 指针指向当前用于调用成员函数的那个对象。
  - (e) 像其他指针一样，this 指针可以用来访问它所指向的对象的成员。
  - (f) 可以通过给 this 指针赋对象地址的方式让它指向任意对象。
  - (g) 纯虚函数强制程序员在派生类中重新定义该虚函数。

## 调试练习

### 9.1 找出下面程序中的错误。

```cpp
#include <iostream.h>
class Info
{
    char *name;
    int number;
public:
    void getInfo()
    {
        cout << "Info::getInfo ";
        getName();
    }
    void getName()
    {
        cout << "Info::getName ";
    }
};
class Name: public Info
{
    char *name;
public:
    void getName()
    {
        cout << "Name::getName ";
    }
};
void main()
{
    Info *p;
    Name n;
    p = n;
    p->getInfo();
}
/*
```

### 9.2 找出下面程序中的错误。

```cpp
#include <iostream.h>
class Person
{
    int age;
public:
    Person()
    {
    }
    Person(int age)
    {
        this.age = age;
    }
    Person& operator < (Person &p)
    {
        return age < p.age ? p: *this;
    }
    int getAge()
    {
        return age;
    }
};
void main ()
{
    Person P1 (15);
    Person P2 (11);
    Person P3;
    //if p1 is less than p2
    p3 = p1 < p2; p1. lessthan(p2)
    cout << p3.getAge( );
}
/*
```

### 9.3 找出下面程序中的错误。

```cpp
#include "iostream.h"
class Human
{
public:
    Human( )
    {
    }
    virtual ~Human( )
    {
        cout << "Human::~Human"; 
    }
};
class Student: public Human
{
public:
    Student( )
    {
    }
    ~Student( )
    {
        cout << "Student::~Student( )";
    }
};
void main( )
{
    Human *H = new Student( );
    delete H;
}
```

### 9.4 改正下面程序中的错误。

```cpp
class test
{
private:
    int m;
public:
    void getdata( )
    {
        cout << "Enter number:";
        cin >> m;
    }
    void display( )
    {
        cout << m;
    }
};
main( )
{
    test T;
    T->getdata( );
    T->display( );
    test *p;
    p = new test;
    p.getdata( );
    (*p).display( );
}
```

### 9.5 调试并运行下面程序。输出是什么？

```cpp
#include <iostream.h>
class A
{
protected:
    int a,b;
public:
    A(int x = 0, int y)
    {
    }
};

class A
{
public:
    int a = x;
    int b = y;
    virtual void print();
};

class B: public A
{
private:
    float p, q;
public:
    B(int m, int n, float u, float v)
    {
        p = u;
        q = v;
    }
    B() { p = q = 0; }
    void input(float u, float v);
    virtual void print(float);
};

void A::print(void)
{
    cout << "A values: " << a << "," << b << "\n";
}

void B::print(float)
{
    cout << "B values:" << u << "," << v << "\n";
}

void B::input(float x, float y)
{
    p = x;
    q = y;
}

main()
{
    A a1(10,20), *ptr;
    B b1;
    b1.input(7.5,3.142);

    ptr = &a1;
    ptr->print();

    ptr = &b1;
    ptr->print();
}
```

### 9.6 测试下面程序的输出：

```cpp
#include<iostream>
using namespace std;
class BC
{
public:
    void show(void){cout<<"\nI am in base class..";}
};
class DC: public BC
{
public:
    void show(void){cout<<"\nI am in derived class..";}
```

