

```cpp
void test14() {
    cout << "14. Testing S14: Overloaded subscript operator."
         << endl << endl;
    cout << "14. Testing S14: Overloaded subscript operator."
        << endl << endl;
    String s14("C++ is fun.");
    for (int i = -1; i <= s14.getLength(); i++) {
        char& ch = s14[i];
        if (ch == '\0')
            ch = ch;
    }
    s14.print();
    wait();
}

void test15() {
    cout << "15. Testing S15: Pointer notation."
         << endl << endl;
    cout << "15. Testing S15: Pointer notation."
        << endl << endl;
    String s15("ABCDE");
    for(int i = 0; i < s15.getLength(); i++)
        ++(*(s15+i));
    for (int j = 0; j < s15.getLength(); j++) {
        cout << *(j + s15);
        cout << *(j + s15);
    }
    cout << endl;
    cout << endl;
    wait();
}
```

```cpp
void test16() {
    cout << "16. Testing S16, T16, U16, V16, W16, X16, Y16, Z16: "
         << "Increment and decrement operators."
         << endl << endl;
    cout << "16. Testing S16, T16, U16, V16, W16, X16, Y16, Z16: "
         << "Increment and decrement operators."
         << endl << endl;
    String s16("ABC");
    String t16(s16++);
    s16.print();
    t16.print();

    String u16("ABC");
    String v16(u16++);
    u16.print();
    v16.print();

    String w16("ABC");
    String x16(~w16);
    w16.print();
    x16.print();

    String y16("ABC");
    String z16(y16--);
    y16.print();
    z16.print();
    wait();
}

void test17() {
    cout << "17. Testing S17, T17: Substr function."
         << endl << endl;
    cout << "17. Testing S17, T17: Substr function."
         << endl << endl;
    String s17("All You Need Is Love"), t17;
    t17 = s17.substr(4, 8);
    s17.print();
    t17.print();
    wait();
}
```

```cpp
void test18() {
    cout << "18. Testing S18, T18: Output function."
         << endl << endl;
    cout << "18. Testing S18, T18: Output function."
         << endl << endl;
    String s18("Red");
    String t18("Green");
    String u18("Blue");
    cout << s18 << t18 << u18;
    cout << s18 << t18 << u18;
    cout << endl;
    cout << endl;
    wait();
}

void test19() {
    cout << "19. Testing S19, T19, U19: ReverseString class."
         << endl << endl;
    cout << "19. Testing S19, T19, U19: ReverseString class."
         << endl << endl;
    ReverseString s19("Computer");
    ReverseString t19;
    t19 = ~s19;
    s19.print();
    t19.print();
    ReverseString u19(~~s19);
    u19.print();
    wait();
}

void test20() {
    cout << "20. Testing S20, T20, U20: CaseString class."
         << endl << endl;
    cout << "20. Testing S20, T20, U20: CaseString class."
         << endl << endl;
    CaseString s20("BallLooN");
    CaseString t20;
    t20 = s20;
    s20.print();
    t20.print();
    CaseString u20(s20);
    u20.print();
    wait();
}

void wait() {
    char buf;
    cout << endl << "Press any key to continue." << endl;
    cout << endl << endl;
    cin.get(buf);
}
```

- 多态简介
- 静态绑定与动态绑定
- 虚函数
- 抽象类
- 虚析构函数
- 虚函数机制
- 如何在 C++ 中泄漏内存
- 多态作业
- 多态实验（图书馆馆藏）

## 多态简介

对于任何计算机语言若要自称面向对象编程语言，都必须包含三个基本组件：

- 数据抽象与封装

这是定义某种新数据类型或类的过程。这包括指定该类型的内部表示以及用于操作该类型的函数。C++ 通过类机制支持数据抽象和封装。

- 继承

继承涉及以某种层次结构方式从现有类型创建新类型。C++ 通过类派生支持继承。

- 多态与动态绑定

多态源自希腊语：poly（许多）和 morphos（形式）。它指具有多种形式、多种形状的特性。在面向对象编程的语境下，多态描述了 C++ 代码根据运行时情况表现出不同行为的能力。它指的是从共同类派生的不同对象能够以不同方式响应同一消息的能力。单个操作在不同对象中可以具有不同的行为。C++ 通过虚函数支持多态和动态绑定。

## 静态绑定与动态绑定

在大多数传统编程语言中，编译器根据源代码调用固定的函数标识符。然后链接器获取这些标识符并将其替换为物理地址。

这被称为早期绑定或静态绑定，因为在编译和链接过程中（运行前）函数标识符与物理地址关联。早期绑定的问题是程序员必须预测在所有情况下所有函数调用中将使用哪些对象。这不仅具有局限性，而且有时是不可能的。

早期绑定最好的一点是它很快。唯一产生的运行时开销是：

- * 传递参数
- * 执行函数调用
- * 以及清理栈

在 C++ 中，多态函数只有在实际对象被传递给多态函数时，才可能与众多可能函数中的某一个关联。换句话说，源代码本身并不总能告诉你一段代码将如何执行。函数调用仅在源代码中指示，而不指定要调用的确切函数。这称为晚期绑定或动态绑定。

晚期绑定的问题在于其运行时效率。代码本身必须在运行时推断要调用哪个函数，然后调用它。某些语言（如 Smalltalk）专门使用晚期绑定，这导致了一种功能强大但存在一定速度损失的语言。另一方面，ANSI C 专门使用早期绑定，这带来了高速度但缺乏灵活性。

C++ 通过应用我们之前见过的一条规则，使多态成为可能：

![](img/adb3588dc0dfe9f607c1d417be6bb240_386_0.png)

基类指针可以指向基类对象或任何派生类对象。然而，这是一条单行道。指向派生类对象的指针不能指向基类对象。

但是，请回想一下，这带来了一些困难。当我们使用类型为 `Base` 的指针时，唯一可以引用的成员函数（或数据）是属于 `Base` 类的，即使该指针指向一个 `Derived` 类对象！

这不是多态，因为被指向的对象从未接收到发送的消息！原因是编译器只知道指针本身的类型，而不知道指针在运行时最终将指向哪个对象。

面向对象编程语言的目标是向指针所指向的任何对象发送消息，而不是向指针本身的类型发送消息。

为什么这很重要？因为这样你可以在运行时控制指针的内容（或地址），而指针变量本身的类型一旦被硬编码就无法更改。这样一来，对象本身可以“弄清楚”如何处理该消息，从而实现多态的概念。

## 虚函数

### 访问成员函数

让我们看看当基类和派生类都具有同名函数，并且我们使用指针访问这些函数但没有虚函数时会发生什么。给定以下类：

```
class Base {
 protected:
 int value;
 public:
 Base( int x ) { value = x; }
 int getValue() { return value; }
 };
```

我们现在可以声明并使用一个基类对象：

```
int main() {
 Base b(10);
 cout << "value = " << b.getValue() << endl;
 return 0;
 }
```

上述代码生成以下输出：

value = 10

我们现在将从基类派生一个类，将基类值乘以指定的数量：

```
class Derived : public Base {
 protected:
 int mult;
 public:
 Derived( int x, int y ) : Base(x), mult(y) { }
 int getValue() { return value * mult; }
 };
```

