
```cpp
class Buffer {
protected:
char a[128];
// ...
};

class Linked_buffer : public Buffer { // ...
};

class Circular_buffer : public Buffer { // ...
void f(Linked_buffer* p)
{
a[0] = 0; // OK: access to Circular_buffer’s own protected member
p->a[0] = 0; // error : access to protected member of different type
}
};
```

这可以防止一个派生类破坏属于其他派生类的数据时发生的细微错误。

#### 20.5.1.1 `protected` 成员的使用

数据隐藏的简单`private`/`public`模型很好地服务于具体类型（§16.3）的概念。然而，当使用派生类时，类的使用者有两种类型：派生类和“普通公众”。实现类上的操作的成员和友元代表这些使用者对类对象进行操作。`private`/`public`模型允许程序员清楚地区分实现者和普通公众，但它没有提供专门针对派生类的方法。

声明为`protected`的成员比声明为`private`的成员更容易被滥用。特别是，声明数据成员为`protected`通常是设计错误。将大量数据放在所有派生类共用的公共类中会使该数据容易被破坏。更糟的是，`protected`数据像`public`数据一样难以重构，因为没有很好的方法找到每个使用。因此，`protected`数据成为软件维护问题。

幸运的是，你不必使用`protected`数据；`private`是类中的默认值，并且是通常更好的选择。以我的经验，总会有替代方案，不必将大量信息放在公共基类中供派生类直接使用。

#### 20.5.1.1 使用 `protected` 成员

然而，对于受保护的成员函数而言，这些反对意见都不重要；`protected`是指定供派生类使用的操作的绝佳方式。§21.2.2 中的`Ival_slider`就是一个例子。如果该示例中的实现类是私有的，那么进一步的派生将不可行。另一方面，将提供实现细节的基类设为公共会招致错误和误用。

### 20.5.2 基类的访问控制

与成员一样，基类可以声明为`private`、`protected`或`public`。例如：

```cpp
class X : public B { /*...*/ };

class Y : protected B { /*...*/ };

class Z : private B { /*...*/ };
```

不同的访问说明符服务于不同的设计需求：

- `public`派生使派生类成为其基类的子类型。例如，`X`是一种`B`。这是最常见的派生形式。

- `private`基类在通过限制对基类的接口以提供更强保证时最为有用。例如，`B`是`Z`的实现细节。§25.3 中那个为其`Vector<void*>`基类添加类型检查的指针`Vector`模板就是一个很好的例子。

- `protected`基类在以进一步派生为常态的类层次结构中很有用。与`private`派生一样，`protected`派生用于表示实现细节。§21.2.2 中的`Ival_slider`就是一个很好的例子。

基类的访问说明符可以省略。在这种情况下，对于`class`，基类默认为`private`；对于`struct`，基类默认为`public`。例如：

```cpp
class XX : B { /*...*/ }; // B 是 private 基类

struct YY : B { /*...*/ }; // B 是 public 基类
```

人们期望基类是`public`（即表示子类型关系），因此省略基类的访问说明符对`class`来说可能会令人惊讶，但对`struct`来说则不然。

基类的访问说明符控制对基类成员的访问，以及从派生类类型到基类类型的指针和引用的转换。考虑从基类`B`派生的类`D`：

- 如果`B`是`private`基类，则其`public`和`protected`成员只能由`D`的成员函数和友元使用。只有`D`的友元和成员才能将`D*`转换为`B*`。

- 如果`B`是`protected`基类，则其`public`和`protected`成员只能由`D`的成员函数和友元以及从`D`派生的类的成员函数和友元使用。只有`D`的友元和成员以及从`D`派生的类的友元和成员才能将`D*`转换为`B*`。

- 如果`B`是`public`基类，则其`public`成员可以被任何函数使用。此外，其`protected`成员可以被`D`的成员和友元以及从`D`派生的类的成员和友元使用。任何函数都可以将`D*`转换为`B*`。

这基本上重申了成员访问规则（§20.5）。在设计类时，我们选择基类访问的方式与选择成员访问的方式相同。有关示例，请参见 §21.2.2 中的`Ival_slider`。

#### 20.5.2.1 多重继承与访问控制

如果在多重继承格（§21.3）中可以通过多条路径到达基类的名称，那么只要通过任何一条路径可以访问，它就是可访问的。例如：

```cpp
struct B {

    int m;

    static int sm;

    // ...

};

class D1 : public virtual B { /* ... */ };

class D2 : public virtual B { /* ... */ };

class D12 : public D1, private D2 { /* ... */ };

D12* pd = new D12;

B* pb = pd; // OK：通过 D1 可访问

int i1 = pd->m; // OK：通过 D1 可访问
```

如果单个实体可以通过多条路径到达，我们仍然可以在没有歧义的情况下引用它。例如：

```cpp
class X1 : public B { /* ... */ };

class X2 : public B { /* ... */ };

class XX : public X1, public X2 { /* ... */ };

XX* pxx = new XX;

int i1 = pxx->m; // 错误，有歧义：是 XX::X1::B::m 还是 XX::X2::B::m？

int i2 = pxx->sm; // OK：XX 中只有一个 B::sm（sm 是静态成员）
```

### 20.5.3 `using`-声明与访问控制

`using`-声明（§14.2.2、§20.3.5）不能用来获取额外的信息访问权。它仅仅是一种使已可访问的信息更方便使用的机制。另一方面，一旦访问权可用，就可以将其授予其他用户。例如：

```cpp
class B {

private:

    int a;
```

```cpp
class Std_interface {

public:

    virtual void start() = 0;

    virtual void suspend() = 0;

    virtual void resume() = 0;

    virtual void quit() = 0;

    virtual void full_size() = 0;

    virtual void small() = 0;

    virtual ~Std_interface() {}

};
```

每个操作的确切含义由调用它的对象来定义。通常，在发出请求的人或程序与接收请求的对象之间有一层软件。理想情况下，这类中间软件层不应需要了解各个操作（如`resume()`和`full_size()`）的任何细节。如果它们需要了解，那么每次操作发生变化时，中间层都必须更新。因此，这类中间层仅仅传输表示要调用操作的数据，从请求的发出方传送到接收方。

实现这一点的一种简单方法是发送一个表示要调用的操作的**字符串**。例如，要调用`suspend()`，我们可以发送字符串“suspend”。然而，必须有人创建该字符串，也必须有人解码它以确定它对应于哪个操作——如果有对应操作的话。这通常显得间接而繁琐。相反，我们可以简单地发送一个表示操作的整数。例如，可以用 2 来表示`suspend()`。但是，虽然整数对机器来说处理起来很方便，但对人来说可能会变得相当晦涩。我们仍然需要编写代码来确定 2 表示`suspend()`并调用`suspend()`。

不过，我们可以使用成员指针来间接引用类的成员。考虑`Std_interface`。如果我想在不直接提及`suspend()`的情况下为某个对象调用`suspend()`，我需要一个指向`Std_interface::suspend()`的成员指针。我还需要一个指向或引用我要挂起的对象的指针或引用。考虑一个简单的例子：

```cpp
using Pstd_mem = void (Std_interface::*)(); // 指向成员的指针类型

void f(Std_interface* p)

{

    Pstd_mem s = &Std_interface::suspend; // 指向 suspend() 的指针

    p->suspend(); // 直接调用

    p->*s(); // 通过成员指针调用

}
```

可以通过将地址运算符`&`应用于完全限定的类成员名来获得成员指针，例如`&Std_interface::suspend`。类型为“指向类 X 成员的指针”的变量使用形式为`X::*`的声明符来声明。

使用别名来弥补 C 声明符语法可读性不足的做法很典型。但请注意`X::*`声明符与传统的`*`声明符的精确匹配方式。

成员指针`m`可以与对象结合使用。运算符`->*`和`.*`允许程序员表达这种结合。例如，`p->*m`将`m`绑定到`p`所指向的对象，而`obj.*m`将`m`绑定到对象`obj`。结果可以根据`m`的类型来使用。无法存储`->*`或`.*`操作的结果以供以后使用。

自然，如果我们知道要调用哪个成员，我们会直接调用它，而不是使用成员指针。与普通函数指针一样，当我们需要在不知道函数名称的情况下引用某个函数时，会使用指向成员函数的指针。然而，成员指针并不像指向变量的指针或指向函数的指针那样是指向某块内存的指针。它更像是对结构体的偏移量或对数组的索引，但当然，实现会考虑数据成员、虚函数、非虚函数等之间的差异。当成员指针与指向正确类型对象的指针结合时，会产生一个标识特定对象的特定成员的东西。

`p->*s()`调用可以这样图形化表示：

```
vtable:

p: X::start

s: X::suspend
```

### 20.6.1 指向函数成员的指针

因为指向虚成员的指针（本例中的`s`）是一种偏移量，它不依赖于对象在内存中的位置。因此，只要两边使用相同的对象布局，指向虚成员的指针就可以在不同的地址空间之间传递。与指向普通函数的指针一样，指向非虚成员函数的指针不能在地址空间之间交换。

注意，通过成员指针调用的函数可以是**虚**函数。例如，当我们通过成员指针调用`suspend()`时，对于应用该成员指针的对象，我们会得到正确的`suspend()`。这是成员指针的一个基本特性。

在编写解释器时，我们可能会使用成员指针来调用以字符串形式呈现的函数：

```cpp
map<string, Std_interface*> variable;

map<string, Pstd_mem> operation;

void call_member(string var, string oper)

{

    (variable[var]->*operation[oper])(); // var.oper()

}
```

一个**静态**成员不与特定对象关联，因此指向**静态**成员的指针只是一个普通指针。例如：

```cpp
class Task {

    // ...

    static void schedule();

};

void (*p)() = &Task::schedule;         // OK

void (Task::* pm)() = &Task::schedule; // 错误：普通指针赋值给成员指针
```

指向数据成员的指针在 §20.6.2 中描述。

### 20.6.2 指向数据成员的指针

自然地，指向成员的指针概念适用于数据成员以及带参数和返回类型的成员函数。例如：

```cpp
struct C {

const char* val;

int i;

void print(int x) { cout << val << x << '\n'; } int f1(int);

void f2();

C(const char* v) { val = v; }

};

using Pmfi = void (C::*)(int); // pointer to member function of C taking an int

using Pm = const char* C::*; // pointer to char* data member of C

void f(C& z1, C& z2) {

C* p = &z2;

Pmfi pf = &C::print; Pm pm = &C::val;

z1.print(1);

(z1.*pf)(2);

z1.*pm = "nv1 "; p->*pm = "nv2 "; z2.print(3);

(p->*pf)(4);

pf = &C::f1; // error : return type mismatch

pf = &C::f2; // error :argument type mismatch

pm = &C::i; // error : type mismatch

pm = pf; // error : type mismatch

}
```

指向函数的指针类型像其他任何类型一样检查。

### 20.6.3 基类和派生类成员

派生类至少具有从其基类继承的成员。通常它还有更多。这意味着我们可以安全地将指向基类成员的指针赋给指向派生类成员的指针，但反之则不行。这种属性通常称为逆变。例如：

```cpp
class Text : public Std_interface {

public:

void start();

void suspend();

// ...

virtual void print();

private:

vector s;

};

void (Std_interface::* pmi)() = &Text::print; // error

void (Text::*pmt)() = &Std_interface::start; // OK
```

这种逆变规则似乎与“我们可以将指向派生类的指针赋给指向其基类的指针”这一规则相反。事实上，这两种规则都存在是为了保持一个基本保证：指针永远不会指向一个对象，该对象至少不具备指针所承诺的属性。在这种情况下，`Std_interface::*`可以应用于任何`Std_interface`，而其中大多数对象很可能不是`Text`类型。因此，它们不具有我们试图用来初始化`pmi`的成员`Text::print`。通过拒绝初始化，编译器使我们免于运行时错误。

### 20.7 建议

[1] 避免类型字段；§20.3.1。  
[2] 通过指针和引用访问多态对象；§20.3.2。  
[3] 使用抽象类以将设计集中于提供干净的接口；§20.4。  
[4] 在大型类层次结构中使用`override`使重写显式化；§20.3.4.1。  
[5] 仅谨慎地使用`final`；§20.3.4.2。  
[6] 使用抽象类来指定接口；§20.4。  
[7] 使用抽象类以将实现细节排除在接口之外；§20.4。  
[8] 具有虚函数的类应具有虚析构函数；§20.4。  
[9] 抽象类通常不需要构造函数；§20.4。  
[10] 优先使用私有成员作为实现细节；§20.5。  
[11] 优先使用公共成员作为接口；§20.5。  
[12] 仅在确实需要时才谨慎使用受保护成员；§20.5.1.1。  
[13] 不要声明受保护的数据成员；§20.5.1.1。

# 类层次结构

> *抽象是选择性无知。*  
> — Andrew Koenig

- 简介
- 类层次结构的</message?>
  - 实现继承；接口继承；替代实现；本地化对象创建
- 多重继承
  - 多个接口；多个实现类；歧义解析；基类的重复使用；虚基类；复制 vs. 虚基
- 建议

## 21.1 简介

本章的主要关注点是设计技术，而非语言特性。示例取自用户界面设计，但我避免了通常用于图形用户界面（GUI）系统的事件驱动编程主题。关于屏幕上的操作如何转化为成员函数调用的详细讨论将对类层次结构设计的问题贡献甚少，却有巨大的分心潜力：它本身就是一个有趣且重要的主题。欲了解 GUI，请查阅众多 C++ GUI 库之一。

## 21.2 类层次结构的 fiy

考虑一个简单的设计问题：为程序（“应用程序”）提供一种从用户获取整数值的方法。这可以通过令人眼花缭乱的多种方式完成。为了使我们的程序免受这种多样性的影响，并且也有机会探索可能的 fiy 选择，让我们首先定义程序对这种简单输入操作的模型。

想法是有一个类`Ival_box`（“整数值输入框”），它知道将接受的输入值范围。程序可以向`Ival_box`请求其值，并在必要时要求其提示用户。此外，程序可以询问`Ival_box`用户自上次查看以来是否更改了值：

```
user

(via “system”)

Ival_box:
```
