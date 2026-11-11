

### 问题7. 以下程序的输出是什么？

```cpp
#include <iostream.h>

class MyClass {
    int a;
protected:
    int b;
public:
    int c;
    MyClass(int n, int m) {
        a = n;
        b = m;
    }
    int geta() {
        return a;
    }
    int getb() {
        return b;
    }
};

int main()
{
    MyClass object(10, 20);
    object.c = 30;
    cout << object.geta() << ' ';
    cout << object.getb() << ' ' << object.c << '\n';
    return 0;
}
```

**答案。** 上述程序的输出如下：

```text
10 20 30
```

### 问题8. 以下程序的输出是什么？

```cpp
#include <iostream.h>

class NumberDisplay{
    int num1;
    int num2;
public:
    NumberDisplay(int x, int y) {
        num1 = x;
        num2 = y;
    }
    int getNum1() {
        return num1;
    }
    int getNum2() {
        return num2;
    }
};

int main()
{
    NumberDisplay object1(7, 9), object2(5, 2);
    cout << "Values in object1 are " << object1.getNum1() << " and " <<
         object1.getNum2() << endl;
    cout << "Values in object2 are " << object2.getNum1() << " and " <<
         object2.getNum2() << endl;

    return 0;
}
```

**答案。** 上述程序的输出如下：

```text
Values in object1 are 7 and 9
Values in object2 are 5 and 2
```

### 问题9. 以下程序的输出是什么？

```cpp
#include <iostream.h>

class InLineUse {
    int a, b;
public:
    void init(int i, int j);
    void show();
};

inline void InLineUse::init(int i, int j)
{
    a = i;
    b = j;
}

inline void InLineUse::show()
{
    cout << a << " " << b << "\n";
}

int main()
{
    InLineUse x;
    x.init(100, 500);
    x.show();
    return 0;
}
```

**答案。** 上述程序的输出如下：

| 100 | 500 |
|---|---|
### 问题10. 以下程序的输出是什么？

```cpp
#include <iostream.h>

class Stack {
    int stck[3],size,top;
public:
    Stack();
    ~Stack();
    void push(int i);
    int pop();
};

Stack::Stack(){
    top = 0;
    size=3;
    cout << "Stack Initialized\n";
}

Stack::~Stack(){
    cout << "Stack Destroyed\n";
}
void Stack::push(int i){
    if( top == size ) {
        cout << "Stack is full.\n";
        return;
    }
    stck[ top ] = i;
    top++;
}
int Stack::pop() {
    if( top == 0 ) {
        cout << "Stack underflow.\n";
        return 0;
    }
    top--;
    return stck[ top];
}
int main()
{
    Stack a, b;
    for(int i=0,j=10;i<3;i++)
    {
        a.push(j);
        j=j+10;
    }
    for(int k=0,l=100;k<3;k++)
    {
        b.push(l);
        l=l+100;
    }
    for(i=0;i<3;i++)
    {
        cout<<a.pop()<<" ";
    }
    cout<<endl;
    for(k=0;k<3;k++)
    {
        cout<<b.pop()<<" ";
    }
    cout<<endl;
    return 0;
}
```

**答案。** 上述程序的输出如下：

```text
Stack Initialized
Stack Initialized
30 20 10
300 200 100
Stack Destroyed
Stack Destroyed
```

### 问题11. 以下程序的输出是什么？

```cpp
#include <iostream.h>

class StaticUse {
    static int i;
public:
    static void init(int x) {
        i = x;
    }
    void show() {
        cout << i;
    }
};
int StaticUse::i;
int main()
{
    StaticUse::init(40);
    StaticUse x,y;
    x.show();
    y.show();
    return 0;
}
```

**答案。** 上述程序的输出如下：

```text
4040
```

### 问题12. 以下程序的输出是什么？

```cpp
#include <iostream.h>

class ThisPtr {
    int a, b;
public:
    ThisPtr(int n, int m) {
        this->a = n;
        this->b = m;
    }
    int add() {
        return this->a + this->b;
    }
    void show();
};

void ThisPtr::show()
{
    int t;

    t = this->add();
    cout << t << endl;
}

int main()
{
    ThisPtr ob(10, 14);
    ob.show();
    return 0;
}
```

**答案。** 上述程序的输出如下：

```text
24
```

## 07 关于继承

### 目标

- 7.1 探索基类和派生类的概念
- 7.2 使用 protected 访问说明符
- 7.3 创建简单的继承程序
- 7.4 解释各种派生类型
- 7.5 重写基类成员
- 7.6 调用基类和派生类的构造函数和析构函数
- 7.7 创建容器类
- 7.8 解释继承的形式
- 7.9 描述实现多重继承时的一些问题
- 7.10 创建和使用指针对象
- 7.11 实现静态绑定和动态绑定

继承是面向对象编程（OOP）的一个重要特性。它是一种机制，其中一个类获取另一个类的属性和功能。例如，Dog 这样的类从哺乳动物类继承眼睛颜色和毛发颜色等特征。继承或派生自另一个类的类称为派生类或子类，而被继承的类称为基类或超类。继承使你能够在新的 C++ 程序中重用现有程序的代码。如果现有程序不能满足新项目的要求，你也可以修改现有程序的代码。

在 C++ 中，当从基类派生一个类时，基类通过访问说明符来指定，访问说明符是以下关键字之一：

- public
- protected
- private

根据访问说明符，C++ 中恰好有三种派生类型，包括私有派生、保护派生和公有派生。访问说明符出现在基类名称之前，并且仅适用于该基类。访问说明符控制基类成员在派生类中的可访问性或可见性。如果使用 virtual 关键字指定基类名称，则该基类称为虚基类。你也可以从一个由逗号分隔的多个基类继承一个类。这种继承类型称为多重继承。

在本章中，你将学习使用基类和派生类以及 protected 访问说明符的继承机制。你还将学习三种派生类型：私有、保护和公有，以及派生类如何重写基类的成员。此外，你还将了解在实现继承时构造函数和析构函数的调用顺序，以及容器类。本章还讨论了不同形式的继承，例如单继承、多重继承和多级继承。它解释了实现多重继承时编译器会出现的问题。接下来，你将学习如何创建和使用基类和派生类的指针对象来访问其成员。本章最后描述了绑定（binding）的概念，以及通过虚函数、纯虚函数和抽象类实现动态绑定。

让我们首先探索继承中基类和派生类的概念。

### 7.1 探索基类和派生类的概念

如前所述，继承或派生自另一个类的类称为派生类，而被继承的类称为基类。基类也称为超类，派生类也称为子类。

派生类的实例包含基类的大部分特征。因此，派生类可能包含比其基类更多的特征。派生类可以修改基类的部分或全部继承特征。图1显示了基类（Car）和派生类（Maruti Zen）之间的关系：

![](img/8a6886c00caa6a1651a6c0e62bff341f_471_0.png)

▲ 图1：显示基类和派生类之间的关系

在图1中，派生类 Maruti Zen 继承了基类 Car 的多种特征，例如 `no_of_tyres`、转向和 `no_of_lights`，并且还有自己的特征，例如自动锁和空调。图1中的箭头表示继承的方向；也就是说，Car 是基类，Maruti Zen 是派生类。箭头从派生类指向基类的方向表示派生类能够访问基类的特征；反之则不能。

在 C++ 中创建和使用基类和派生类的一些优点是：

- 减少代码冗余，因为代码位于一处，即基类中。
- 使您能够轻松维护源代码。这是因为对基类所做的任何更改都会自动反映在其派生类的行为中；因为这些类会自动继承新行为。
- 通过向派生类添加函数来扩展基类（或现有类）的功能。

在 C++ 中，从现有类（或基类）继承新类（或派生类）的基本语法是：

```cpp
class <BaseClass>
{
...
};
class <DerivedClass> : <access_specifier> <BaseClass>
{
...
};
```

在前面的语法中，基类和派生类前面都有 `class` 关键字。声明派生类时，需要在派生类名称和访问说明符之后指定基类的名称。派生类名称后面跟着冒号（`:`）符号。访问说明符（`public`、`private` 或 `protected`）指示派生或继承的类型。

以下代码片段显示了派生类和基类的示例：

```cpp
class Dog: public Mammal
```

在前面的代码片段中，Dog 指从基类 Mammal 派生的派生类。

派生类型将在本章的*解释各种派生类型*一节中讨论。现在，始终使用 `public` 访问说明符从基类继承派生类。在从基类继承派生类之前，必须先声明基类；否则，会出现编译错误。

现在，让我们讨论 protected 访问说明符，它在继承中起着重要作用。

