
我们现在可以通过调用 `Smiley` 的基类和成员 `draw(j)` 来定义 `Smiley::draw()`：

```
void Smiley::draw() const
{
  Circle::draw();
  for (auto p : eyes)
    p->draw();
  mouth->draw();
}
```

`Smiley::draw()` 的方式即使调用者不知道对象的大小和数据布局，对象也能被正确使用。调用者的实现只需要知道 `Container` 中指向 `vtable` 指针的位置以及每个虚函数使用的索引。这种虚函数调用机制可以确保 `Smiley` 的基类和成员被正确调用。虚函数调用确保了调用的是正确的派生类。

### 5.5.1 层次结构带来的好处

类层次结构提供了两种好处：

- 接口继承：在任何需要基类对象的地方，都可以使用派生类。

- 实现继承：基类提供实现。例如，考虑一个从输入流读取形状的函数：

```cpp
enum Kind { circle, triangle, smiley };

Shape* read_shape(istream& is) // 它从输入流读取
{
  Kind k; // 找到 Kind
  switch (k) {
    case Kind::circle: // 读取圆数据 (Point,r)
      return new Circle(p,r);
    case Kind::triangle: // 读取三角形数据 (Point,p2,p3)
      return new Triangle(p1,p2,p3);
    case Kind::smiley: // 读取笑脸数据 (Point,r)
      Smiley* ps = new Smiley(p,r);
      ps->add_eye(e1);
      ps->add_eye(e2);
      ps->set_mouth(m);
      return ps;
  }
}
```

程序可以使用：

```cpp
void user()
{
  vector<Shape> v;

  while (cin)
    v.push_back(read_shape(cin));

  draw_all(v);
  rotate_all(v,45);

  for (auto p : v)
    delete p;
}
```

显然，这个示例是简化的——特别是关于错误处理——但它生动地说明了 `user()` 绝对没有它要操作的形状。`user()` 代码可以被编译并用于以后添加的形状。注意，外部没有指针指向 `user()`，所以 `user()` 的虚析构函数负责释放这些。由于析构函数是虚的，`delete` 运算符会正确调用最派生类的 `Shape` 虚析构函数。这至关重要，因为派生类可能获取了需要释放的所有资源（如文件句柄、锁和输出流）。在这种情况下，`Smiley` 删除它的眼睛和嘴对象。在完成这些之后，它会调用 `Circle` 的析构函数。对象是“自下向上”（基类优先）构造的，并“自上向下”（派生类）析构的。

如果在运行时，`dynamic_cast` 参数（此处为 `ps`）所指向的对象不是预期的类型（此处为 `Smiley`）或该预期类型的派生类，`dynamic_cast` 返回 `nullptr`。

当不同派生类的对象是有效变体时，我们使用 `dynamic_cast` 对指针进行类型转换。然后我们测试它是否为 `nullptr`。这种测试通常可以方便地放在变量的初始化中。

当另一种类型不可接受时，可以使用 `dynamic_cast` 转换为引用类型。如果对象不是预期的类型，`dynamic_cast` 会抛出 `bad_cast` 异常：

点击此处查看代码图片

```
Shape* ps (read_Shape());
Smiley& r (dynamic_cast<Smiley&>(*ps)); // 否则，捕获 std::bad_cast;
```

当我们节制使用 `dynamic_cast` 时，代码会更简洁。如果我们避免在运行时类型信息，就可以编写更简单、更高效的代码，但偶尔会丢失信息且必须恢复。这通常发生在我们将对象传递给某些接受类指定的接口的系统时。当该系统后将对象传回给我们时，我们可能必须恢复原始类型。与 `dynamic_cast` 类似的操作被称为“is kind of”和“is instance of”操作。

### 5.5.3 避免资源泄漏

“泄漏”是当我们获取资源但未能释放它时发生的一种通用术语。资源泄漏是可以避免的，因为泄漏会导致系统无法使用该资源。因此，随着系统耗尽所需的资源，泄漏最终会导致运行变慢或崩溃。

经验丰富的程序员会注意到，我在 `Smiley` 示例中留下了三个可能出错的机会：

- 实现者可能忘记删除指向 `mouth` 的指针。

- `read_Shape()` 的用户可能忘记删除返回的指针。

- `Shape` 容器的所有者可能忘记删除所指向的对象。

从这个意义上说，指向在空闲存储（free store）上分配对象的指针是危险的：不应使用“**普通旧指针**（plain old pointer，即裸指针）来进行适当的所有权管理。例如：

点击此处查看代码图片

```
void user(int x) {
  Shape* p = new Circle(Point(0,0),10);
  //...
  if (x<0) throw Bad_x(); // 否则泄漏
  if (x==0) return; // 否则泄漏
  //...
  delete p;
}
```

除非 `x` 为正数，否则这将泄漏。将 `new` 的结果赋值给“裸指针”是自找麻烦。

解决此类问题的简单方法之一是在需要删除时使用标准库的 `unique_ptr` (15.2.1) 而不是“裸指针”

点击此处查看代码图片

```
class Smiley : public Circle {
  // ...
  private:
    vector<unique_ptr<Shape>> eyes; // 通常使用两个
    unique_ptr<Shape> mouth;
};
```

这是一个简单、通用且高效的资源管理技术（6.3）示例。作为这一改变的额外益处，我们不再需要为 `Smiley` 定义析构函数。编译器将隐式生成 `vector` 中 `unique_ptr` (6.3) 所需的析构函数。使用 `unique_ptr` 的代码与正确使用原始指针的代码一样简单。

现在考虑 `read_shape()` 的用户：

点击此处查看代码图片

```
unique_ptr<Shape> read_shape(istream& is) // 从输入流读取形状描述
{
  // ... 从输入流读取形状头并找到其类型 k ...

  switch (k) {
    case Kind::circle:
      // ... 将圆形数据 (Point,int) 入 p 和 r
      return unique_ptr<Shape>(new Circle(p)); // 15.2.1
  }
}
```

```
void user() {
  vector<unique_ptr<Shape>> v;

  while (cin) {
    v.push_back(read_shape(cin));
  }

  draw_all(v); // 为每个元素绘制(all)
  rotate_all(v,45); // 为每个元素旋转(45)
}
```

每个对象都由一个 `unique_ptr` 所有，该指针在不再需要对象时（即其 `unique_ptr` 出作用域时）将删除对象。

为了让 `unique_ptr` 版本的 `user()` 发工作，我们需要接受 `vector<unique_ptr<Shape>>` 的 `draw_all()` 和 `rotate_all()` 版本。编写许多 `_all()` 函数可能会变得冗长；7.3.2 显示了替代方案。

## 5.6 建议

[1] 在代码中直接表达思想；5.1; [CG:2]。

[2] 具体的类型是最简单的类类型。在适用情况下，优先使用具体类型而非更复杂的类；5.2; [CG:10]。

[3] 使用具体类来表示简单的概念；5.2。

[4] 对于性能至关重要的组件，优先使用具体类而非类层级结构；5.2。

[5] 定义构造函数来处理对象的初始化；5.2.1, 6.1; [CG:4]。

[6] 只有当函数需要直接访问类的表示时才创建该函数；5.2.1; [CG:4]。

[7] 定义运算符以模拟惯用法；5.2.1; [CG:6]。

[8] 对称操作使用数值类型；5.2.1; [CG:1]。

[9] 声明一个不修改 `const` 状态的成员函数；5.2.1。

[10] 如果构造函数获取了资源，则类需要删除该资源；5.2.2; [CG:20]。

[11] 避免“裸” `new` 和 `delete` 操作；5.2.2; [CG:11]。

[12] 使用资源句柄和 RAII 管理资源；5.2.2; [CG:1]。

[13] 如果类是容器，它有一个初始化列表构造函数；5.2.3; [CG:10]。

[14] 当需要完全分离接口和实现时，使用抽象类作为接口；5.3; [CG:22]。

[15] 通过指针和引用访问多态对象；5.3; [CG:126]。

[16] 抽象类通常不需要构造函数；5.3; [CG:126]。

[17] 使用类层级结构表示具有固有结构的概念；5.5; [CG:127]。

[18] 带有虚函数的类应该有虚析构函数；5.5; [CG:127]。

[19] 使用 `override` 在类层级结构中显式重写；5.5; [CG:28]。

[20] 在设计类层级结构时，区分初始化和接口继承；5.5; [CG:29]。

[21] 使用 `dynamic_cast` 转换为类型时是预期的；5.5。

[22] 转换为引用类型时使用 `dynamic_cast`；5.5; [CG:146]。

[23] 使用 `unique_ptr` 或 `shared_ptr` 避免使用 `new` 创建对象；5.5; [CG:15]。

# 6 核心操作

> 有人说我想要一个糖果，

– Alan Perlis

- 引言

- 核心操作; 转换; 成员初始化

- 拷贝和移动

    - 拷贝容器；移动容器

- 资源管理

- 运算符重载

- 惯用操作    - 容器操作；输入输出操作

- 用户定义字面量

- 建议

## 6.1 引言

初始化、赋值、拷贝和移动等操作在逻辑上是基础的因为语言规则对它们做了假设。如果类具有执行非空任务的析构函数（例如释放内存或释放锁），该类可能需要实现：

### 6.1.1 核心操作

构造函数、析构函数以及拷贝和移动操作对于一个类型来说在逻辑上并不是独立的。我们必须将它们定义一组，否则会导致逻辑或性能问题。

```
class X {
public:
    X(Sometype); // “普通构造函数”：创建一个对象
    X(); // 默认构造函数
    X(const X&); // 拷贝构造函数
    X(X&&); // 移动构造函数
    X& operator=(const X&); // 拷贝赋值：清理目标并拷贝
    X& operator=(X&&); // 移动赋值：清理目标并移动
    ~X(); // 析构函数：清理
};
```

在五种情况下可以拷贝或移动：

- 作为赋值的源

- 作为对象初始化

- 作为函数参数

- 作为函数返回值

- 作为异常

赋值使用拷贝或移动赋值运算符。原则上，其他情况使用拷贝或移动构造函数。然而，编译器通常会通过直接在目标对象中构造对象来优化拷贝或移动构造函数的调用。例如：

```
X make(Sometype);
x = make(value);
```

在这里，编译器通常直接在 `x` 中从 `make()` 构建 X；消除拷贝。

除了命名对象和空闲存储对象的初始化外，构造函数还用于初始化临时对象和实现显式类型转换。除了“普通构造函数”外，这些特殊成员函数将在需要时由编译器生成。如果你想显式生成默认实现，可以：

点击此处查看代码图片

```
class Y {
public:
    Y(Sometype); // 我真的想要默认拷贝构造函数
    Y(const Y&) = default; 
    Y(Y&&) = default; // 以及默认移动构造函数
    // ...
};
```

如果你显式指定了某些默认值，其他的默认定义将不会生成。

当类拥有指针成员时，显式地定义拷贝和移动操作通常是一个好主意。这是因为指针可能指向类需要删除的内存，在这种情况下，默认的成员函数将是错误的。或者，指针可能指向类并不需要删除的内容。无论哪种情况，代码层面都应该知道这一点。例如，请参见 §6.2.1。

一个好的经验法则（有时被称为“零规则”）是要么定义所有的基本操作，要么一个都不定义（对所有操作使用默认）。例如：

点击此处查看代码

```cpp
struct Z {
  Vector v;
  string s;
};

Z z1; // Default initialize z1.v and z1.s
Z z2 = z1; // Default copy z1.v and z1.s
```

在这里，编译器将根据需要合成成员的默认构造、拷贝、移动和析构函数，并具有正确的语义。

使用 `=delete` 来补充 `=default`，指示不生成某个操作。类层次结构中的基类是一个不允许成员拷贝的经典例子。例如：

点击此处查看代码

```cpp
class Shape {
public:
  Shape(const Shape&)=delete; // No copying
  Shape& operator=(const Shape&)=delete;
  // ...
};

void copy(Shape& s1, const Shape& s2)
{
  s1 = s2; // Error: Shape copy is deleted
}
```

`=delete` 会使删除的函数成为编译错误；`=delete` 可以用于任何函数，而不只是基本成员函数。

## 6.1.2 转换

接受单个参数的构造函数定义了从其参数类型的转换。例如，complex (§5.2.1) 提供了一个从 `double` 的构造函数：

点击此处查看代码

```cpp
complex z1 = 3.14; // z1 becomes (3.14,0.0)
complex z2 = *z1; // z2 becomes z1*(2.0,0) == (6.28,0.0)
```

这种隐式转换有时是理想的，但并非总是如此。例如，Vector (§5.2.2) 提供了一个从 `int` 的构造函数：

点击此处查看代码

```cpp
Vector v1 = 7; // OK: v1 has 7 elements
```

这通常被认为是不利的，标准库中的 `vector` 不允许这种从 `int` 到 `vector` 的“转换”。

避免此问题的方法是说明只允许显式“转换”；即，我们可以这样定义构造函数：

点击此处查看代码

```cpp
class Vector {
public:
    explicit Vector(int s); // No implicit conversion from int to Vector
    // ...
};
```

这使得：

点击此处查看代码

```cpp
Vector v1 = 7; // OK: v1 has 7 elements
Vector v2 = 7; // Error: no implicit conversion from int to Vector
```

涉及转换时，更多像 Vector 这样的类型与 complex 类似，因此除非有充分理由，否则对接受单个参数的构造函数使用 `explicit`。

## 6.1.3 成员初始化

当类的成员被定义时，我们可以提供一个称为默认成员初始化器的默认初始化值。complex (§5.2.1) 的修订版：

点击此处查看代码

```cpp
class complex {
    double re = 0;
    double im = 0; // representation: two doubles with default value 0.0
public:
    complex(double r, double i) : re(r), im(i) {} // construct complex from two scalars: {r,i}
    complex(double r) : re(r) {} // construct complex from one scalar: {r,0}
    complex() {} // default complex: {0,0}
};
```

当构造函数没有提供值时，就会使用默认值。这简化了代码并帮助我们避免意外遗漏成员初始化。

## 6.2 拷贝和移动

默认情况下，对象是被拷贝的。这对于用户定义的类型以及内置类型都是如此。拷贝的默认含义是成员拷贝：拷贝每个成员。例如，使用 §5.2.1 中的 complex：

点击此处查看代码

```cpp
void test(complex z1)
{
    complex z2 (z1); // Il initialization
    complex z3;
    z3 = z2; // Il copy assignment
    // ...
}
```

现在 z1、z2 和 z3 具有相同的值，因为赋值和初始化都拷贝了两个成员。

当我们设计一个类时，必须始终考虑对象可能何时以及如何被拷贝。对于简单的具体类型，成员拷贝是拷贝的正确语义。对于复杂的复合类型（如 Vector），成员拷贝不是拷贝的正确语义；对于抽象类型，它几乎永远不是。

### 6.2.1 拷贝容器
