

现在我们可以声明并使用 Derived 类对象：

```
int main() {
   Derived d(10, 2);
   cout << "value = " << d.getValue() << endl;
   return 0;
}
```

请注意，这里调用的是 Derived 类的 getValue() 成员函数，它返回用于初始化对象的两个值的乘积。上述代码生成的输出为：

```
value = 20
```

## 通过指针访问成员函数

现在让我们声明一个 Base 类指针，并为所寻址的对象调用 getValue() 成员函数：

```
int main() {
   Base *bptr;
   bptr = new Base(10);
   cout << "value = " << bptr->getValue() << endl;
   return 0;
}
```

上述代码生成的输出为：

```
value = 10
```

这与预期一致。

现在我们可以声明一个指向 Derived 类对象的指针，并调用在 Derived 类中定义的替换 getValue() 成员函数。

```
int main() {
    Derived *dptr;
    dptr = new Derived(10, 2);
    cout << "value = " << dptr->getValue() << endl;
    return 0;
}
```

上述代码生成的输出为：

```
value = 20
```

这也与预期一致。

应用 C++ 关于指针和派生类的规则，我们还可以声明一个指向 Base 类的指针，并将 Derived 类对象的地址赋给该指针：

```
int main() {
    Base *bptr;
    bptr = new Derived(10, 2);
    cout << "value = " << bptr->getValue() << endl;
    return 0;
}
```

请注意，bptr 被声明为寻址 Base 类的对象，我们创建了一个 Derived 对象并将该对象的地址赋给了 bptr。但请看这段代码生成的输出：

```
value = 10
```

代码可以编译，但它没有产生预期的结果，即：

```
value = 20
```

就 C++ 所知，bptr 寻址的是一个 Base 类对象。因此，C++ 调用 Base 类中的 getValue() 成员函数！C++ 规则是，由指针本身的类型决定调用哪个成员函数。被指向对象的类型根本不会被考虑！

## 虚函数

但我们确实希望 C++ 调用指针实际寻址的 Derived 对象的 getValue() 成员函数。为了实现这一点，我们必须将 getValue() 声明为虚成员函数。对虚函数的调用在运行时链接（晚期绑定）。虚成员函数和晚期绑定使得对象能够在运行时确定自身行为，这是多态性的主要特征。就 C++ 而言，需要一种方法，将哪个成员函数执行的选择推迟到执行时间。

拥有这种方法意味着，通过使用单个指针和成员函数名，可以将相同的函数调用（消息）发送到指针中存储其地址的对象。如果这些对象以不同方式实现相同的成员函数，则可以获得不同的结果！这种方法称为晚期或动态绑定，因为调用哪个成员函数的决定不再在编译时做出，而是在运行时做出。C++ 规则如下：

> "如果基类定义中的函数被声明为虚函数，并且在一个或多个派生类中以完全相同的方式声明（包括返回类型），那么使用 Base 类类型的指针或引用对该函数的所有调用都将调用由被指向对象指定的函数，而不是由指针本身的类型指定的函数。"

以下代码演示了此规则：

```
// virtual1.cpp
#include <iostream>
using namespace std;
class Base {
    protected:
        int value;
    public:
        Base (int x) { value = x; }
        virtual int getValue() { return value; }
};

class Derived : public Base {
    protected:
        int mult;
    public:
        Derived(int x, int y) : Base(x), mult(y) {}
        virtual int getValue() { return value * mult; }
};

int main() {
    Base *bptr;

    bptr = new Base(10);
    cout << "value = " << bptr->getValue() << endl;
    delete bptr;

    bptr = new Derived(10, 2);
    cout << "value = " << bptr->getValue() << endl;
    delete bptr;

    return 0;
}
```

关键字 virtual 告诉编译器，对 getValue() 的调用应在运行时链接。两个 getValue() 虚成员函数的地址存储在一个内部表中。当语句调用虚成员函数时，C++ 会从此表中查找正确的函数地址。我们稍后会详细讨论这一点。但如果你认为这个查找操作需要时间，你是正确的。使用虚成员函数可能会降低程序的性能（两次额外查找），尽管在实践中严重的减速情况很少见。

上述程序产生的输出为：

```
value = 10
value = 20
```

现在比较上面的两个输出语句。它们完全相同！那么它们如何产生不同的输出呢？我们现在有足够的信息来回答这个问题。被寻址的对象自己确定调用哪个虚 getValue() 成员函数。该决定由程序在运行时而非编译时做出。

请注意，一旦我们在类中将函数声明为虚函数，任何使用相同原型声明相同函数的子类也被视为虚函数。请记住，晚期绑定在 C++ 中仅对类层次结构中的对象有意义。对于未用作基类的类声明虚函数在语法上是正确的，但会导致不必要的运行时开销。

将多态性视为对消息的响应可能会有所帮助。在经典面向对象编程术语中，诸如：

```
bptr->getValue()
```

向 bptr 所寻址的对象发送名为 getValue() 的消息。收到此消息后，对象以某种预定方式响应。更重要的是，相同的消息可以发送到其他对象，这些对象确定自己的响应，或者它们可能忽略该消息。无论 bptr 寻址哪种类型的对象，对象本身都会以其编程方式响应 getValue() 消息。

以下是另一个示例：

```
// virtual2.cpp

#include <iostream>
using namespace std;

class Base {
public:
    void show() { cout << "Base" << endl; }
};

class Derived1 : public Base {
public:
    void show() { cout << "Derived1" << endl; }
};

class Derived2 : public Base {
public:
    void show() { cout << "Derived2" << endl; }
};

int main() {
    Derived1 dv1;
    Derived2 dv2;
    Base *bptr;

    bptr = &dv1;
    bptr->show();

    bptr = &dv2;
    bptr->show();
    return 0;
}
```

现在，当我们执行以下行时：

```
bptr = &dv1;
bptr->show();
```

调用哪个成员函数：

```
Base::show()
or
Derived1::show()
```

或者当我们执行以下行时：

```
bptr = &dv2;
bptr->show();
```

调用哪个成员函数：

```
Base::show()
or
Derived2::show()
```

在每种情况下，被调用的成员函数都是：

```
Base::show()
```

产生以下输出：

```
Base
Base
```

编译器只是忽略指针 bptr 的内容，并选择与指针本身类型匹配的成员函数。

我们可以再次通过在 Base 类中 show() 成员函数的声明前放置关键字 virtual，并可选地在派生类中放置，来更改此行为。

```
// virtual3.cpp
#include <iostream>
using namespace std;
class Base {
  public:
    virtual void show() { cout << "Base" << endl; }
};
class Derived1 : public Base {
  public:
    virtual void show() { cout << "Derived1" << endl; }
};
class Derived2 : public Base {
  public:
    virtual void show() { cout << "Derived2" << endl; }
};

int main() {
    Derived1 dv1;
    Derived2 dv2;
    Base *bptr;

    bptr = &dv1;
    bptr->show();

    bptr = &dv2;
    bptr->show();
    return 0;
}
```

现在生成的输出为：

```
Derived1
Derived2
```

现在执行的是派生类的成员函数，而不是 `Base` 类的成员函数。因此函数调用：

```
bptr->show();
```

根据指针本身的内容执行不同的函数。再次强调，规则是被调用的函数基于指针的内容，而不是基于指针的类型，与之前一样。

## 纯虚函数

在我们之前的示例中，`Base::show()` 永远不会被执行。这是一种常见情况。通常不需要特定函数的基类版本。我们只使用派生类中的函数版本。当这种情况成立时，可以删除基类中虚函数的函数体，并在函数声明中添加符号 `=0`：

