

```
for(int i = 0; i<9; ++i)
pos.at(i) = arg.pos.at(i); return *this;
}
// ... other operations ...
enum State { empty, nought, cross };
private:
vector<State> pos;
};
```

这据说曾是真实程序的一部分。它使用“魔数”9来实现拷贝赋值，该赋值访问其参数 arg 而不检查参数是否真的有九个元素。此外，它显式实现了拷贝赋值，但没有实现拷贝构造函数。我认为这不是好的代码。

## Section 17.6.3.4 Partially Specified Invariants 523

我们定义了拷贝赋值，因此我们也必须定义析构函数。该析构函数可以是 =default，因为它所需要做的只是确保成员 pos 被销毁，而如果没有定义拷贝赋值，本来也会这样做。此时，我们注意到用户定义的拷贝赋值本质上就是默认情况下会得到的那一个，因此我们也可以将其 =default。为完整起见再添加一个拷贝构造函数，我们得到：

```
class Tic_tac_toe {
public:
Tic_tac_toe(): pos(9) {} // always9positions
Tic_tac_toe(const Tic_tac_toe&) = default;
Tic_tac_toe& operator=(const Tic_tac_toe& arg) = default;
~Tic_tac_toe() = default;
// ... other operations ...
enum State { empty, nought, cross };
private:
vector<State> pos;
};
```

观察到这一点，我们意识到这些 =default 的净效果只是消除了移动操作。我们想要这样吗？可能不是。当我们把拷贝赋值设为 =default 时，我们消除了对魔数 9 的讨厌依赖。除非 Tic_tac_toe 上的其他操作，到目前为止尚未提及，也“硬编码了魔数”，否则我们可以安全地添加移动操作。做到这一点最简单的方法是移除显式的 =default，然后我们会发现 Tic_tac_toe 实际上是一个完全普通的类：

```
class Tic_tac_toe {
public:
// ... other operations ...
enum State { empty, nought, cross };
private:
vector<State> pos {Vector<State>(9)}; // always9positions
};
```

我从这个例子以及其他定义了“奇特组合”的默认操作的例子中得出的一个结论是，我们应该对这类类型高度怀疑：它们的非规则性往往隐藏着设计缺陷。对于每个类，我们都应问自己：

- [1] 是否需要默认构造函数（因为默认的默认构造函数不充分或已被其他构造函数抑制）？
- [2] 是否需要析构函数（例如，因为某些资源需要被释放）？
- [3] 是否需要拷贝操作（因为默认的拷贝语义不充分，例如因为该类旨在作为基类或因为它包含指向必须由该类删除的对象的指针）？
- [4] 是否需要移动操作（因为默认语义不充分，例如因为空对象没有意义）？

特别是，我们绝不能孤立地考虑其中一个操作。

## 17.6.4 deleted Functions

我们可以“删除”一个函数；也就是说，我们可以声明一个函数不存在，这样尝试使用它（隐式或显式）就会出错。最明显的使用是消除原本会被默认的函数。例如，通常希望防止用作基类的类的拷贝，因为这种拷贝很容易导致切片（§17.5.1.4）：

```
class Base {
// ...
Base& operator=(const Base&) = delete;// disallowcopying
Base(const Base&) = delete;

Base& operator=(Base&&) = delete; // disallowmoving Base(Base&&) = delete;
};
Base x1;
Base x2 {x1}; // error : no copy constructor
```

启用和禁用拷贝与移动通常更方便地通过说明我们想要什么（使用 =default；§17.6.1）而不是说明我们不想要什么（使用 =delete）来实现。然而，我们可以删除任何我们可以声明的函数。例如，我们可以从函数模板的可能特化集合中消除一个特化：

```
template<class T>
T* clone(T*p) // returncopyof*p
{
return new T{*p}; };
Foo* clone(Foo*) = delete; // don’t trytoclone a Foo

void f(Shape * ps, Foo* pf) {
Shape* ps2 = clone(ps); Foo* pf2 = clone(pf);
}

// fine
// error : clone(Foo*) deleted
```

另一个应用是消除不需要的转换。例如：

```cpp
struct Z {
// ...
Z(double); // can initialize with a double
Z(int) = delete; // but not with an integer
};

void f() {
Z z1 {1}; // error: Z(int) deleted
Z z2 {1.0}; // OK
}
```

## Section 17.6.4 **deleted** Functions 525

进一步的用途是控制类可以被分配的位置：

```cpp
class Not_on_stack {
// ...
~Not_on_stack() = delete;
};

class Not_on_free_store {
// ...
void* operator new(size_t) = delete;
};
```

你不能拥有一个无法被销毁的局部变量（§17.2.2），也不能在你已 **=deleted** 其类内存分配操作符时在自由存储上分配对象（§19.2.5）。例如：

```cpp
void f()
{
Not_on_stack v1; // error: can’t destroy Not_on_free_store
Not_on_free_store v2; // OK

Not_on_stack* p1 = new Not_on_stack; // OK
Not_on_free_store* p2 = new Not_on_free_store; // error: can’t allocate
}
```

然而，我们永远无法 **delete** 那个 **Not_on_stack** 对象。使析构函数 **private**（§17.2.2）的替代技术可以解决这个问题。

注意 **=delete**d 函数与根本未声明的函数之间的区别。在前一种情况下，编译器注意到程序员尝试使用 **deleted** 函数并给出错误。在后一种情况下，编译器会寻找替代方案，例如不调用析构函数或使用全局 **operator new()**。

## 17.7 Advice

- [1] 将构造函数、赋值和析构函数设计为一组匹配的操作；§17.1。
- [2] 使用构造函数为类建立不变量；§17.2.1。
- [3] 如果构造函数获取资源，其类需要析构函数来释放资源；§17.2.2。
- [4] 如果类有虚函数，它需要虚析构函数；§17.2.5。
- [5] 如果类没有构造函数，它可以通过逐成员初始化进行初始化；§17.3.1。
- [6] 优先使用 {} 初始化而非 = 和 () 初始化；§17.3.2。
- [7] 仅当存在“自然”的默认值时才为类提供默认构造函数；§17.3.3。
- [8] 如果类是容器，请为其提供 initializer-list 构造函数；§17.3.4。
- [9] 按声明顺序初始化成员和基类；§17.4.1。
- [10] 如果类有引用成员，它可能需要拷贝操作（拷贝构造函数和拷贝赋值）；§17.4.1.1。
- [11] 在构造函数中优先使用成员初始化而非赋值；§17.4.1.1。
- [12] 使用类内初始化器提供默认值；§17.4.4。
- [13] 如果类是资源句柄，它可能需要拷贝和移动操作；§17.5。
- [14] 编写拷贝构造函数时要小心复制每个需要被复制的元素（注意默认初始化器）；§17.5.1.1。
- [15] 拷贝操作应提供等价性和独立性；§17.5.1.3。
- [16] 警惕纠缠的数据结构；§17.5.1.3。
- [17] 优先使用移动语义和写时复制而非浅拷贝；§17.5.1.3。
- [18] 如果类用作基类，请防止切片；§17.5.1.4。
- [19] 如果类需要拷贝操作或析构函数，它可能需要构造函数、析构函数、拷贝赋值和拷贝构造函数；§17.6。
- [20] 如果类有指针成员，它可能需要析构函数和非默认拷贝操作；§17.6.3.3。
- [21] 如果类是资源句柄，它需要构造函数、析构函数和非默认拷贝操作；§17.6.3.3。
- [22] 如果默认构造函数、赋值或析构函数是合适的，让编译器生成它（不要自己重写）；§17.6。
- [23] 明确你的不变量；使用构造函数建立它们，使用赋值维护它们；§17.6.3.2。
- [24] 确保拷贝赋值对自赋值是安全的；§17.5.1。
- [25] 向类添加新成员时，检查是否有用户定义的构造函数需要更新以初始化该成员；§17.5.1。

