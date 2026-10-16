

(§22.5) 通过将指向类型信息的指针放在对象的类 (§3.2.3) 的虚函数表中，将其关联到一个对象。例如：

```
**My_slider:**

...

vptr vtbl: **type_info**:...
“**My_slider**” bases
**type_info:**
“**Ival_slider**”
**My_slider::get_value()**
```

虚线箭头表示一个偏移量，它允许仅根据指向多态子对象的指针找到完整对象的开始。很明显，**dynamic_cast** 可以高效地实现。所涉及的只是对代表基类的 **type_info** 对象的几次比较；不需要昂贵的查找或字符串比较。

将 **dynamic_cast** 限制为多态类型从逻辑上讲也是有意义的。也就是说，如果一个对象没有虚函数，就不能在不知道其确切类型的情况下安全地操作它。因此，应注意不要将此类对象放入其类型未知的情况下。如果其类型已知，我们就不需要使用 **dynamic_cast**。

**dynamic_cast** 的目标类型不必是多态的。这使我们能够将具体类型包装在多态类型中，例如，通过对象 I/O 系统 (§22.2.4) 传输，然后稍后“解包”具体类型。例如：

```
class Io_obj { // base class for object I/O system
virtual Io_obj* clone() = 0;
};
```

## Section 22.2.1 dynamic_cast

```
class Io_date : public Date, public Io_obj { };

void f(Io_obj* pio) {
Date* pd = dynamic_cast<Date*>(pio);
// ...
}
```

**dynamic_cast** 到 **void*** 可用于确定多态类型对象的开始地址。例如：

```
void g(Ival_box* pb, Date* pd)
{
void* pb2 = dynamic_cast<void*>(pb); // OK
void* pd2 = dynamic_cast<void*>(pd); // error: Date not polymorphic
}
```

在派生类对象中，表示基类的对象，例如 **Ival_box**，不一定是该最派生类对象中的第一个子对象。因此，**pb** 不一定与 **pb2** 持有相同的地址。

此类转换仅对与非常低级函数的交互有用（只有此类函数处理 void* s）。不能从 void* 进行 dynamic_cast（因为没有办法知道在哪里找到 vptr；§22.2.3）。

## 22.2.1.1 dynamic_cast to Reference

要获得多态行为，必须通过指针或引用操作对象。当 dynamic_cast 用于指针类型时，nullptr 表示失败。这对于引用来说既不可行也不希望。

给定一个指针结果，我们必须考虑结果为 nullptr 的可能性，即指针不指向对象。因此，指针的 dynamic_cast 结果应始终显式测试。对于指针 p，dynamic_cast<T*>(p) 可以看作是问题“p 所指向的对象，如果有，是类型 T 吗？”例如：

```
void fp(Ival_box* p)
{
if (Ival_slider* is = dynamic_cast<Ival_slider*>(p)) { // does p point to an Ival_slider?
// ... use is ...
}
else {
// ... *p not a slider;handle alternatives ...
}
}
```

另一方面，我们可以合法地假设引用引用一个对象 (§7.7.4)。因此，引用 r 的 dynamic_cast<T&>(r) 不是一个问题而是一个断言：“r 所引用的对象是类型 T。” dynamic_cast 对于引用的结果由 dynamic_cast 本身的实现隐式测试。如果 dynamic_cast 到引用的操作数不是预期类型，则会抛出 bad_cast 异常。例如：

```
void fr(Ival_box& r) {
Ival_slider& is = dynamic_cast<Ival_slider&>(r); // r references an Ival_slider! // ...
use is ...
}
```

失败的动态指针转换和失败的动态引用转换的结果差异反映了引用和指针之间的根本差异。如果用户想防止对引用的错误转换，必须提供合适的处理程序。例如：

```
void g(BB_ival_slider& slider, BB_ival_dial& dial)
{
try { fp(&slider); // pointer to BB_ival_slider passed as Ival_box*
fr(slider); // reference to BB_ival_slider passed as Ival_box&
fp(&dial); // pointer to BB_ival_dial passed as Ival_box*
fr(dial); // dial passed as Ival_box
}
catch (bad_cast) { // §30.4.1.1
// ...
}
}
```

对 fp() 的调用和第一次对 fr() 的调用将正常返回（假设 fp() 真的可以处理 BB_ival_dial），但第二次调用 fr() 将导致 bad_cast 异常，该异常将被 g() 捕获。

显式对 nullptr 的测试很容易被意外遗漏。如果这让你担心，你可以编写一个转换函数，在失败时抛出异常而不是返回 nullptr。

## 22.2.2 Multiple Inheritance

当仅使用单继承时，一个类及其基类构成以单个基类为根的树。这很简单但通常限制很大。当使用多重继承时，就没有单一根。就其本身而言，这并不会使事情复杂化太多。然而，如果一个类在层次结构中出现多次，我们在引用表示该类的对象或对象时必须小心一些。

自然地，我们尝试在应用程序允许的范围内保持层次结构尽可能简单（并且不过于简单）。然而，一旦构建了非平凡的层次结构，我们有时需要导航它以找到要使用的特定类。这种需求有两种变体：

- 有时，我们希望明确命名一个基类以用作接口，例如，解决歧义或调用特定函数而不依赖于虚函数机制（显式限定调用；§21.3.3）。
- 有时，我们希望给定指向另一个的指针，获得指向层次结构子对象的指针，例如，从指向基的指针获取指向完整派生类对象的指针（向下转换；§22.2.1）或从指向另一个基的指针获取指向基类对象的指针（交叉转换；§22.2.4）。

在这里，我们考虑如何使用类型转换（casts）导航类层次结构以获得所需类型的指针。为了说明可用的机制和指导它们的规则，考虑一个包含重复基和虚基的格：

Section 22.2.2 Multiple Inheritance

```
class Component
: public virtual Storable { /*...*/ };
class Receiver
: public Component { /*...*/ };
class Transmitter
: public Component { /*...*/ };
class Radio
: public Receiver, public Transmitter { /*...*/ };
```

或图形表示：

Storable
Component Component
Receiver Transmitter

Radio

这里，Radio 对象有两个 Component 子对象。因此，在 Radio 内部从 Storable 到 Component 的 dynamic_cast 将是模棱两可的并返回 0。根本没有办法知道程序员想要哪个 Component：

```
void h1(Radio& r)
{
Storable* ps = &r; // a Radio has a unique Storable
//...
Component* pc = dynamic_cast<Component*>(ps); // pc = 0; a Radio has two Components //...
}
```

通常——并且典型地——程序员（以及查看单个翻译单元的编译器）并不知道完整的类格。相反，代码是用对某个子格的知识编写的。例如，程序员可能只知道 Radio 的 Transmitter 部分并编写：

```
void h2(Storable*ps) // ps might or might not point to a Component
{
if (Component* pc = dynamic_cast<Component*>(ps)) {
// we have a component!
}
else {
// it wasn’t a Component
}
}
```

指向 Radio 对象的指针的歧义通常在编译时无法检测到。这种运行时歧义检测仅对虚基是必需的。对于普通基，下转换时（即朝向派生类；§22.2）总是有唯一的给定转换的子对象（或没有）。对于虚基，等价的歧义发生在上转换时（即朝向基），但此类歧义在编译时被捕获。

## 22.2.3 static_cast and dynamic_cast

dynamic_cast 可以从多态虚基类转换到派生类或同胞类 (§22.2.1)。static_cast (§11.5.2) 不检查它转换的对象，因此它不能：

```
void g(Radio& r)
{
Receiver* prec = &r; // Receiver is an ordinary base of Radio Radio* pr =
static_cast<Radio*>(prec); // OK, unchecked
pr = dynamic_cast<Radio*>(prec); // OK, run-time checked
Storable * ps = &r; // Storable is a virtual base of Radio
```

