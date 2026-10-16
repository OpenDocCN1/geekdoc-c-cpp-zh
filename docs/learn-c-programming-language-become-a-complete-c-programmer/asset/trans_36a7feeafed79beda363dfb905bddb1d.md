

并不是编译器的职责去决定什么是过度什么是必要的。要为你自己的数据结构获得拷贝到移动的优化，你必须提供移动操作（显式或隐式；参见 §17.6）。

内置类型，如 int 和 double*，被认为具有简单的拷贝的移动操作。像往常一样，你必须小心包含指针的数据结构（§3.3.1）。特别是，不要假设被移动的指针被设为 nullptr。拥有移动操作会影响从函数返回大型对象的惯用法。考虑：

```
Matrix operator+(const Matrix& a, const Matrix& b)
// res[i][j] = a[i][j]+b[i][j] for each i and j
{
if (a.dim[0]!=b.dim[0] || a.dim[1]!=b.dim[1])
throw std::runtime_error("unequal Matrix sizes in +");

Matrix res{a.dim[0],a.dim[1]};
constexpr auto n = a.size();
for (int i = 0; i!=n; ++i)

res.elem[i] = a.elem[i]+b.elem[i];
return res;
}
```

Matrix 有一个移动构造函数，因此“按值返回”既简单高效又“自然”。如果没有移动操作，我们会有性能问题并且必须求助于变通方法。我们可能考虑过：

```
Matrix& operator+(const Matrix& a, const Matrix& b) // beware!
{
Matrix& res = *new Matrix; // allocate on free store
// res[i][j] = a[i][j]+b[i][j] for each i and j
return res;
}
```

在 operator+() 中使用 new 并不明智，并且迫使用户处理棘手的内存管理问题：

- 通过 new 创建的对象如何被删除？
- 我们需要垃圾回收器吗？
- 我们应该使用 Matrix 的池而不是通用的 new 吗？
- 我们需要使用引用计数的 Matrix 表示吗？
- 我们应该重新设计 Matrix 加法的接口吗？
- operator+() 的调用者是否必须记住删除结果？
- 如果计算抛出异常，新分配的内存会怎样？

这些替代方案都不优雅也不通用。

## 17.6 生成默认操作

编写常规操作，如拷贝和析构函数，可能会很繁琐且容易出错，因此编译器可以根据需要为我们生成它们。默认情况下，一个类提供：

- 默认构造函数：`X()`
- 拷贝构造函数：`X(const X&)`
- 拷贝赋值：`X& operator=(const X&)`
- 移动构造函数：`X(X&&)`
- 移动赋值：`X& operator=(X&&)`
- 析构函数：`~X()`

默认情况下，如果程序使用它，编译器会生成其中每一个操作。然而，如果程序员通过定义一个或多个这些操作来接管控制，相关操作的生成将被抑制：

- 如果程序员为一个类声明了任何构造函数，则不会为该类生成默认构造函数。
- 如果程序员为一个类声明了拷贝操作、移动操作或析构函数，则不会为该类生成拷贝操作、移动操作或析构函数。

不幸的是，第二条规则只是不完全被强制执行：为了向后兼容，即使定义了析构函数，拷贝构造函数和拷贝赋值也会被生成。然而，这种生成在 ISO 标准中已被弃用（§iso.D），你应该期望现代编译器会对此发出警告。

如果需要，我们可以明确哪些函数被生成（§17.6.1）以及哪些不被生成（§17.6.4）。

### 17.6.1 显式默认值

由于否则默认操作的生成可能会被抑制，必须有一种方法来获取默认值。此外，一些人更喜欢在程序文本中看到操作的完整列表，即使该完整列表并非必需。例如，我们可以写：

```
class gslice {
  valarray<size_t> size;
  valarray<size_t> stride;
  valarray<size_t> d1;
public:
  gslice() = default;
  ~gslice() = default;
  gslice(const gslice&) = default;
  gslice(gslice&&) = default;
  gslice& operator=(const gslice&) = default;
  gslice& operator=(gslice&&) = default;
  // ...
};
```

这是 `std::gslice` 实现的一部分（§40.5.6）等价于：

```
class gslice {
  valarray<size_t> size;
  valarray<size_t> stride;
  valarray<size_t> d1;
public:
// ...
};
```

我更喜欢后者，但我可以看到在由经验不足的 C++ 程序员维护的代码库中使用前者的意义：你看不到的东西，你可能会忘记。

使用 =default 总是比自己编写默认语义的实现更好。有人可能会认为写点东西比什么都不写更好，于是写：

```
class gslice {
valarray<size_t> size; valarray<size_t> stride; valarray<size_t> d1;

public:
// ...
gslice(const gslice& a);
};

gslice::gslice(const gslice& a)
:size{a.size },
stride{a.stride},
d1{a.d1}
{
}
```

这不仅冗长，使 gslice 的定义更难阅读，而且也为犯错提供了机会。例如，我可能会忘记拷贝其中一个成员并让它被默认初始化（而不是拷贝）。此外，当用户提供一个函数时，编译器不再知道该函数的语义，一些优化就会被抑制。对于默认操作，这些优化可能很重要。

### 17.6.2 默认操作

每个生成的操作的默认含义，如编译器生成时所实现，是将该操作应用于类的每个基类和非静态数据成员。也就是说，我们得到逐成员拷贝、逐成员默认构造等。例如：

```
struct S {
string a;
int b;
};
```

```
S f(S arg) {
S s0 {}; // default construction: {"",0}
S s1 {s0}; // copyconstruction
s1 = arg; // copyassignment
return s1; // moveconstruction
```

```
```cpp
struct Z { // invariant:
// my_favorite is the index of my favorite element of elem
// largest points to the element with the highest value in elem

vector<int> elem;
int my_favorite;
int* largest;
};
```
```

程序员在注释中声明了一个不变量，但编译器不读注释。此外，程序员没有留下关于该不变量如何建立和维护的提示。特别是，没有声明构造函数或赋值。那个不变量是隐式的。其结果是 Z 可以使用默认操作进行拷贝和移动：

```
```cpp
Z v0; // no initialization (oops! possibility of undefined values) Z val { {1,2,3},1,&val[2]};
// OK, but ugly and error-prone
Z v2 = val; // copies: v2.largest points into val
Z v3 = move(val); // moves: val.elem becomes empty; v3.my_favorite is out of range
```
```

这是一团糟。根本问题是 Z 设计得很糟糕，因为关键信息“隐藏”在注释中或完全缺失。默认操作生成的规则是启发式的，旨在捕获常见错误并鼓励对构造、拷贝、移动和销毁的系统化方法。尽可能：

- [1] 在构造函数中建立不变量（可能包括资源获取）。
- [2] 使用拷贝和移动操作维护不变量（使用通常的名称和类型）。
- [3] 在析构函数中执行必要的清理（包括可能释放资源）。

### 17.6.3.3 资源不变量

与资源管理相关的不变量是最关键和最明显的用途之一。考虑一个简单的 **Handle**：

```
```cpp
template<class T> class Handle {

T * p;
public:
Handle(T* pp) :p{pp} { }
T& operator*() { return *p; }
~Handle() { delete p; }
};
```
```

想法是，你构造一个 **Handle**，给定一个使用 **new** 分配的对象指针。**Handle** 提供对指向对象的访问并最终 **delete** 该对象。例如：

```
```cpp
void f1()
{
Handle<int> h {new int{99}};
// ...
```
```

Handle 声明了一个带参数的构造函数；这会抑制默认构造函数的生成。这很好，因为默认构造函数可能会使 `Handle<T>::p` 未初始化：

```
void f2()
{
  Handle<int> h; // error : no default constructor
  // ...
}
```

没有默认构造函数使我们免于使用随机内存地址进行 `delete` 的可能性。此外，`Handle` 声明了一个析构函数：这会抑制拷贝和移动操作的生成。同样，这使我们免于一个糟糕的问题。考虑：

```
void f3() {
  Handle<int> h1 {new int{7}};
  Handle<int> h2 {h1}; // error : no copy constructor
  // ...
}
```

如果 `Handle` 有默认拷贝构造函数，`h1` 和 `h2` 都将拥有指针的拷贝，并且两者都会 `delete` 它。结果将是未定义的并且很可能灾难性的（§3.3.1）。注意：拷贝操作的生成只是被弃用，而不是被禁止，所以如果你忽略警告，你可能会让这个例子通过编译器。一般来说，如果一个类有指针成员，默认的拷贝和移动操作应被视为可疑。如果该指针成员表示所有权，逐成员拷贝是错误的。如果该指针成员不表示所有权并且逐成员拷贝是合适的，显式的 `=default` 和注释很可能是一个好主意。

如果我们想要拷贝构造，我们可以定义类似：

```
template<class T>
class Handle {
  // ...

  Handle(const T& a) :p{new T{*a.p}} { } // clone

};
```

### 17.6.3.4 部分指定的不变量

依赖于不变量但仅通过构造函数或析构函数部分表达它们的麻烦示例更少见但并非闻所未闻。考虑：

```
class Tic_tac_toe {
public:
  Tic_tac_toe(): pos(9) {} // always 9 positions
  Tic_tac_toe& operator=(const Tic_tac_toe& arg) {
```

