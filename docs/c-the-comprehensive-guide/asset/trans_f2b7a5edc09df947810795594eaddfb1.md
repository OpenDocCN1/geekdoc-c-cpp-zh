

## 二叉树

Tree 实现了一棵*二叉树*。每个节点最多可以有两个子节点。在搜索过程中始终向右或向左分支，在最优情况下，每次比较都能排除树中一半的元素。这意味着，在一棵有 1,000,000 个节点的树中，访问大约 20 个节点后，你就可以确定键是否存在。

然而，请注意，这仅适用于*最优*情况。在最坏情况下，如果你按有序顺序插入元素，你将不得不查看 1,000,000 个节点！这是因为这个简单算法不会*平衡*树。为此有像*红黑树*或*AVL 树*这样的复杂机制，但详细说明这些将超出本书范围。

如果你想在排序树结构中存储数据键，只需使用第四部分的 `map`。`map` 数据类型保证树是平衡的，并且还能处理移动和迭代器。

## 18.2 非公有继承

当一个类从前驱继承某些内容时，通常用 `public:` 引入基类：

```cpp
// https://godbolt.org/z/Pq5aWq8xr
#include <iostream>
using std::cout; using std::ostream;
// ... as before ...
struct NormalCase : public DerivedPublic {
    void print() {
        cout << xPublic;
        cout << xProtected;
    }
};

struct SpecialCase : public DerivedPrivate {
    void print() {
        cout << xPublic;             // ✗ no access
        cout << xProtected;          // ✗ no access
    }
};
int main() {
    NormalCase n {};
    n.print();                       // Output: 12
    SpecialCase s {};
    s.print();
}
```

**清单 18.5** 进一步派生时的继承可见性。

SpecialCase 类从其祖先 DerivedPrivate 公有继承，但它通过 DerivedPrivate : private Base 包含了 Base 类。因此，Base 的所有字段都变为私有，像 SpecialCase 这样的进一步派生类不再具有直接访问权限。

当选择这种方法时，中间的类自然会使用基类的属性，因此最终的类也会间接使用这些属性。

```cpp
// https://godbolt.org/z/WYqYe7PoY
#include <iostream>
using std::cout; using std::ostream;
class Base {
    public: int data = 5;
};
class Middle : private Base {
protected: void print() {
        cout << data;  // data is inherited privately here
    }
};
class Ultimately : public Middle {
public: void go() {
    print();             // 'data' is not visible; 'print' is protected visible
}
};
int main() {
    Ultimately u {};
    u.go();              // output: 5
}
```

**清单 18.6** 在实践中，子类间接使用私有继承的成员。

在 main 中，我实例化 Ultimately 并调用其唯一的公有方法 go。在它里面，我可以访问从 Middle 继承的 print() 方法。data 字段不可见，但继承的 print 方法会自然地间接使用该字段。

### 18.2.2 实践中的非公有继承

在实际开发中，公有继承是迄今为止最常见的。你也应遵循这一做法，把受保护和私有继承留给极端特殊情况。

在像 Java 这样的语言中，所有继承都是公有继承。

有时你会看到私有继承用于不是 is-a 关系而是 has-a 关系的情况。因为被继承类 B 的接口不会成为继承类 D 的接口的一部分，所以类 D 在外部不会表现为一个 B，因此实际上并不是一个 B。

在我解释私有继承之前，你知道如何在 C++ 中表示这种 has-a 关系吗？是的，你会知道：不要让 B 成为 D 的祖先，而应把它作为数据成员。一般来说，你应优先使用数据成员。但有时使用继承是值得的。因此，私有继承有时也被称为*由...实现*关系。

对于受保护继承，从外部角度看，与私有继承相同。在更大的类层次结构中，可见性方面存在细微差异，但它仍然是一种由...实现关系。这种继承在实践中甚至更少有用。下面的清单是一个如何实现 has-a 关系的具体示例。

```cpp
// https://godbolt.org/z/ETr73T5a9
class Engine {
public:
    Engine(int numCylinders);
    void start();             // start engine
};

class Car : private Engine {    // Car has an engine
public:
  Car() : Engine{8} { }        // initializes a car with 8 cylinders
    using Engine::start;       // starts car by starting the engine
};
```

清单 18.7 通过私有继承实现的 has-a 关系。

这里你会看到 using 的另一种用法。有几种情况会使基类中的方法不再可见——这就是其中之一。Engine 的 start 方法在 Car 中通常只是私有的，因为 Engine 是通过私有继承——一种 has-a 继承——包含的。为了让公有方法在 Car 中可见，你可以在适当的部分用 using Engine::start 声明来自 Engine 的 start 标识符。如果 start 有多个重载，它们都会自动包含。或者，你可以通过将方法重写为 `void start() { Engine::start(); }` 来使其更明确。

### 遮蔽

简短题外话：可以在派生类中重写一个方法，同时给它不同的签名。被重写的版本随后就被遮蔽——它被隐藏起来，不再可见：

```cpp
// https://godbolt.org/z/Gb3zx1j7
#include <string>
struct Base {
    void func(int x) {};
};
struct Derived : public Base {
    void func(std::string y) {};   // shadows func(int)
};
int main() {
    Derived d;
    d.func("Text");
    d.func(3);                     // ❌ Error: func(int) is no longer visible
}
```

d.func(3) 调用再也看不到 func(int) 重载。你需要删除 Derived 类中 func(string) 的定义才能让它再次工作（并在 main() 中删除 d.func("Text")）。

以这种方式遮蔽方法通常不可取。你应该分配新名称。如果你想重写并使用虚方法，那么使用 `override` 来确保你确实在重写。

使用成员的常规实现如下面的清单所示。（基类）`Engine` 类保持不变。

```cpp
// https://godbolt.org/z/67EjhMf54
class Car {
public:
    Car() : engine_{8} { }        // initializes a car with 8 cylinders
    void start() { engine_.start(); } // starts the car by starting the engine
private:
    Engine engine_;               // Car has-a engine
};
```

**清单 18.8** 使用成员实现的 has-a 关系。

两种实现的共同点如下：

- 在两种情况下，每个 `Car` 实例中恰好有一个 `Engine`。
- 在两种情况下，`Car*` 类的使用者都不能将其转换为 `Engine*`，而公有继承时则可能这样转换。
- 在两个示例中，`Car` 都有一个 `start()` 方法，该方法会调用所包含发动机的 `start()` 方法。

然而，也存在差异。对于继承变体，以下情况适用：

- 如果 `Car` 应包含多个 `Engine` 实例，则不能选择这种方式。
- `Car` 的成员可以将 `Car*` 转换为 `Engine*`。
- `Car` 的方法可以访问 `Engine` 的*受保护*字段。
- `Car` 可以重写 `Engine` 的虚方法。

> **何时应使用私有继承来表示 has-a 关系？**
>
> 答案很简单：只要可以就用成员，必须用时才用私有继承；而必须用的情况仅涉及*受保护*成员或虚方法。

## 18.3 作为接口的签名类

签名类在 C++ 中并不是额外的东西；它们没有额外的语法要求或关键字。它们只是你已经知道的一种特殊形式的名称：一个只有纯虚方法的类就是*签名类*。提醒一下，纯虚方法是没有实现的虚方法，在源代码中用 `= 0` 表示。其他一些语言，例如 Java，称这样的方法为*抽象*方法。

