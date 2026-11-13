

## 示例
## 编写程序求两个数的最大公约数

```cpp
#include<iostream.h>
class GCD
{
private:
    int a, b;
public:
    void input();
    void find();
};
inline void GCD :: input()
{
    cout << endl << "Enter two numbers";
    cin >> a >> b;
}
inline void GCD :: find()
{
    int r;
    if (a > b) // Makes a as greater than b
    {
        r = a;
        a = b;
        b = r;
    }
    r = a % b;
    while (r != 0)
    {
        a = b;
        b = r;
        r = a % b;
    }
    cout << "GCD" << b;
}
void main()
{
    GCD obj;
    obj.input();
    obj.find();
}
```

## 语法

```cpp
inline return_type function_name(argument list...)
{
    Body of function;
    Return(value/variable/expression);
}
```

使用内联函数有一些限制，例如

- 如果函数包含静态变量
- 如果函数包含循环、switch 或 goto 语句、条件语句
- 如果函数是递归的
- 如果函数包含 return 语句。

## 4.9 友元函数

在正常情况下，我们可以通过将数据成员声明在私有部分来隐藏/保护它们。但友元可以访问类的任何成员，无论其访问说明如何。关键字 friend 使函数成为类的非成员，即使其声明在类内部。

友元函数可以在类的任何位置声明。由于它不是类的成员，因此必须将对象作为其参数传递，以提取类的成员。

## 语法

```cpp
friend return_type function_name(data_type var,..........);
```

关键字 friend 可从四种不同的方式来学习

- 简单友元函数
- 带内联替换的友元
- 将友谊授予另一个类
- 两个或多个类拥有相同的友元函数。

## 4.9.1 简单友元函数

```cpp
#include<iostream.h>
class a
{
private:
    friend void display(a obj);
    int x;
};
void display(a obj)
{
    cout << "Enter a number";
    cin >> obj.x;
    cout << "The value is " << obj.x;
}
void main()
{
    a obj;
    display(obj);
}
```

## 输出

Enter a number 23
The value is 23

问题：友元函数在类内部声明，那么它是如何成为类的非成员的？

答：毫无疑问，友元函数在类内部声明，但它不遵循类成员的属性，这意味着如果我们要提取类的成员，则必须通过对象来访问，即 Object_name.member_name，但友元函数在 main() 中作为普通函数调用。第二点是，作为类的成员，如果我们要在类外部提供定义，则必须使用作用域解析运算符，但在这里我们将友元函数定义为普通函数。因此，从上述讨论中我们知道，即使友元函数在类内部声明，它也不是类的成员。

## 4.9.2 带内联替换的友元

```cpp
#include<iostream.h>
class a
{
private:
    int x;
public:
    friend void display(a obj);
};
inline void display(a obj)
{
    cout << "Enter a number";
    cin >> obj.x;
    cout << "The value is " << obj.x;
}
void main()
{
    a obj;
    display(obj);
}
```

## 4.9.3 将友谊授予另一个类（友元类）

在这种方法中，一个类可以将其友谊授予另一个类。例如，让我们考虑两个类 A 和 B。如果 A 将友谊授予 B，那么 B 有能力访问类 A 的成员，但反之则不然。

## 语法

```cpp
class A
{
    friend class B;
private:
    data member;
    member function();
public:
    data member;
    member function();
protected:
    data member;
    member function();
};
class B
{
private:
    data member;
    member function();
    return_type function_name(A obj);
public:
    data member;
    member function();
    return_type function_name(A obj);
protected:
    data member;
    member function();
    return_type function_name(A obj);
};
```

## 示例

```cpp
#include<iostream.h>
#include<stdio.h>
class std
{
    friend class mark;
private:
    char name[20], add[20];
    int age, roll, m[5], total;
    float avg;
public:
    void input();
};
class mark
{
public:
    void result(std obj);
};
void std :: input()
{
    total = 0;
    cout << "Enter the name and address";
    gets(name);
    gets(add);
    cout << "Enter the age, roll";
    cin >> age >> roll;
    cout << "Enter the marks in 5 subjects";
    for (int i = 0; i < 5; i++)
    {
        cin >> m[i];
        total = total + m[i];
    }
    avg = float(total) / 5;
}
void mark :: result(std obj)
{
    cout << endl << "NAME IS " << obj.name;
    cout << endl << "ADDRESS " << obj.add;
    cout << endl << "AGE IS " << obj.age;
    cout << endl << "ROLL IS " << obj.roll;
    for (int i = 0; i < 5; i++)
        cout << endl << "MARK " << i + 1 << " IS " << obj.m[i];
    cout << endl << "TOTAL IS " << obj.total;
    cout << endl << "AVERAGE IS " << obj.avg;
    if (obj.avg >= 50)
        cout << endl << "P A S S";
    else
        cout << endl << "F A I L";
}
void main()
{
    std obj;
    mark obj1;
    obj.input();
    obj1.result(obj);
}
```

## 4.9.4 多个类拥有相同的友元函数

友元函数也可用于不同的类。为此，如果 N 个类希望将一个友元函数作为共用，那么我们必须将 N-1 个类声明为前置声明。

```cpp
class name1;
class name2
........................
........................
class nameN-1;
class nameN
{
private:
    data member;
    member function();
public:
    data member;
    member function();
    friend return_type function_name(name1 obj1, name2 obj2, ..., nameN objn);
protected:
    data member;
    member function();
};
class name1
{
private:
    data member;
    member function();
public:
    data member;
    member function();
    friend return_type function_name(name1 obj1, name2 obj2, ..., nameN objn);
protected:
    data member;
    member function();
};
class nameN-1
{
private:
    data member;
    member function();
public:
    data member;
    member function();
    friend return_type function_name(name1 obj1, name2 obj2, ..., nameN objn);
protected:
    data member;
    member function();
}
```

## 示例

```cpp
#include<iostream.h>
class A;
class B;
class C
{
private:
    int x;
public:
    void input();
    friend void average(A obj1, B obj2, C obj2);
};
class A
{
private:
    int y;
public:
    void input();
    friend void average(A obj1, B obj2, C obj2);
};
class B
{
private:
    int z;
public:
    void input();
    friend void average(A obj1, B obj2, C obj2);
};
void C :: input()
{
    cout << "Enter a number";
    cin >> x;
}
void A :: input()
{
    cout << "Enter a number";
    cin >> y;
}
void B :: input()
{
    cout << "Enter a number";
    cin >> z;
}

void average(A obj, B obj1, C obj2)
{
    float avg;
    avg = float(obj2.x + obj.y + obj1.z) / 3;
    cout << "AVERAGE OF " << obj2.x << " " << obj1.z << " " << obj1.y << " IS " << avg;
}
void main()
{
    A obj;
    B obj1;
    C obj2;
    obj.input();
    obj1.input();
    obj2.input();
    average(obj, obj1, obj2);
}
```

## 4.10 静态数据成员和成员函数

static 是一个存储类说明符，通常用于声明具有特定性的变量，与其他普通变量相比，即使变量超出函数作用域，它也能保持变量值的一致性。在 C++ 中，我们可以将 static 用于类的成员。当我们将数据成员声明为 static 时，变量的初始化值为零，并且它会为所有对象创建变量的单个副本，该副本由所有对象共享。静态变量的作用域是局部的，但它的工作方式类似于全局变量。

静态数据成员在编译期间分配内存，而非静态数据成员在编译期间分配内存。

在 main 函数之前，我们必须定义静态数据成员，如下所示

```cpp
data_type class_name :: variable;
or
data_type class_name :: variable = value;
```

## 普通数据成员与静态数据成员的区别

```cpp
class demo
{
private:
    int x;
};
void main()
{
    demo obj1, obj2, obj3;
    .........
    .........
}
```

在上述情况下，对于三个对象 obj1、obj2、obj3 将创建数据成员 'x' 的 3 个副本。因此，如果我们通过 obj1 更改 'x'，则不会影响 obj2 和 obj3 的 'x'。

```cpp
class demo
{
private:
    static int x;
};
int demo :: x;
void main()
{
    demo obj1, obj2, obj3;
    .........
    .........
}
```

在这种情况下，它不会创建三个副本，而是为所有对象创建数据成员 'x' 的单个副本，并由对象共享。因此，如果我们通过 obj1 更改数据成员的值，则会影响 obj2 和 obj3。

