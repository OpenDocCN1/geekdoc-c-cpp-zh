

指向数据成员的指针在 §20.6.2 中描述。

## 20.6.2 指向数据成员的指针

自然地，指向成员的指针概念适用于数据成员以及带参数和返回类型的成员函数。例如：

```
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

指向函数的指针类型像其他任何类型一样进行检查。

## 20.6.3 基类和派生类成员

派生类至少具有从其基类继承的成员。通常它还有更多。这意味着我们可以安全地将指向基类成员的指针赋给指向派生类成员的指针，但反之则不行。这种属性通常称为逆变。例如：

```
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

这种逆变规则似乎与“我们可以将指向派生类的指针赋给指向其基类的指针”这一规则相反。事实上，这两种规则都存在是为了保持一个基本保证：指针永远不会指向一个对象，该对象至少不具备指针所承诺的属性。在这种情况下，Std_interface::* 可以应用于任何 Std_interface，而其中大多数对象很可能不是 Text 类型。因此，它们不具有我们试图用来初始化 pmi 的成员 Text::print。通过拒绝初始化，编译器使我们免于运行时错误。

## 第 20.7 节 建议 611

## 20.7 建议

[1] 避免类型字段；§20.3.1。
[2] 通过指针和引用访问多态对象；§20.3.2。 [3] 使用抽象类以将设计集中于提供干净的接口；§20.4。 [4] 在大型类层次结构中使用 override 使重写显式化；§20.3.4.1。 [5] 仅谨慎地使用 final；§20.3.4.2。

[6] 使用抽象类来指定接口；§20.4。
[7] 使用抽象类以将实现细节排除在接口之外；§20.4。 [8] 具有虚函数的类应具有虚析构函数；§20.4。 [9] 抽象类通常不需要构造函数；§20.4。

[10] 优先使用私有成员作为实现细节；§20.5。
[11] 优先使用公共成员作为接口；§20.5。
[12] 仅在确实需要时才谨慎使用受保护成员；§20.5.1.1。 [13] 不要声明受保护的数据成员；§20.5.1.1。

本页故意留空

## 类层次结构

> *抽象是选择性无知。*  
> — Andrew Koenig

+   - 简介
+   - 类层次结构的<|message|>
+     - 实现继承；接口继承；替代实现；本地化对象创建
+   - 多重继承
+     - 多个接口；多个实现类；歧义解析；基类的重复使用；虚基类；复制 vs. 虚基
+   - 建议

## 21.1 简介

本章的主要关注点是设计技术，而非语言特性。示例取自用户界面设计，但我避免了通常用于图形用户界面（GUI）系统的事件驱动编程主题。关于屏幕上的操作如何转化为成员函数调用的详细讨论将对类层次结构设计的问题贡献甚少，却有巨大的分心潜力：它本身就是一个有趣且重要的主题。欲了解 GUI，请查阅众多 C++ GUI 库之一。

## 21.2 类层次结构的 fiy

考虑一个简单的设计问题：为程序（“应用程序”）提供一种从用户获取整数值的方法。这可以通过令人眼花缭乱的多种方式完成。为了使我们的程序免受这种多样性的影响，并且也有机会探索可能的 fiy 选择，让我们首先定义程序对这种简单输入操作的模型。

想法是有一个类 `Ival_box`（“整数值输入框”），它知道将接受的输入值范围。程序可以向 `Ival_box` 请求其值，并在必要时要求其提示用户。此外，程序可以询问 `Ival_box` 用户自上次查看以来是否更改了值：

```
user
(via “system”)
Ival_box:
value application set_value() get_value()
```

由于实现这种基本思想的方式有很多，我们必须假设会有许多不同种类的 `Ival_box`，例如滑块、用户可以在其中输入数字的普通框、拨盘和语音交互。

总体方法是为应用程序构建一个“虚拟用户界面系统”。该系统提供现有用户界面系统提供的部分服务。它可以在各种系统上实现，以确保应用程序代码的可移植性。当然，还有其他方法可以使应用程序与用户界面系统隔离开来。我选择这种方法是因为它通用，因为它允许我展示各种技术和 fiy 权衡，因为这些技术也是构建“真实”用户界面系统时使用的技术，而且——最重要的是——这些技术适用于远超接口系统狭窄领域的各种问题。

除了忽略如何将用户操作（事件）映射到库调用的主题外，我还忽略了多线程 GUI 系统中锁定的需求。

### 21.2.1 实现继承

我们的第一个解决方案是使用实现继承的类层次结构（如旧程序中常见）。

类 `Ival_box` 定义了所有 `Ival_box` 的基本接口，并指定了更具体的 `Ival_box` 类型可以覆盖的默认实现。此外，我们声明实现基本概念所需的数据：

```
class Ival_box {
protected:
int val;
int low, high;
bool changed {false}; // changed by user using set_value()
public:
Ival_box(int ll, int hh):val{ll}, low{ll}, high{hh}{ }

virtual int get_value() { changed = false; return val; } virtual void set_value(int i) {
changed = true; val = i; } virtual void reset_value(int i) { changed = false; val = i; }
virtual void prompt() { }
virtual bool was_changed() const { return changed; }

virtual ~Ival_box() { }; };
// for application // for user
// for application

第 21.2.1 节 实现继承 615
函数的默认实现相当粗糙，这里主要用于说明预期语义。现实的类例如会提供一些范围检查。程序员可能会像这样使用这些“ival 类”：

```
void interact(Ival_box * pb)
{
pb->prompt(); // alert user
// ...
int i = pb->get_value();

if (pb->was_changed()) {
// ... newvalue; do something ... }
else {
// ... do something else ... }
}

void some_fct() {
unique_ptr<Ival_box> p1 {new Ival_slider{0,5}}; // Ival_slider derived from Ival_box
interact(p1.get());

unique_ptr<Ival_box> p2 {new Ival_dial{1,12}};
interact(p2.get());
}
```

大多数应用程序代码都是以（指向）普通 Ival_box 的形式编写的，就像 interact() 那样。这样，应用程序就不必知道 Ival_box 概念的潜在大量变体。对此类专用类的了解被隔离在创建此类对象的相对较少的函数中。这使用户免受派生类实现更改的影响。大多数代码可以对存在不同种类的 Ival_box 的事实视而不见。

我使用 unique_ptr（§5.2.1，§34.3.1）以避免忘记删除 ival_box。
为简化讨论，我不涉及程序如何等待输入的问题。
也许程序确实在 get_value() 中等待用户（例如，使用 future 上的 get()；§5.3.5.1），也许程序将 Ival_box 与事件关联并准备响应回调，或者也许程序为 Ival_box 启动一个线程并稍后查询该线程的状态。此类决策在用户界面系统的 fiy 中至关重要。然而，在这里以任何现实的细节讨论它们只会分散对编程技术和语言设施的介绍。 这里描述的 fiy 技术和支持它们的语言设施并非特定于用户界面。它们适用于更广泛的问题范围。

不同种类的 Ival_box 被定义为派生自 Ival_box 的类。例如：

```
class Ival_slider : public Ival_box {
private:
// ... graphics stuff to define what the slider looks like,etc. ...
public:
Ival_slider(int, int);
int get_value() override; // get value from user and deposit it in val
void prompt() override;
};
```

Ival_box 的数据成员被声明为 protected 以允许从派生类访问。因此，Ival_slider::get_value() 可以将值存入 Ival_box::val。受保护成员可由类自己的成员和派生类的成员访问，但对普通用户不可访问（参见 §20.5）。

除了 Ival_slider 之外，我们还会定义 Ival_box 概念的其他变体。这些可以包括 Ival_dial，它允许您通过转动旋钮来选择值；

