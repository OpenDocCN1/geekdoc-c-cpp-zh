
模板和类层次结构的结合提供了单一方法无法提供的设计选择和灵活性。例如，指向基类的指针可作为模板参数使用以提供运行时多态（§3.2.4），模板参数可用于指定基类接口以提供类型安全（§26.3.7、§27.3.1）。

不能有 `virtual` 函数模板（§23.4.6.2）。

## 27.2.1 生成的类型

类模板可被理解为一种规范，说明特定类型如何创建。换句话说，模板实现是一种机制，当需要时基于规范生成类型。因此，类模板有时被称为 `类型生成器`。

就 C++ 语言规则而言，从单个类模板生成的两个类之间没有关系。例如：

```
class Shape {
// ...
};
```

```
class Circle : public Shape { {
// ...
};
```

给定这些声明，人们有时认为 `set<Circle>` 和 `set<Shape>` 之间必须存在继承关系，或者至少 `set<Circle*>` 和 `set<Shape*>` 之间存在继承关系。这是基于有缺陷的论证的严重逻辑错误：“一个 `Circle` 是一个 `Shape`，所以一个 `Circle` 的集合也是一个 `Shape` 的集合；因此，我应该能够将一个 `Circle` 的集合用作一个 `Shape` 的集合。” 这个论证的“因此”部分不成立。原因是一个 `Circle` 的集合保证集合的成员是 `Circle`；一个 `Shape` 的集合不提供该保证。例如：

第 27.2.1 节 生成的类型 763

```
class Triangle : public Shape { // ...
};
```

```
void f(set<Shape *>& s) {
```

```cpp
// ...
s.insert(new Triangle{p1,p2,p3});
}

void g(set<Circle*>& s)
{
    f(s); // error, type mismatch: s is a set<Circle*>, not a set<Shape*>
}
```

这不会编译，因为不存在从 `set<Circle*>&` 到 `set<Shape*>&` 的内置转换。也不应该有。`set<Circle*>` 的成员都是 Circles 这一保证使我们能够安全高效地对集合的成员应用 Circle 特定操作，例如确定半径。如果我们允许将 `set<Circle*>` 当作 `set<Shape*>` 来处理，我们就无法再维持该保证。例如，`f()` 将 `Triangle*` 插入到其 `set<Shape*>` 参数中。如果 `set<Shape*>` 可能是一个 `set<Circle*>`，那么 `set<Circle*>` 只包含 `Circle*` 的基本保证就会被违反。

从逻辑上讲，我们可以将不可变的 `set<Circle*>` 当作不可变的 `set<Shape*>`，因为当我们无法更改集合时，就不会出现向集合中插入不适当元素的问题。也就是说，我们可以提供从 `const set<const Circle*>` 到 `const set<const Shape*>` 的转换。语言默认不这样做，但 `set` 的设计者可以这样做。

数组与基类的组合尤其糟糕，因为内置数组不提供容器所提供的类型安全。例如：

```cpp
void maul(Shape* p, int n) // Danger!
{
    for (int i=0; i!=n; ++i)
        p[i].draw(); // looks innocent; it is not
}

void user()
{
    Circle image[10]; // an image is composed of 10 Circles
    // ...
    maul(image, 10); // “maul” 10 Circles
    // ...
}
```

我们如何用 `image` 调用 `maul()`？首先，`image` 的类型从 `Circle[]` 转换（衰变）为 `Circle*`。接下来，`Circle*` 转换为 `Shape*`。将数组名隐式转换为指向数组第一个元素的指针是 C 风格编程的基础。同样，将指向派生类的指针隐式转换为指向其基类的指针也是面向对象编程的基础。结合起来，它们提供了灾难的机会。

在上面的示例中，假设 `Shape` 是一个大小为 4 的抽象类，而 `Circle` 添加了一个中心和一个半径。那么 `sizeof(Circle) > sizeof(Shape)`，当我们查看 `image` 的布局时，我们会发现类似这样的情况：

```text
user() view: image[0] image[1] image[2] image[3]
maul() view: p[0]     p[1]     p[2]     p[3]
```

当 `maul()` 尝试在 `p[1]` 上调用虚函数时，期望的位置上没有虚函数指针，调用很可能会立即失败。

请注意，没有需要显式转换才能得到这种灾难：

- 优先使用容器而不是内置数组。

- 视形如 `void f(T* p, int count)` 的接口为高度可疑；当 `T` 可以是基类且 `count` 是元素计数时，麻烦即将到来。

- 当应用于 supposed to be 运行时多态的东西时，将 `.` 视为可疑，除非它显然应用于引用。

# 27.2.2 模板转换

从同一个模板生成的类之间没有任何默认关系（§27.2.1）。然而，对于某些模板，我们希望表达这种关系。例如，当我们定义一个指针模板时，我们希望反映指向对象的继承关系。成员模板（§23.4.6）允许我们在需要时指定许多此类关系。考虑：

```cpp
template<typename T>
class Ptr { // pointer to T
    T* p;

public:
    Ptr(T*);
    Ptr(const Ptr&); // copy constructor

    template<typename T2>
    explicit operator Ptr<T2>(); // convert Ptr<T> to Ptr<T2>
    // ...
};
```

我们希望定义转换运算符，以为这些用户定义的 `Ptr` 提供我们对内置指针所习惯的继承关系。例如：

```cpp
void f(Ptr<Circle> pc)
{
    Ptr<Shape> ps{pc};  // should work
    Ptr<Circle> pc2{ps}; // should give error
}
```

我们希望仅当 `Shape` 真的是 `Circle` 的直接或间接公共基类时才允许第一次初始化。一般来说，我们需要定义转换运算符，使得 `Ptr<T>` 到 `Ptr<T2>` 的转换仅在 `T*` 可以赋给 `T2*` 时才被接受。这可以这样做：

```cpp
template<typename T>
template<typename T2>
Ptr<T>::operator Ptr<T2>()
{
    return Ptr<T2>{p};
}
```

只有当 `p`（它是一个 `T*`）可以作为 `Ptr<T2>(T2*)` 构造函数的参数时，return 语句才会编译。因此，如果 `T*` 可以隐式转换为 `T2*`，则 `Ptr<T>` 到 `Ptr<T2>` 的转换将起作用。例如，我们现在可以写：

```cpp
void f(Ptr<Circle> pc)
{
    Ptr<Shape> ps{pc};   // OK: can convert Circle* to Shape*
    Ptr<Circle> pc2{ps}; // error: cannot convert Shape* to Circle*
}
```

要小心只定义逻辑上有意义的转换。如果有疑问，请使用命名转换函数，而不是转换运算符。命名转换函数提供更少的歧义机会。

模板的模板参数列表与其模板成员之一的模板参数列表不能合并。例如：

```cpp
template<typename T, typename T2> // error
Ptr<T>::operator Ptr<T2>()
{
    return Ptr<T2>(p);
}
```

解决此问题的另一种方法使用类型特征和 `enable_if()`（§28.4）。

# 27.3 类模板的层次结构

使用面向对象技术，基类通常用于为一组派生类提供通用接口。模板可用于参数化此类接口，并且在这样做时，很容易想用相同的模板参数来参数化整个派生类层次结构。例如，我们可以用用于提供目标输出“设备”抽象的类型来参数化经典的形状示例（§3.2.4）：

```cpp
template<typename Color_scheme, typename Canvas> // questionable example
class Shape {
    // ...
};

template<typename Color_scheme, typename Canvas>
class Circle : public Shape {
    // ...
};

template<typename Color_scheme, typename Canvas>
class Triangle : public Shape {
    // ...
};
```

```cpp
void user()
{
    auto p = new Triangle<RGB, Bitmapped>{
        {{0, 0}, {0, 60}, {30, sqrt(60 * 60 - 30 * 30)}}
    };
    // ...
}
```

沿着这条线通常是程序员在看到类似 `vector<T>` 的东西后，习惯于面向对象编程时首先考虑的想法。然而，在混合面向对象和通用技术时应谨慎。

如所写，这种参数化形状层次结构对于实际使用来说过于冗长。这可以通过使用默认模板参数（§25.2.5）来解决。然而，冗长并不是主要问题。如果程序中只使用一种 `Color_scheme` 和 `Canvas` 组合，生成的代码量几乎与未参数化的等价物相同。“几乎”是因为编译器会抑制类模板的未使用非虚成员函数的定义代码生成。然而，如果程序中使用了 N 种 `Color_scheme` 和 `Canvas` 组合，则每个虚函数的代码将被复制 N 次。因为图形层次结构可能有许多派生类、许多成员函数和许多复杂的函数，所以结果很可能导致巨大的代码膨胀。特别是，编译器无法知道虚函数是否被使用，因此必须为所有此类函数以及此类函数调用的所有函数生成代码。用许多虚成员函数的大型类层次结构参数化通常是一个糟糕的主意。

对于此形状示例，`Color_scheme` 和 `Canvas` 参数不太可能影响接口太多：大多数成员函数不会将其作为函数类型的一部分。这些参数是“实现细节”，却逃逸到了接口中——可能带来严重的性能影响。并不是整个层次结构需要这些参数；而是少数配置函数和（很可能）少数低级绘图/渲染函数。一般来说，“过度参数化”（§23.4.6.3）不是一个好主意：尽量避免只影响少数成员的参数。如果只有少数成员函数受参数影响，请尝试使这些函数成为具有该参数的函数模板。例如：

```cpp
class Shape {
    template<typename Color_scheme, typename Canvas>
    void configure(const Color_scheme&, const Canvas&);
    // ...
};
```

如何在不同类和不同对象之间共享配置信息是另一个问题。显然，我们不能简单地在 `Shape` 中存储一个 `Color_scheme` 和 `Canvas`，而不对 `Shape` 本身进行参数化。一个解决方案是让 `configure()` 将 `Color_scheme` 和 `Canvas` 中的信息“翻译”成一组标准配置参数（例如，一组整数）。另一个解决方案是给 `Shape` 一个 `Configuration*` 成员，其中 `Configuration` 是一个提供配置信息通用接口的基类。

## 27.3.1 模板作为接口

模板类可用于为通用实现提供灵活且类型安全的接口。§25.3 中的 `Vector` 就是一个很好的例子：

```
template<typename T>
class Vector<T*>
    : private Vector<void*>
{
    // ...
};
```

总的来说，这种技术可用于提供类型安全的接口，并将类型转换局部化到实现中，而不是强迫用户编写它们。

# 27.4 模板参数作为基类

在经典的基于类层次结构的面向对象编程中，我们将不同类之间可能不同的信息放置在派生类中，并通过基类中的虚函数来访问它（§3.2.4、§21.2.1）。这样，我们就能编写通用代码，而不必担心实现中的变化。然而，这种技术不允许我们改变接口中使用的类型（§27.2）。此外，与内联函数的简单操作相比，虚函数调用可能代价较高。为了弥补这一点，我们可以将特化的信息和操作作为模板参数传递给基类。实际上，模板参数可以用作基类。

以下两个小节讨论的一般问题是：“我们如何将分别指定的信息组合成一个具有良好定义接口的紧凑对象？”这是一个基本问题，其解决方案具有普遍重要性。

## 27.4.1 组合数据结构

考虑编写一个平衡二叉树库。由于我们提供的库会被许多不同的用户使用，我们不能将用户（应用）数据的类型构建到我们的树节点中。我们有许多备选方案：

-   我们可以将用户数据放在派生类中，并使用虚函数来访问它。但虚函数调用（或者说运行时解析和检查的解决方案）相对昂贵，而且我们面向用户数据的接口不是以用户类型来表达的，因此仍然需要使用类型转换来访问它。

-   我们可以在节点中放置一个 `void*`，让用户用它来引用在节点外部分配的数据。但这会使分配次数加倍，增加许多（可能代价高昂的）指针解引用，并且每个节点还要增加一个指针的空间开销。我们还需要使用类型转换，以正确的类型访问用户数据。这种转换无法进行类型检查。

-   我们可以在节点中放置 `Data*`，其中 `Data` 是数据结构的“通用基类”。这可以解决类型检查问题，但结合了前两种方法的代价和不便。

还有其他备选方案，但请考虑：

```
template<typename N>
struct Node_base { // doesn’t know about Val (the user data)
    N* left_child;
    N* right_child;

    Node_base();
    void add_left(N* p) {
        if (left_child == nullptr)
            left_child = p;
        else
            // ...
    }
    // ...
};
```

```
template<typename Val>
struct Node : Node_base<Node<Val>> { // use derived class as part of its own base
    Val v;
    Node(Val vv);
    // ...
};
```

这里，我们将派生类 `Node<Val>` 作为模板参数传递给其自身的基类（`Node_base`）。这使得 `Node_base` 能够在其接口中使用 `Node<Val>`，甚至不需要知道它的真实名称！注意，`Node` 的布局是紧凑的。例如，`Node<double>` 大致等价于以下形式：

```
struct Node_base_double {
    double val;
    Node_base_double* left_child;
    Node_base_double* right_child;
};
```

遗憾的是，在这种设计下，用户必须了解 `Node_base` 的操作以及所生成树的结构。例如：

```
using My_node = Node<double>;

void user(const vector<double>& v)
{
    My_node root;
    int i = 0;

    for (auto x : v) {
        auto p = new My_node{x};
        if (i++ % 2) // choose where to insert
            root.add_left(p);
        else
            root.add_right(p);
    }
}
```
