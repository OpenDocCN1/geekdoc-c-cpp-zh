
```cpp
    }
    else
    {
        cout<<"Addition is not possible"<<endl;
    }
return res;
}
Matrix sub(Matrix t)
{
int i,j;
Matrix res;
res.rows=rows;
res.cols=cols;
if(rows==t.rows && cols==t.cols)
{
for(i=0;i<=rows-1;i++)
{
for(j=0;j<=cols-1;j++)
{
    res.mat[i][j]=mat[i][j]-t.mat[i][j];
}
}
}
else
{
    cout<<"Subtraction is not possible"<<endl;
}
return res;
}
Matrix multiply(Matrix t)
{
int i,j,k;
Matrix res;
if(cols==t.rows)
{
res.rows=rows;
res.cols=t.cols;
for(i=0;i<=rows-1;i++)
{
for(j=0;j<=t.cols-1;j++)
{
    res.mat[i][j]=0;
    for(k=0;k<=cols-1;k++)
```

```cpp
int b;
void input()
{
    cin>>a>>b;
}
void output()
{
    cout<<a<<b;
}
};
void main()
{
    DATA o1,o2;
    o1.a=10;
    o1.b=20;
    o2.input();
    o1.output();
    o2.output();
}
```

### 程序2

```cpp
#include<iostream.h>
void main()
{
    DATA d1,d2;
    d1.input();
    d1.output();
    d2.input();
    d2.output();
}
class DATA
{
private:
int x;
int y;
public:
    void input()
    {
        cin>>x>>y;
    }
    void output()
    {
        cout<<x<<" "<<y;
    }
};
```

### 程序3

```cpp
#include<iostream.h>
class Student
{
private:
int roll_no;
char name[100];
public:
    void input()
    {
    cin>>roll_no>>name;
    }
    void output()
    {
    cout<<roll_no<<" "<<name<<endl;
    }
};
void main()
{
Student s1;
s1.input();
s1.output();
Student s2,s3;
s2.output();
s3.output();
}
```

### 程序4

```cpp
#include<iostream.h>
class NUMBER
{
private:
int x;
int f;
public:
    void input()
    {
    cout<<"Enter x";
    cin>>x;
    }
    f=1;
    while(x>0)
    {
    f=f*x;
```

```cpp
o2.set_data(20);
o1.increment();
o2.increment();
o1.output();
o2.output();
}
```

### 程序6

```cpp
#include<iostream.h>
class Course
{
private:
char name[100];
float fees;
public:
    void input()
    {
        cin>>name>>fees;
    }
    void output()
    {
        cout<<"name="<<name<<"fees="<<fees<<endl;
    }
};
void main()
{
Course c1;
Course *p;
p->input();
p->output();
Course *q;
q->input();
q->output();
}
```

### 测验

- 1. 以下哪项不是OOP范式的特征？
  - (a) 封装
  - (b) 数据隐藏
  - (c) 安全性
  - (d) 模块化
- 2. 以下哪项（哪些）陈述是正确的？
  - (a) 结构体不支持封装，而类支持封装。
  - (b) 结构体的所有成员默认是私有的，而类的所有成员默认是公有的。
  - (c) 结构体的所有成员默认是公有的，而类的所有成员默认是私有的。
  - (d) 结构体和类没有区别。
- 3. 友元函数的主要用途是
  - (a) 实现数据隐藏
  - (b) 实现多态
  - (c) 在类的作用域之外访问类的私有成员
  - (d) 实现封装
- 4. 类的成员变量的内存是在何时分配的
  - (a) 创建类的对象时
  - (b) 定义类时
  - (c) 创建指向类的指针时
  - (d) 成员变量被初始化为特定值时
- 5. 以下哪个运算符可用于通过指针访问类的成员
  - (a) 成员运算符（.）
  - (b) 箭头运算符（->）
  - (c) 地址运算符（&）
  - (d) 以上都不是
- 6. 数据隐藏和封装的优点是
  - (a) 它们向程序员隐藏了代码的复杂性
  - (b) 它们有助于代码的可重用性
  - (c) 它们为类的私有变量提供安全性
  - (d) 它们减少程序的代码行数
- 7. 当使用对象调用类的成员函数时，这称为
  - (a) 抽象
  - (b) 消息传递
  - (c) 多态
  - (d) 继承
- 8. 对象默认通过何种方式传递给函数
  - (a) 值传递
  - (b) 引用传递
  - (c) 地址传递
  - (d) 对象不能作为参数传递给函数

### 复习题

- 1. 为什么需要面向对象编程？请举例说明。
- 2. 简要说明C++中的类和对象。
- 3. 编写一个C++程序，创建一个名为Student的类，成员包括roll_number、names和marks。将n名学生的数据存储在计算机内存中，并按成绩升序排列这n名学生。
- 4. 编写一个C++程序，创建一个名为Polar的类，包含radius和angle两个成员。编写一个add()函数以执行Polar对象的加法。
- 5. 编写一个C++程序，创建一个名为`Date`的类，包含成员`dd`、`mm`和`yyyy`。创建一个成员函数`diff()`来求两个日期之间的天数。在求两个`Date`对象之间的差值时，还要考虑闰年的情况。
- 6. 解释指针与对象的使用。并举例说明使用指针调用类的成员函数的过程。
- 7. 创建对象数组有什么优点？与基本类型数组相比有何不同？
- 8. 简要说明友元函数。给出一个C++中友元函数的例子。友元函数有什么缺点？
- 9. 什么是封装和数据隐藏？举例说明。
- 10. 编写一个C++程序，重载函数`root()`以返回整数、浮点数和长整型数据类型的平方根。并写出该程序的输出。

## 第12章：构造函数和析构函数

### 12.1 概述

我们知道，C++中的类是一种用户定义的数据类型，它将成员和成员函数组合成一个单元。回顾第11章，数据隐藏和封装是面向对象编程范式的关键特性。因此，建议将类内创建的变量设为私有，将类内定义的函数设为公有，这样，类内定义的私有变量的值只能通过该类的公有函数访问。这一特性为类的私有成员提供了安全性，因为它们只能使用该类定义的公有函数访问。

此外，正如我们为基本类型的变量提供初始值一样，我们可能也需要为程序中创建的每个对象的成员变量提供初始值。例如，让我们考虑一个ShoppingCart类，其对象可以存储客户在在线购物系统中购买的商品列表。如图12.1所示，

![](img/57c0d966bb33c67a5a188e6bf39e4e02_667_0.png)

**图12.1：** ShoppingCart类的伪代码

我们在ShoppingCart类中创建一个变量count，它表示客户要购买的商品数量。因此，每当创建一个新购物车时，变量count的初始值（表示购物车中的商品数量）必须设置为零。显然，每当向购物车中添加一个商品时，必须递增变量count的值，以表示任意时刻购物车中的商品数量。因此，我们包含了一个函数addItem()，当商品添加到购物车时，它会递增count的值，如图12.1所示。此外，我们还编写了一个函数setInitialValue()，它将变量count的初始值设置为零，表示空购物车。

因此，每当创建新的ShoppingCart对象时，程序员有责任调用函数setInitialValue()将变量count的初始值设置为零。这意味着创建ShoppingCart对象需要在程序中编写以下两条语句，才能使完整程序准确运行：

```cpp
ShoppingCart c1;
c1.setInitialValue();
```

上面的第一条语句创建了名为c1的ShoppingCart类对象，第二条语句调用了成员函数setInitialValue()，它将变量count的初始值设置为零。类似地，如果我们创建该类的n个对象，如c1、c2……cn，那么现在程序员有责任为每个对象c1到cn调用函数setInitialValue()，如图12.2所示。这是因为，客户创建的每个新购物车在程序中必须最初保持为空。

因此，如图12.2所示，我们需要为ShoppingCart类的每个对象重复调用同一个函数。这是因为，ShoppingCart类的每个对象都有一个共同需求：将成员count的初始值设置为零。当程序中要创建大量ShoppingCart对象时，这可能给程序员带来额外开销。在C++中，可以使用“构造函数”来避免这种为每个对象设置初始值而重复调用函数的开销。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_668_0.png)

**图12.2：** 创建ShoppingCart类的多个对象

