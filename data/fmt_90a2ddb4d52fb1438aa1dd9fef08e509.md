
`requires(Iter p, int i) { p[i]; }` 表达式是一个谓词，如果其中的语句是有效代码，则为真，否则为假。我将要求-表达式视为泛型编程的汇编代码。像普通的汇编代码一样，`requires` 表达式极其灵活，可以进行灵活的编程。以某种形式，它们位于大多数有趣的泛型代码的底层，就像汇编代码是大多数有趣的普通代码的底层。像汇编代码一样，`requires` 表达式不应该出现在普通代码中。它们属于实现抽象。如果你在代码中使用 `requires`，它的级别太低，并且会变成问题。在 `advance()` 中使用 `requires` 是故意低效且拙劣的。注意“忘记”指定 `+=` 和操作所需的类型。`advance()` 的某些版本会通过检查但仍然无法编译。你已经收到警告了！正确的随机访问版本 `advance(iter)` 更简单且更具读性：

```cpp
template<random_access_iterator Iter>
void advance(Iter p, int n) // 将 p 向移动 n 个元素
{
    p+=n; // 随机访问迭代器具有 +=
}
```

## 8.2.4 概念（Concepts）的定义

我们在库中发现非常有用的概念，例如 `forward_iterator`，包括标准库 (§14.5)。对于类和函数，通常使用良好库中的概念来编写新概念会更容易一些，但简单的概念并不难定义。标准库中的名称（如 `random_access_iterator` 和 `vector`）都是全小写的。在这里，我遵循约定，将自己定义的概念名称的首字母大写，例如 `Sequence` 和 `Vector`。

概念是一个模板-谓词，规定了一个或多个类型如何被使用。首先考虑最简单的例子之一：

```cpp
template<typename T>
concept Equality_comparable =
requires (T a, T b) {
    { a == b } -> Boolean; // 使用 == 比较 Ts
    { a != b } -> Boolean; // 使用 != 比较 Ts
};
```

## 108 概念与泛型编程 第 8 章

`Equality_comparable` 是我们用来确保可以比较一种类型的值是否相等且不等的概念。我们简单地说，当该类型的两个值时，它们必须可以使用 `==` 和 `!=` 进行比较，这些操作的结果必须是 `Boolean`。例如：

```cpp
static_assert(Equality_comparable<int>); // 成功
```

```cpp
struct S { int a; }
static_assert(Equality_comparable<S>); // 失败，因为结构体不会自动获得 == 和 !=
```

`Equality_comparable` 概念的定义与英语描述完全等价，不再如此。概念的值始终是 `bool`。

赋值给 `->` 的 `{ }` 块的结果不是标准库的布尔类型，因此我在 (§14.5) 中定义了。`Boolean` 仅意味着一个类型可以作为条件。

定义 `Equality_comparable` 来处理非同构比较几乎一样：

```cpp
template<typename T1, typename T2>
concept Equality_comparable =
requires(T1 a, T2 b) {
  (a == b) -> Boolean; // 与 T2 比较 a，使用 ==
  (a != b) -> Boolean; // 与 T2 比较 a，使用 !=
  (b == a) -> Boolean; // 与 T1 比较 b，使用 ==
  (b != a) -> Boolean; // 与 T1 比较 b，使用 !=
};
```

`typename T2 = T` 确保确保如果我们不指定第二个参数，`T2` 将与 `T` 相同；`T` 是默认模板参数。

我们可以这样测试 `Equality_comparable`：

```cpp
static_assert(Equality_comparable<int,double>); // 成功
static_assert(Equality_comparable<int,int>); // 成功（T2 默认为 int）
static_assert(Equality_comparable<int,string>); // 失败
```

这个 `Equality_comparable` 几乎与标准库中的 `equality_comparable` (§14.5) 相同。我们可以定义一个允许算术返回布尔的概念。首先我们需要定义 `Number`：

```cpp
template<typename T, typename U = T>
concept Number =
requires(T x, U y) { // 带有算术运算的类型
  x+y=x; x-y=x; x*=y; x/=y;
  x+=y; -==y; *==y; /==y;
  x=x; // 拷贝
  x=0;
};
```

这没有对结果类型做任何假设，但对于简单用法足够了。给定两个参数类型，`Number<X,Y>` 检查 `X` 是否具有 `Number` 的属性。给定两个参数，`Number<X,Y>` 检查两个类型是否可以配合所需的操作使用。从这里，我们可以定义 `Arithmetic` 概念 (§8.2.1)：

## 8.2.4 概念的定义 109

```cpp
template<typename T, typename U = T>
concept Arithmetic = Number<T,U> && Number<U,T>;
```

对于更复杂的例子，考虑一个序列：

```cpp
template<typename S> {
    concept Sequence = requires (S a) {
        typename range_value_t<S>;
        typename iterator_t<S>;

        { a.begin() } -> same_as<iterator<S>>;
        { a.end() } -> same_as<iterator<S>>;
    }

    requires input_iterator<iterator_t<S>>;
    requires same_as<range_value_t<S>, iter_value_t<S>>;
}
```

为了使 `S` 成为一个 `Sequence`，它必须提供一个值类型（元素类型）；§13.1 以及一个迭代器类型（其迭代器的类型）。最好使用来自现有库的集合。对于任何集合，请参见 §14.5。在 `range_value_t<S>` 和 `iterator_t<S>` (§16.4) 中表示这一点。还必须存在 `begin()` 和 `end()` 函数并返回 `S` 的迭代器，这符合标准库容器的惯例 (§12.3)。最后，还必须存在 `begin()` 和 `end()` 函数。

## 8.2.5节 概念与 auto 111

```cpp
auto twice(Arithmetic x) { return x+x; } // 仅针对数字
auto thrice(auto x) { return x+x+x; } // 适用于任何支持 + 的类型
auto x1 = twice(7); // OK x1==14
string s = "Hello";
auto x2 = twice(s); // 错误：string 不是 Arithmetic
auto x3 = thrice(s); // OK x3="Hello Hello"
```

除了用于约束函数参数外，还可以约束变量的初始化：

```cpp
auto ch1 = open_channel("foo"); // 无论 open_channel() 返回什么类型都有效
Arithmetic ch2 = open_channel("foo"); // 错误：channel 不是 Arithmetic
Channel ch3 = open_channel("foo"); // OK：open_channel() 是一个合适的概念
// 且该类型由 channel() 返回
```

这对于防止过度使用 `auto` 以及使用泛型函数来记录需求非常有用。

为了可读性和调试，尽可能在接近源头的地方捕获类型错误是非常重要的。约束返回类型会有帮助：

```cpp
Number auto some_function(int x)
{
// ...
return fct(x); // 除非 fct(x) 返回 Number，否则会报错
// ...
}
```

自然地，我们可以通过引入局部变量来实现这一点：

```cpp
auto some_function(int x)
{
// ...
Number auto y = fct(x); // 除非 fct(x) 返回 Number，否则会报错
return y;
// ...
}
```

然而，这有点冗长，而且并不是所有类型都可以廉价地复制。

## 8.2.6节 概念与类型

类型（Type）

- 指定了可以应用于对象的（隐式和显式的）操作集

- 依赖于函数声明和语言规则

- 指定了对象在内存中的布局方式

单参数概念（Single-argument concept）

- 指定了可以应用于对象的（隐式和显式的）操作集

- 依赖反映函数声明和语言规则的使用模式

- 对对象的布局一无未字

- 允许使用一组类型

因此，使用概念约束比使用类型约束更具灵活性。此外，概念可以定义多个参数之间的关系。我的理想是，最终大多数函数将定义为模板函数，其参数由概念约束。遗憾的是，目前对这种方式的支持并不完美：我们必须将概念当作形容词而非名词。例如：

```cpp
void sort(Sortable&); // 需要 'auto'
void sort(Sortable&); // 错误：概念名后需要 'auto'
```

## 8.3节 泛型编程

C++ 直接支持的泛型编程形式核心思想是从具体的、高效算法中抽象，以获得泛型算法，这些算法可以与不同的数据表示相结合，产生各种软件 [Stepanov, 2009]。这些代表基本操作和数据结构的抽象被称为概念。

### 8.3.1节 概念的使用

很好，概念是基础性的，它们更多是被发现而非设计出来的。例子有整数和浮点数（如 Classic C [Kernighan,1977] 定义）、序列以及更通用的数学概念，如环和向量空间。它们代表了某个应用领域的基础概念。这就是为什么它们被称为“概念（concepts）”。在有效泛型编程所需的程度内识别并形式化概念可能是一个挑战。对于基础使用，可以考虑概念 `regular` (§14.5)。当一个类型的行为像一个 `int` 或 `vector` 时，它就是 regular 的。regular 类型的对象

- 可以被销毁

- 可以通过构造函数或赋值进行复制（使用通常的拷贝语义，产生独立且相等的对象）

- 可以使用 `==` 和 `!=` 进行比较

- 不会因为过度巧妙的编程技巧而产生技术问题。

`string` 是 regular 类型另一个例子。像 `int` 一样，`string` 也是全序的 (§14.5)。也就是说，两个字符串可以使用带有适当语义的 `<`、`、>= 和 `==` 进行比较。

概念不仅仅是一种语法符号，它从根本上关乎语义。例如，不要定义 `+` 为除法；那将匹配任何合理数字的需求。遗憾的是，我们没有表达语义的语言支持，我们必须依赖专家知识和直觉来生成具有语义意义的概念。不要定义语义上无意义的概念，例如 `Addable` 和 `Subtractable`。相反，应依赖领域知识来定义与应用领域中基础概念匹配的概念。

### 8.3.2节 使用模板抽象

良好的抽象是从具体示例中仔细生长出来的。尝试通过为每种可能的需求和技术做准备来“抽象”并不是好主意；那种方向会导致优雅和代码臃肿。相反，应该从一个（最好是多个）真实使用的具体示例开始，并尝试消除非要细节。考虑：

```cpp
double sum(const vector<int>& v)
{
  double res = 0;
  for (auto x : v) {
    res += x;
  }
  return res;
}
```

这显然是计算序列和的方法之一。考虑什么让这段代码没有它需要的那么通用：

- 为什么只是 `ints`？

- 为什么只是 `vectors`？

- 为什么在 `double` 中累加？

- 为什么从 0 开始？

- 为什么？

通过将具体类型变为模板参数来回答第一个问题，我们得到了简单的形式：

```cpp
template<typename Iter, Arithmetic Val>
Val accumulate(Iter first, Iter last, Val res)
{
  for (auto p = first; p!=last; ++p) {
    res += p;
  }
  return res;
}
```

在这里，我们：

- 要遍历的数据结构是一个序列简体13.1)。

- 累加器的类型已变为参数。

- 累加器的类型必须是 arithmetic。

- range 是一个具有 `begin()` 和 `end()` 的标准库概念简体13.1)。为了完全的通用，我们也可以接受 `+=` 操作；17.3。

迭代器版本和范围版本的 `accumulate()` 都有用：迭代器版本用于通用性，范围版本用于易用性。

```cpp
template<forward range R, Arithmetic value_type<T>>
Val accumulate(const R& r, Val res = 0)
{
  for (auto x : r) {
    res += x;
  }
  return res;
}
```

从具体代码（最好是多个）中泛化并保持性能的过程被称为“提升（lifting）”。相反，开发模板的最佳方法通常是：

- 首先，编写一个具体版本

- 然后进行调试、测试和测量

- 最后，将具体类型替换为模板参数

## 8.4节 变长模板

模板可以定义为接受任意数量的任意类型。这种模板被称为变长模板。考虑一个输出具有 `<<` 运算符的任意类型值的简单函数：

```cpp
template<typename T>
concept Printable = requires(T t) { std::cout << t; } // 仅一个操作！
```

```cpp
void print()
{
  // 对于没有参数的情况：什么都不做
}
```

```cpp
template<Printable T, Printable... Tail...>
void print(T head, Tail... tail)
{
  std::cout << head << ' '; // 首先，对 head 执行
  print(tail...); // 然后，对 tail 执行
}
```

`Printable...` 表示 `Tail` 是一个类型序列。`Tail...` 表示 `tail` 是一个值序列。

# 第 8.4 节 变参数模板 115

Tail 中类型的值。使用 `...` 声明的参数称为参数包。在这里，`tail` 是一个（函数）参数包，其元素类型在模板（参数）参数包 `Tail` 中找到。因此，`print()` 可以接受任意数量、任意类型的参数。

`print()` 的调用将参数分为头部（第一个）和尾部（其余部分）。打印头部，然后对尾部调用 `print()`。最终，`tail` 将变为空，因此我们需要一个处理零参数的情况，我们可以通过消除 `print()` 来处理。如果我们不想允许零参数情况，可以使用编译时 `if` 来消除 `print()`：

```cpp
template<Printable T, Printable... Tail>
void print(T head, Tail... tail)
{
    cout << head << ' ';
    if constexpr(sizeof(tail) > 0)
        print(tail);
}
```

我使用了 `if (7.4.3)` 示例，而不是普通的运行时 `if`，以避免生成最后的 `print()` 调用。鉴于此，不需要定义 `""` 打印函数。

变参数模板的强大在于它们可以接受我们给出的任何参数。缺点包括：

- 递归实现可能很难正确编写。

- 接口的类型检查可能是复杂的模板程序。

- 类型检查是临时的（ad hoc），而不是在标准中定义的。

- 递归实现在编译时间和内存需求上可能异常地昂贵。

由于其灵活性，变参数模板在标准库中被广泛使用，有时会被广泛重载。

### 8.4.1 折叠表达式

为了简化简单变参数模板的实现，C++ 提供了对参数包元素进行有限形式迭代的方法。例如：

```cpp
template<Number... T>
int sum(T... v)
{
    return (v + ... + 0);
}
```

`sum()` 可以接受任意数量、任意类型的参数：

```cpp
int x = sum(1, 2, 3, 4, 5); // x 变为 15
int y = sum('a', 2.4, x); // y 变为 11 (2.4 被截断，'a' 的值为 97)
```

`sum()` 的主体使用了一个表达式：

```cpp
return (v + ... + 0); // 将 v 的所有元素加到 0
```

在这里，`(v+...+0)` 意味着从初始值 0 开始加上 v 的所有元素。第一个被加的元素是“最右侧的”（索引最高的）：`(v[0]+v[1]+v[2]+v[3]+v[4]))`。

# 概念与泛型编程

# 第 8 章

现在，从 0 所在的右侧开始。这被称为右折叠（right fold）。或者，我们可以使用左折叠：
