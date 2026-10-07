
就 C++ 而言，`bptr` 指向一个基类（Base）对象。因此，C++ 调用了基类中的 `getValue()` 成员函数！C++ 的规则是：由指针本身的类型决定调用哪个函数。所指向的对象的类型根本没有被考虑在内！

## 虚函数

但我们真的希望 C++ 调用指针所指向的派生类（Derived）对象的 `getValue()` 成员函数。为了实现这一点，我们必须将 `getValue()` 声明为虚成员函数。虚函数的调用在运行时链接（晚绑定）。虚成员函数和晚绑定使得对象能够在运行时决定自己的行为，这是多态的核心特征。在 C++ 中，这需要一种方法，将“选择执行哪个成员函数”的选择推迟到程序执行时。

拥有这样的方法意味着，通过使用单个指针和成员函数名，可以将同一个函数发送到指针中存储了其地址的对象。由于这些对象以不同的方式实现了同一个成员函数，那么就可以获得不同的结果！这种方法被称为晚绑定或动态绑定，因为调用哪个成员函数的决策不再在编译时做出，而是在运行时做出。C++ 的规则如下：

> “如果基类定义中的一个函数被声明为虚函数，并且在一个或多个派生类中完全相同的方式声明（包括返回类型），那么所有使用基类类型指针或引用对该函数的调用都将调用由所指向的对象指定的函数，而不是由指针本身的类型。”

下面的代码演示了这一规则：

```cpp
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
```

```cpp
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
  cout << "Value = " << bptr->getValue() << endl;
  delete bptr;

  bptr = new Derived(10, 2);
  cout << "Value = " << bptr->getValue() << endl;
  delete bptr;
  return 0;
}
```

`virtual` 关键字告诉编译器对 `getValue()` 的调用将在运行时链接。两个 `getValue()` 成员函数的地址存储在一个内部表中。当语句调用虚成员函数时，C++ 会从该表中查找正确的函数地址。我们稍后会详细讨论这一点。但如果你认为这个查找动作需要耗时，那么你是正确的。使用虚成员函数可能会降低程序的性能（两次额外的查找），尽管在实践中严重的减速是稀缺的。

上述程序产生的输出是：

```
value = 10
value = 20
```

现在比较上面的两个输出语句。它们完全相同！那么它们是如何产生不同输出的呢？我们现在有足够的信息来回答这个问题。被指向的对象自己决定调用两个虚 `getValue()` 成员函数中的哪一个。这个决策是由程序在运行时做出的，而不是编译时。

注意，一旦我们在类中将一个函数声明为虚函数，任何以相同原型声明相同函数的子类也都被视为虚函数。请记住，在 C++ 中，晚绑定对于类层次结构一部分的对象才有意义。对于一个不作为基类的类声明虚函数，在语法上是正确的，但会导致不必要的运行时开销。

将多态类为对消息的响应可能很有帮助。在经典的面向对象编程术语中，如下表达式：

```cpp
bptr->getValue()
```

向 `bptr` 指向的对象发送一个名为 `getValue()` 的消息。接收到此消息后，对象以某种预定义方式响应。更重要的是，相同的消息可以发送给其他决定自己响应的对象，或者它们可能会忽略该消息。无论 `bptr` 指向什么类型的对象，对象本身按照其编程方式对 `getValue()` 消息做出响应。

这是另一个例子：

```cpp
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
```

```cpp
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

现在，当执行以下行时：

```cpp
bptr = &dv1;
bptr->show();
```

调用了哪个成员函数：

Base::show()
或
Derived1::show()

或者当执行以下行时：

```cpp
bptr = &dv2;
bptr->show();
```

调用了哪个成员函数：

Base::show()
或
Derived2::show()

在每情况下，调用的成员函数都是：

```
Base::show()
```

产生以下输出：

```
Base
```

等待，规则是函数根据指针的内容而不是指针的类型来决定的。我们可以通过在基类的函数声明前放置 `virtual` 关键字，并可选地在派生类中提供体来改变这种行为。

现在的输出是：

```cpp
// virtual3.cpp

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
```

```cpp
int main() {
    Base *bptr;
    Derived1 dv1;
    Derived2 dv2;

    bptr = &dv1;
    bptr->show();

    bptr = &dv2;
    bptr->show();
    return 0;
}
```

产生的输出是：

```
Derived1
Derived2
```

你可能会想，如果我们移除基类中虚函数的体，为什么不直接删除函数呢？那样会更简洁，但行不通。基类中没有 `show()` 函数，如下语句：

```
list[0]->show();
```

将无效。

## 纯虚函数

在我们之前的示例中，不需要某个函数的基类版本。我们只使用派生类中的版本。当这样做时，可以移除基类中虚函数的体，并在函数声明上添加 `=0`：

```cpp
class Base {
public:
    virtual void show() = 0;
};
```

`=` 符号与赋值无关，`0` 也没有赋值给任何东西。`=0` 语法仅仅告诉编译器某个函数是纯的，即没有体。这被称为纯虚函数。

```cpp
// virtual.cpp

#include <iostream>

using namespace std;

class Base {
public:
    virtual void show() = 0;
};

class Derived1 : public Base {
public:
    virtual void show() {
        cout << "Derived1" << endl;
    }
}

class Derived2 : public Base {
public:
    virtual void show() {
        cout << "Derived2" << endl;
    }
};

int main() {
    Base *list[2];
    Derived1 dv1;
    Derived2 dv2;
    list[0] = &dv1;
    list[1] = &dv2;
    for (int i=0; i<2; i++)
        list[i]->show();
}
```

产生的输出是：

```
Derived1
Derived2
```

这是另一个例子。

```cpp
// student.cpp

#include <iostream>

using namespace std;

class Person {
protected:
    char name[40];
public:
    void setName() {
        cout << "Enter name: ";
        cin >> name;
    }
    void getName() {
        cout << "Name is: " << name << endl;
    }
    virtual int isOutstanding() = 0;
};
```
