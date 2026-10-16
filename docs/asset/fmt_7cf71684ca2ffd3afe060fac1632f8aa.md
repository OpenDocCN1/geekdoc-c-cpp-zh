

`dynamic_cast` 要求一个多态操作数，因为非多态对象中没有存储任何可用于查找其作为基类所代表的那些对象的信息。特别是，具有由其他语言（如 Fortran 或 C）确定的布局约束的类型的对象，可以用作虚基类。对于这类对象，只有静态类型信息可用。然而，提供运行时类型识别所需的信息包括实现 `dynamic_cast` 所需的信息。

为什么有人会想用 `static_cast` 来导航类层次结构？使用 `dynamic_cast` 会有运行时开销（§22.2.1）。更重要的是，在 `dynamic_cast` 可用之前就已经编写了数百万行代码。这些代码依赖于其他方式来确保转换是有效的，因此 `dynamic_cast` 所做的检查被视为多余。然而，这类代码通常使用 C 风格转换（§11.5.3）编写；往往会留下难以发现的错误。在可能的情况下，应使用更安全的 `dynamic_cast`。

编译器不能对 `void*` 所指向的内存做任何假设。这意味着必须检查对象以确定其类型的 `dynamic_cast` 不能从 `void*` 进行转换。为此，需要 `static_cast`。例如：

```cpp
Radio* f1(void* p)
{
    Storable* ps = static_cast<Storable*>(p); // trust the programmer
    return dynamic_cast<Radio*>(ps);
}
```

`dynamic_cast` 和 `static_cast` 都遵守 `const` 和访问控制。例如：

```cpp
class Users : private set<Person> { /*...*/ };

void f2(Users* pu, const Receiver* pcr)
{
    static_cast<set<Person>*>(pu); // error: access violation
    dynamic_cast<set<Person>*>(pu); // error: access violation
    static_cast<Receiver*>(pcr); // error: can't cast away const
    dynamic_cast<Receiver*>(pcr); // error: can't cast away const
    Receiver* pr = const_cast<Receiver*>(pcr); // OK
    // ...
}
```

无法使用 `static_cast` 或 `reinterpret_cast` 转换到私有基类，而“去掉 `const`”（或 `volatile`）需要 `const_cast`（§11.5.2）。即便如此，也只有在对象最初没有被声明为 `const`（或 `volatile`）时，使用转换得到的结果才是安全的（§16.2.9）。

# 22.2.4 恢复接口

从设计角度看，`dynamic_cast`（§22.2.1）可以看作是一种询问对象是否提供给定接口的机制。

举个例子，考虑一个简单的对象 I/O 系统。用户希望从流中读取对象，确定它们是预期的类型，然后使用它们。例如：

```cpp
void user()
{
    // ... open file assumed to hold shapes, and attach ss as an istream for that file ...
    unique_ptr<Io_obj> p{get_obj(ss)}; // read object from stream
    if (auto sp = dynamic_cast<Shape*>(p.get())) {
        sp->draw(); // use the Shape
        // ...
    }
    else {
        // oops: non-shape in Shape file
    }
}
```

函数 `user()` 完全通过抽象类 `Shape` 处理形状，因此可以使用各种形状。使用 `dynamic_cast` 是必不可少的，因为对象 I/O 系统可以处理许多其他类型的对象，而且用户可能意外打开了一个包含用户从未听说过的类的完全有效对象的文件。

我使用 `unique_ptr<Io_obj>`（§5.2.1、§34.3.1）以便不会忘记删除由 `get_obj()` 分配的对象。

这个对象 I/O 系统假定读写的每个对象都是派生自 `Io_obj` 的类的对象。`Io_obj` 类必须是多态类型，以便 `get_obj()` 的用户能够使用 `dynamic_cast` 来恢复返回对象的“真实类型”。例如：

```cpp
class Io_obj {
public:
    virtual Io_obj* clone() const = 0; // polymorphic
    virtual ~Io_obj() {}
};
```

对象 I/O 系统中的关键函数是 `get_obj()`，它从 `istream` 读取数据，并基于这些数据创建类对象。假设输入流上表示对象的数据以一个标识对象类的字符串作为前缀。`get_obj()` 的工作是读取该字符串，并调用一个能够读取并创建正确类对象的函数。例如：

```cpp
using Pf = Io_obj*(istream&); // pointer to function returning an Io_obj*
map<string, Pf> io_map; // maps strings to creation functions
string get_word(istream& is); // read a word from is; throw Read_error if the read failed

Io_obj* get_obj(istream& is)
{
    string str = get_word(is); // read initial word
    if (auto f = io_map[str])   // look up str to get function
        return f(is);            // call function
    throw Unknown_class{};       // no match for str
}
```

名为 `io_map` 的映射表保存了名称字符串与能够构造具有该名称的类的对象的函数之间的配对。

我们可以按 `user()` 的需要从 `Io_obj` 派生 `Shape` 类：

```cpp
class Shape : public Io_obj {
    // ...
};
```

然而，使用已定义的 `Shape`（§3.2.4）而不加修改会更有趣（而且在许多情况下更现实）：

```cpp
struct Io_circle : Circle, Io_obj {
    Io_circle(istream&); // initialize from input stream
    Io_circle* clone() const { return new Io_circle{*this}; } // use copy constructor
    static Io_obj* new_circle(istream& is) { return new Io_circle{is}; } // for io_map
};
```

这个例子展示了如何借助一个抽象类将某个类适配到层次结构中，而所需的远见要比一开始就把它构建为节点类所需的远见更少（§21.2.2）。

`Io_circle(istream&)` 构造函数使用其 `istream` 参数中的数据初始化对象。`new_circle()` 函数是放入 `io_map` 中的那个函数，用于让对象 I/O 系统知道该类。例如：

```cpp
io_map["Io_circle"] = &Io_circle::new_circle; // somewhere
```

其他形状以同样的方式构造：

```cpp
class Io_triangle : public Triangle, public Io_obj {
    // ...
};
```

```cpp
io_map["Io_triangle"] = &Io_triangle::new_triangle; // somewhere
```

# 22.2.4 恢复接口

如果编写对象 I/O 脚手架的工作变得繁琐，模板可能会有所帮助：

```cpp
template<class T>
struct Io : T, Io_obj {
public:
    Io(istream&); // initialize from input stream
    Io* clone() const override { return new Io{*this}; }
    static Io* new_io(istream& is) { return new Io{is}; } // for io_map
};
```

有了这个模板，我们可以定义 `Io_circle`：

```cpp
using Io_circle = Io<Circle>;
```

不过，我们仍然需要显式定义 `Io<Circle>::Io(istream&)`，因为它需要了解 `Circle` 的细节。请注意，`Io<Circle>::Io(istream&)` 无权访问 `T` 的私有或受保护数据。其思想是，类型 `X` 的传输格式就是使用 `X` 的某个构造函数构造 `X` 所需的信息。流中的信息不一定是 `X` 成员值的序列。

`Io` 模板是一个将具体类型适配到类层次结构中的例子，其方式是提供一个作为该层次结构节点的句柄。它从模板参数派生，以允许从 `Io_obj` 进行转换。例如：

```cpp
void f(Io<Shape>& ios)
{
    Shape* ps = &ios;
    // ...
}
```

不幸的是，从模板参数派生使得 `Io` 无法用于内置类型：

```cpp
using Io_date = Io<Date>; // wrap concrete type
using Io_int = Io<int>;   // error: cannot derive from built-in type
```

这个问题可以通过将用户对象作为 `Io_obj` 的成员来处理：

```cpp
template<class T>
struct Io : Io_obj {
    T val;
    Io(istream&); // initialize from input stream
    Io* clone() const override { return new Io{*this}; }
    static Io* new_io(istream& is) { return new Io{is}; } // for io_map
};
```

现在我们可以处理：

```cpp
using Io_int = Io<int>; // wrap built-in type
```

由于将值作为成员而不是基类，我们不能再直接将 `Io_obj<X>` 转换为 `X`，因此我们提供了一个函数来完成这一操作：

```cpp
template<typename T>
T* get_val(Io_obj* p)
{
    if (auto pp = dynamic_cast<Io<T>*>(p))
        return &pp->val;
    return nullptr;
}
```

`user()` 函数现在变成：

```cpp
void user()
{
    // ... open file assumed to hold shapes, and attach ss as an istream for that file ...
    unique_ptr<Io_obj> p{get_obj(ss)}; // read object from stream

    if (auto sp = get_val<Shape>(p.get())) {
        sp->draw(); // use the Shape
        // ...
    }
    else {
        // ... oops: cope with non-shape in Shape file ...
    }
}
```

这个简单的对象 I/O 系统并不能满足所有人的需求，但它几乎可以放在一页纸上，而且其关键机制有许多用途。它是用于以类型安全的方式通过通信通道传输任意对象的系统“接收端”的蓝图。更一般地，这些技术可用于根据用户提供的字符串调用函数，以及通过运行时类型识别发现的接口来操作未知类型的对象。

通常，这种对象 I/O 系统的发送方部分也会使用 RTTI。考虑：

```cpp
class Face : public Shape {
public:
    Shape* outline;
    array<Shape*> eyes;
    Shape* mouth;
    // ...
};
```

要正确写出 `outline` 所指向的 `Shape`，我们需要弄清楚它是哪种 `Shape`。这项工作由 `typeid()` 完成（§22.5）。通常，我们还必须保留一个（指针、唯一标识符）对的表，以便能够传输链接的数据结构，并避免重复由多个指针（或引用）指向的对象。

# 22.3 双分派与访问者

经典的面向对象编程基于根据对象的动态类型（最派生类的类型）选择虚拟函数，仅给出指向接口（基类）的指针或引用。特别是，C++ 可以对一次一个类型执行这种运行时查找（也称为动态分派）。在这方面，C++ 与 Simula 和 Smalltalk 以及 Java 和 C# 等更新的语言相似。无法根据两个动态类型选择函数可能是一个严重的限制。此外，虚拟函数必须是成员函数。这意味着我们无法在不修改提供接口的基类（们）以及应受影响的所有派生类的情况下向类层次结构添加虚拟函数。这也可能是一个严重的问题。本节描述了这些问题的解决方法：

- §22.3.1 双分派 展示了如何根据两种类型选择虚拟函数。
- §22.3.2 访问者 展示了如何使用双分派仅在层次结构中添加一个虚拟函数的情况下向类层次结构添加多个函数。

这些技术的最现实的例子出现在我们处理数据结构时，例如向量、图或指向多态类型对象的指针。在这种情况下，对象的实际类型（例如，向量元素或图节点）只能通过（隐式或显式）检查基类提供的接口在动态时才知道。

## 22.3.1 双分派

考虑如何根据两个参数选择函数。例如：

```cpp
void do_something(Shape& s1, Shape& s2)
{
    if (s1.intersect(s2)) {
        // the two shapes overlap
    }
    // ...
}
```

我们希望它对 `Shape` 层次结构中的任意两个类都有效，例如 `Circle` 和 `Triangle`。

基本策略是进行一次虚拟函数调用以选择 `s1` 的正确函数，然后进行第二次调用以选择 `s2` 的正确函数。为了简化，我将省略是否实际相交的计算，只写出选择正确函数的代码骨架。首先我们定义带有相交函数的 `Shape`：

```cpp
class Circle;
class Triangle;

class Shape {
public:
    virtual bool intersect(const Shape&) const = 0;
    virtual bool intersect(const Circle&) const = 0;
    virtual bool intersect(const Triangle&) const = 0;
};
```

接下来我们需要定义 `Circle` 和 `Triangle` 以重写这些虚拟函数：

```cpp
class Circle : public Shape {
public:
    bool intersect(const Shape&) const override;
    virtual bool intersect(const Circle&) const override;
    virtual bool intersect(const Triangle&) const override;
};

class Triangle : public Shape {
public:
    bool intersect(const Shape&) const override;
    virtual bool intersect(const Circle&) const override;
    virtual bool intersect(const Triangle&) const override;
};
```

现在每个类都可以处理 `Shape` 层次结构中的所有可能类，因此我们只需要决定每种组合应该做什么：

```cpp
bool Circle::intersect(const Shape& s) const { return s.intersect(*this); }
bool Circle::intersect(const Circle&) const { cout << "intersect(circle,circle)\n"; return true; }
bool Circle::intersect(const Triangle&) const { cout << "intersect(circle,triangle)\n"; return true; }
```

