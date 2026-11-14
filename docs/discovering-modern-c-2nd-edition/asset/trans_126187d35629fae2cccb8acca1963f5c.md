

签名）在调用函数时必须可见，但不一定是定义（即实现）。这不仅节省了大量编译时间，还允许我们向用户隐藏我们巧妙（或肮脏）的实现。

从 Tom 发出的唯一调用 `person::all_info()` 的实体是 `p`。这是一个 `person` 类型的对象，我们可以将一个 `student` 对象复制给它。但是，当从派生类复制到基类时，我们会丢失派生类的所有额外数据，只有基类的数据成员会被真正复制。同样，虚函数调用执行基类的相应函数（这里是 `person::all_info()`）。也就是说，当基类对象通过从派生类复制构造时，它的行为不会不同：所有额外成员都消失了，vtable 不再引用派生类的任何方法。同样，按值将参数传递给函数：

```
void glueless(person p)
{
    p.all_info();
}
```

这会禁用晚期绑定，从而阻碍从派生类调用 `virtual` 函数。这是面向对象编程中非常常见（不仅限于）的初学者错误，称为 *切片*。因此，我们必须遵守以下规则：

## 传递多态类型

多态类型必须始终通过引用或（智能）指针传递！

## 6.1.3.1 销毁多态类

多态类型的对象不仅可以通过基类引用，还可以用基类指针存储：

点击此处查看代码图像

```
person* max= new student("Max Smith", "Numerics");
```

当我们删除这个指针时，我们调用的是 `person` 的析构函数而不是 `student` 的，因此只有 `person` 的成员会被销毁。为了正确销毁，我们需要一个 `virtual` 析构函数：

```
class person
{
    virtual ~person() {}
};
```

当所有基类和成员都有适当的析构函数时，只需让编译器以默认方式生成虚拟析构函数即可：

```
virtual ~person() = default;
```

无论哪种方式：

## 多态类型的析构函数

*每个多态类型都需要一个虚拟析构函数。*

希望，未来的 C++ 标准将在用户省略析构函数时，将所有多态类的析构函数声明为虚拟。

## C++11 6.1.3.2 显式重写

即使是高级程序员也时常掉入的另一个流行陷阱是，重写方法的签名略有不同，例如：

点击此处查看代码图像

```
class person
{
    virtual void all_info() const { ... }
};
class student
    : public person
{
    virtual void all_info() { ... }
};

int main ()
{
    student tom("Tom Tomson", "Algebra, Analysis");
    person& pr = tom;
    pr.all_info();
}
```

在这个示例中，pr.all_info() 没有晚期绑定到 student::all_info()，因为签名不同。诚然，这种差异并不明显，这引出了一个问题：方法的 const 限定与签名究竟有什么关系。我们可以将成员函数视为具有一个指向对象本身的隐式隐藏参数：

点击此处查看代码图像

```
void person::all_info_impl(const person &me = *this) { ... }
```

现在很明显，方法的 const 限定符限定了 person::all_info() 中的这个隐藏引用。student::all_info() 中对应的隐藏引用不是 const 限定的，由于签名不同，该方法不被视为重写。编译器不会警告我们，只是将 student::all_info() 视为新的重载。相信我们，当类很大且存储在不同文件中时，这个小小的讨厌错误会让你忙活一阵子。

C++11 我们可以轻松使用 C++11 属性 override 来保护自己免受此类麻烦：

点击此处查看代码图像

```
class student
 : public person
{
    virtual void all_info() override { ... }
};
```

在这里，程序员声明此函数重写了基类的虚函数（具有完全相同的签名）。如果没有这样的虚函数，编译器会报错。1

- 1. 消息已重新格式化以适应页面。

点击此处查看代码图像

```
.... error: 'all_info' marked 'override' but doesn't override
           any member functions
           virtual void all_info() override {
           ^~~~~~~~~~
.... warning: 'student::all_info' hides overloaded virtual
           fct.
.... note: hidden overloaded virtual function 'person::all_info'
           declared here: different qualifiers (const vs
           none)
```

```
virtual void all_info() const { ... }
```

在这里，我们也从 clang++ 得到提示，限定符不同。对非虚函数使用 override 会导致不同的错误消息：

点击此处查看代码图像

```
...: error: only virtual member fct. can be marked 'override'
void all_info() override {
```

override 并未为我们的软件增加激动人心的新功能，但它可以避免我们费力地查找笔误（键盘误操作）。除非需要向后兼容，否则建议到处使用 override。这个词输入很快（尤其是有自动补全时），能让我们的程序更可靠。它还能向其他程序员，甚至是多年未查看代码后的我们自己，传达我们的意图。

C++11 中的另一个新属性是 final。它声明虚拟成员函数不能被重写。这允许编译器用直接函数调用替换间接 vtable 调用，或者在 final 函数被直接调用（而非通过基类调用）时甚至内联函数代码。甚至整个类都可以声明为 final，以防止他人从中派生。

相较之下，override 是关于超类的声明，而 final 指的是子类。两者都是上下文关键字；即，它们仅在特定上下文中保留：作为成员函数的限定符。在其他地方，这些词可以自由使用，例如作为变量名。但是，出于清晰度考虑，建议不要这样做。

核心准则 [63] 建议，虚函数应仅拥有以下声明符中的恰好一个——virtual、override 或 final——因为其他声明符会相应隐含。

## 6.1.3.3 函数调用机制

当调用多态类中的函数时，三种机制会相互作用：

- 重载；
- 重写；以及
- 名称隐藏。

我们已经展示了这些技术，并分别讨论了它们的工作原理。现在将它们组合起来考虑。假设我们有派生类：

```
class c1 { ... };
class c2 : public c1 { ... };
class c3 : public c2 { ... };
class c4 : public c3 { ... };
class c5 : public c4 { ... };
```

并且对于 c3 的引用，我们调用：

```
void call(c3& r)
{
    r.f(2.6);
}
```

现在，编译器将从 c3 中可见的 f 的重载中，为 double 选择最佳匹配。如果 f 在 c3 中声明，则每个重载都可见。c1 和 c2 中的 f 的所有重载都被隐藏，除非在 c3 中有 using c1::f; 或 using c2::f 的声明。如果 f 未在 c3 中声明，则 c2 的重载可见（除非在 c2 内部声明了 using c1::f）。同样，如果 c2 和 c3 都未声明名称 f，则 c1 的重载可见。如果这三个类都未声明 f，则方法调用显然是错误的。

给定方法 f 的一组可见重载，编译时会为参数类型 double 选择最具体的签名。如果所选重载是虚函数，则运行时会选择对象类型的最派生重写。例如，如果 r 引用类型为 c5 的对象，且 f(double) 在 c4 和 c5 中都被重写，则调用 c5 的重写。如果我们有 c5 的重写但没有 c4 的重写，且 r 引用类型为 c4 的对象，则我们调用来自 c3（或其基类继承的）的方法，因为 c5 的重写不合法。

在实践中，情况通常不那么复杂，但我们应该意识到编译时和运行时的混合选择。一个...的隐藏

