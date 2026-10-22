
对于 R = void 的情况，模板是适用的，但这无法通过重载来实现。

-   对非重载函数有效的代码，在函数被重载后可能不再有效。具体来说，给定两个函数模板 f(T) 和 g(T)（其中 T 是模板参数），表达式 `g(&f<int>)` 仅在 f 未被重载时有效（否则，无法确定指的是哪个 f）。

-   友元声明指向特定的函数模板或特定函数模板的实例化。函数模板的重载版本不会自动获得原模板所拥有的特权。

综上所述，这些理由有力地支持为函数模板引入偏特化机制。

对函数模板进行偏特化的一种自然语法是类模板记法的推广：

```
template<typename T>
T const& max (T const&, T const&); // 主模板

template<typename T>
T* const& max <T*>(T* const&, T* const&); // 偏特化
```

一些语言设计者担心这种偏特化方法与函数模板重载之间的交互。例如：

```
template<typename T>
void add (T& x, int i); // 主模板

template<typename T1, typename T2>
void add (T1 a, T2 b); // 另一个（重载的）主模板

template<typename T>
void add<T*> (T*&, int); // 这特化的是哪个主模板？
```

然而，我们预计这类情况会被视为错误，而不会对该特性的实用性产生重大影响。

在 C++11 标准化期间曾简要讨论过这一扩展，但最终并未引起太多关注。尽管如此，这个话题偶尔仍会出现，因为它能巧妙地解决一些常见的编程问题。也许在未来的某个 C++ 标准版本中，它会再次被提上议程。

## 17.4 命名模板实参

第 512 页的 21.4 节描述了一种技术，允许我们为特定参数提供非默认模板实参，而无需指定其他已有默认值的模板实参。虽然这是一项有趣的技术，但显然它为相对简单的效果付出了相当多的努力。因此，提供一种语言机制来命名模板实参是很自然的想法。

我们应当指出，类似的扩展（有时称为*关键字实参*）早先在 C++ 标准化过程中由 Roland Hartinger 提出（参见 [*StroustrupDnE*] 的 6.5.1 节）。尽管技术上可行，但该提案最终因各种原因未被语言采纳。目前没有理由相信命名模板实参将来会被纳入语言，但这一话题在委员会讨论中经常出现。

然而，为了完整性，我们提及一个已被讨论过的语法构想：

```
template<typename T,
typename Move = defaultMove<T>,
typename Copy = defaultCopy<T>,
typename Swap = defaultSwap<T>,
typename Init = defaultInit<T>,
typename Kill = defaultKill<T>>
class Mutator {
…
};

void test(MatrixList ml)
{
mySort (ml, Mutator <Matrix, .Swap = matrixSwap>);
}
```

这里，实参名称前的句点用于表示我们按名称引用模板实参。这种语法类似于 1999 年 C 标准中引入的“指定初始化器”语法：

```
struct Rectangle { int top, left, width, height; };
struct Rectangle r = { .width = 10, .height = 10, .top = 0, .left = 0 };
```

当然，引入命名模板实参意味着模板的模板参数名称现在成为该模板公共接口的一部分，不能随意更改。这可以通过更显式的、选择加入的语法来解决，例如：

```
template<typename T,
Move: typename M = defaultMove<T>,
Copy: typename C = defaultCopy<T>,
Swap: typename S = defaultSwap<T>,
Init: typename I = defaultInit<T>,
Kill: typename K = defaultKill<T>>
class Mutator {
...
};

void test(MatrixList ml)
{
  mySort (ml, Mutator <Matrix, .Swap = matrixSwap>);
}
```

## 17.5 重载类模板

完全可以想象类模板可以在其模板参数上进行重载。例如，可以设想创建一个 `Array` 模板家族，同时包含动态大小和静态大小的数组：

```
template<typename T>
class Array {
// 动态大小数组
...
};

template<typename T, unsigned Size>
class Array {
// 固定大小数组
...
};
```

重载不一定局限于模板参数的数目；参数的*种类*也可以变化：

```
template<typename T1, typename T2>
class Pair {
// 字段对
...
};

template<int I1, int I2>
class Pair {
// 常量整数值对
...
};
```

尽管一些语言设计者已经非正式地讨论过这个想法，但它尚未正式提交给 C++ 标准化委员会。

## 17.6 非末尾包展开的推导

包展开的模板实参推导仅在包展开出现在参数或实参列表末尾时才有效。这意味着，虽然从列表中提取第一个元素相当简单：

```
template<typename... Types>
struct Front;

template<typename FrontT, typename... Types>
struct Front<FrontT, Types...> {
using Type = FrontT;
};
```

但由于第 347 页 16.4 节所述的对偏特化的限制，人们无法轻易提取列表的最后一个元素：

```
template<typename... Types>
struct Back;

template<typename BackT, typename... Types>
struct Back<Types..., BackT> { //错误：包展开不在
using Type = BackT; // 模板实参列表末尾
};
```

变参函数模板的模板实参推导也受到类似限制。放宽关于包展开和偏特化的模板实参推导规则，允许包展开出现在模板实参列表中的任意位置，从而使这类操作变得简单得多，这是合理的。此外，有可能——尽管可能性较小——推导允许在同一参数列表中出现多个包展开：

```
template<typename... Types> class Tuple {
};

template<typename T, typename... Types>
struct Split;

template<typename T, typename... Before, typename... After>
struct Split<T, Before..., T, After...> {
```

## 17.8 模板的类型检查

使用模板进行编程的许多复杂性源于编译器无法在本地检查模板定义是否正确。相反，模板的大部分检查发生在模板实例化期间，此时模板定义上下文和模板实例化上下文交织在一起。这种不同上下文的混合使得难以确定责任归属：是模板定义有错，因为它错误地使用了模板参数；还是模板用户有错，因为提供的模板参数不满足模板的要求？这个问题可以用一个简单的例子来说明，我们附上了典型编译器产生的诊断信息：

```
template<typename T>
T max(T a, T b)
{
return b < a ? a : b;
// 错误：“没有匹配 operator <
// （运算符类型为 ‘X’ 和 ‘X’）”
}

struct X {
};
bool operator> (X, X);

int main()
{
X a, b;
X m = max(a, b); // 注意：“在函数模板特化
// ‘max<X>’ 的实例化中请求此处”
}
```

注意，实际错误（缺少合适的 operator<）是在函数模板 max() 的定义内部检测到的。这可能确实是错误——也许 max() 应该使用 operator> ？然而，编译器还提供了一条注释，指向导致 max<X> 实例化的位置，这可能才是真正的错误——也许 max() 的文档要求使用 operator< ？无法回答这个问题正是导致第 143 页 9.4 节所描述的“错误小说”的原因，即编译器提供了从实例化的最初原因到检测到错误的实际模板定义的完整模板实例化历史。然后，程序员需要确定哪个模板定义（或者可能是模板的最初使用）实际上是有错的。

