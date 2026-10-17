
使用变量时必须指定类型，只要初始化值可以转换为指定的类型，编译器就会执行该转换：

```cpp
cout << pi() << ' ' << pi<int>;
```

在第二次插入时，`long double` 初始化值被转换为 `int`，并显示 3。

也支持特化。例如，可以为 `char const` 类型定义 `pi` 的特化：

```cpp
template<>
constexpr char const *pi<char const> = "pi";
```

通过这种特化，我们可以执行 `cout << pi<char const>` 来显示 `pi`。

# 第 22 章 类模板

模板不仅可以为函数构造，也可以为完整的类构造。当类能够处理不同类型的数据时，可以考虑构造模板。

编译器在未显式指定类型时会尽力推导类型，并且会保持保守态度。在第一个示例中，`vector` 是 `vector<int>`，在第二个示例中是 `vector<double>`。

虽然编译器愿意并能够在许多情况下推导类型是一件好事，但它也是困惑的来源。第一个示例只使用了非负值，那么为什么不定义 `vector<unsigned>` 或 `vector<size_t>` 呢？在第二个示例中，编译器推导出 `vector<double>`，而其实完全可以使用 `vector<float>`。

为了避免困惑，根据经验，在定义类类型对象时，指定类模板的类型可能是一个好主意。这不需要花费多少精力，并且明确了你的需求和意图。因此，优选

```cpp
vector<int> vi{1, 2, 3};
vector<double> vd{1, 2.5 };
```

而不是隐式使用类型的定义。

## 22.0.1.1 Simple定义

以下是一些简单定义的示例，展示了编译器可以（以及不能）指定模板参数的情况。

起点：

```cpp
template <class ...Types      // 任意类型集
class Deduce {
    public:
        Deduce(Types ...params);           // 构造函数
        void fun();                             // 成员函数
};
```

一些定义：

```cpp
// deduce;                          完全定义:
Deduce first(1);                      // 1: int           -> Deduce<int> first(1)
Deduce second;                        Deduce<int>{ 1 }; // int    // 无 Types -> Deduce<int> second;
Deduce &&ref = Deduce                 -> Deduce<int> &&ref
```

```cpp
template <class Type>
Deduce third(static_cast<Type>(0));
```

第三个模板是一个根据为 `third` 指定类型构造 `Deduce` 对象的配方。指针的类型简单地指向指定类型的指针，因此指定的 `<int>` 意味着一个 `int*`。既然 `third` 参数的类型是适用（即 `int *`），编译器推导出 `third(0)` 是一个 `Deduce<int *>`。

这个 `Deduce<int *>` 对象，例如，可以初始化一个命名的 `Deduce<int *>` 对象：

```cpp
auto x = third<int>;               // x 的完全定义: Deduce<int *> x(0)
```

`Deduce` 的成员函数可以被匿名和命名对象使用：

```cpp
x.fun(); // OK: 命名对象调用 fun
third<int>.fun(); // OK: 匿名对象调用 fun
```

这里是一些可以编译的示例：

```cpp
extern Deduce object; // 不是对象定义
Deduce<pointer> = 0; // 可能是为了任何类型集
Deduce function(); // 同样如此
```

在定义对象时，使用函数类型或大括号定义时，模板推导的实现方式如下：

- 首先，形成所有构造函数的列表。该列表包含了所有普通构造函数和构造函数模板（即定义为成员模板的构造函数）；
- 对于该列表的每个元素，编译器都会形成一个平行的虚函数（为构造函数模板创建模板，为普通构造函数创建普通函数）；
- 这些虚函数的返回类型是构造函数的类类型，并使用原始类的模板参数。例如，对于 `Deduce` 构造函数，虚函数

```cpp
template <class ...Types>
Deduce<Types>(...params);
```

被形成。

- 接下来，将普通参数推导和重载解析应用于这组虚函数。如果这导致了最佳匹配，则使用函数的类（或特化版本）。否则，程序是格式错误的。让我们把此过程应用于 `Deduce` 类。虚函数集看起来如下：

```cpp
template <class ...Types> // 已经遇到：匹配
Deduce<Types>(...params); // Deduce(...params)
```

```cpp
template <class ...Types> // 拷贝构造函数：匹配
Deduce<Types>(... const&); // Deduce(...Types const&)
```

```cpp
template <class ...Types> // 移动构造函数，匹配
Deduce<Types>(...&&); // Deduce(...Types&&)
```

对于 `Deduce first(1)`，第一个虚函数赢得了重载，导致对类 `...Types` 的模板参数推导，从而定义了 `Deduce<int> first(1)`。注意，当模板嵌套在类下时，嵌套类模板的名字取决于外部类模板。外部类提供了。

## 22.0.1.2 显式转换

看下面的类接口：

```cpp
template <class T>
class Class {
    std::vector<T> d_data;
    struct Iterator
    {
        using type = T;
        bool operator!=(Iterator const rhs);
        Iterator operator++(int);
        type const &operator() const;
        // ...
    };
    Class();
    Class(T t);
    Class(Iterator begin, Iterator end);
    template <class Tp>
    Class(Tp first, Tp second);
    Iterator begin();
    Iterator end();
};
```

期望两个 `Class::Iterator` 参数的 `Class` 构造函数的实现与下面类似：

```cpp
template <class T>
Class<T>::Class(Iterator begin, Iterator end)
{
    while (begin != end)
        d_data.push_back(*begin);
}
```

其中 `d_data` 是一个存储 `T` 值的容器。现在可以通过一对 `Class::Iterator` 构造 `Class` 对象：

```cpp
Class<int> source;
...
Class<int> dest(source.begin(), source.end());
```

在这里，简单的模板推导过程无法推导出 `int` 模板参数。

```cpp
Class dest(source.begin(), source.end());
```

当通过传递 `Class::Iterator` 来实例化 `Class` 对象时，无法从提供的参数直接推导出使用 `Class<Iterator>::type`：类型是直接不可用的。与 `Class` 的第三个构造函数相比，

```cpp
Class intObject(12);
```

允许编译器创建一个虚函数

```cpp
template <class Type>
Class<Type> imaginary(Type)
```

在这种情况下 `Type` 显然是 `int`，因此构造了一个 `Class<int>` 对象。

当我们对 `Class(Iterator, Iterator)` 这样做时，我们得到

```cpp
template <class Iterator>
Class(Iterator, Iterator);
```

而这里 `Class` 的模板参数没有与 `Iterator` 直接关联：编译器无法推导出其类型并导致编译失败。

类似的参数也适用于第四个构造函数，它接收两个 `Tp` 参数，这两个参数都独立于 `Class` 的模板类型。在这种情况下，简单的模板参数推导失败了。尽管如此，并不是所有情况如此：显式构造，作为添加在类接口下方的显式推导规则可以使用。

显式推导规则将类模板构造函数签名连接到类模板类型。它指定了使用指定签名的构造函数构造的类模板对象的模板参数。显式推导规则的通用语法形式如下：

```
类模板构造函数签名 -> 结果类类型;
```

让我们应用于 `Class(Iterator begin, Iterator end)`。它的签名是

```cpp
template <class Iterator>
Class(Iterator begin, Iterator end)
```

要求 `Iterator` 定义了一个 `typename type`，我们现在可以表述一个类类型：

```cpp
Class<typename Iterator::type>
```

现在我们可以将两者结合在显式推导规则中（作为单独的一行添加在类接口下方）：

```cpp
template <class Iterator>
Class(Iterator begin, Iterator end) -> Class<typename Iterator::type>;
```

# 第 22 章 类模板

// 定义如下。

```cpp
struct Double
{
    // 用于下一次构造
    using type = double;
    // 成员变量 ...
};
```

```cpp
Class dest2(Double{}, Double());
    // 此处结构体 Double 定义了
    // typename double，所以
    // 定义了 Class<typename> dest2。
```

在类内部，仅引用类名时，编译器会使用类本身（在类定义之前）：当在 `Class` 内部引用 `Class` 时，编译器推导出 `Class` 为 `Class<T>`。因此，`Class` 拷贝构造函数的声明和定义头文件如下：

```cpp
Class(Class const &);    // 声明
template <class T>
// 定义
Class<T>::Class(Class const &)
{
    // ...
}
```

有时候默认类型并不是你所需要的，在这种情况下，必须显式地指定所需的类型。考虑一下如果我们为 `Class` 添加一个成员函数 `dup` 会发生什么：

```cpp
template <typename T>
template <typename Tp>
auto Class<T>::dup(Tp first, second)
{
    return Class{first, second}; // 可能不是你想要的
} //（见下文）
```

在这里，我们处于 `Class` 内部，编译器推导出必须返回 `Class<T>`。但在上一节中，我们决定当从迭代器初始化 `Class` 时，应该构造并返回 `Class<typename Tp>`。为了实现这一点，显式地指定了所需的类型：

```cpp
template <typename T>
template <typename Tp>
auto Class<T>::dup(Tp first, second)
{
    return Class<typename Tp>{first, second}; // OK：显式指定了 Class 类型。
}
```

如示例所示，不必一直使用简单的（隐式或显式）推导规则；它们用于许多标准情况，在这些情况下，显式写出类的模板似乎是多余的。语言引入模板参数推导是为了简化使用类模板时的对象构造。但归根结底你并不需要使用这些推导规则：始终可以显式地指定模板参数。

## 22.1 定义类模板

在涵盖了函数模板的构造之后，我们准备好进行下一步：构造类模板。已经存在许多实用的类模板。与其通过查看已有的类模板来演示类模板的构造，不如[下方将]另一个可能有用的新模板的构造。

新类实现了一个循环队列。循环队列具有固定数量的 `max_size` 元素。新元素插入到头部，可以访问尾部元素。循环队列只能从头部移除元素。当追加了 `n` 个元素后，下一个元素将再次插入到队列的（物理）第一个位置。循环队列允许插入，直到达到 `max_size` 个元素。只要循环队列至少包含一个元素就可以被移除；尝试从空队列移除元素或向满的循环队列添加另一个元素将导致抛出异常。除了构造构造外，循环队列必须提供一个初始化其对象的构造函数；此构造函数必须管理 `max_size` 个元素的内存，但不能调用默认构造函数（暗示了 `new` 运算符的位置）。循环队列应该提供值语义以及移动构造函数。

请注意，在上述描述中，完全没有提到循环队列使用的实际数据类型。这清楚表明我们的类完全可以定义为类模板。或者，该类可以为某些具体的数据类型定义，然后在将类转换为类模板时变为抽象类型。

类模板的实际构造将在下一节中提供，那里将开发模板 `CirQue`（循环队列）。

### 22.1.1 构造循环队列：CirQue

本节将阐述类模板的构造。在这里，我们将开发类模板 `CirQue`（循环队列）。该类有一个模板类型参数 `Data`，代表在循环队列中使用的数据类型。类模板接口的输出看起来如下：

```cpp
template<typename Data>
class CirQue
{
    // 成员声明
};
```

类模板的定义与函数模板的定义类似：

- 关键字 `template`，开始模板的定义或声明。
- `template` 后面跟着尖括号括起来列表：包含一个或多个用逗号分隔的元素的列表称为模板参数列表。模板参数列表可以有多个元素，如下：

```cpp
typename Type1, typename Type2, typename Type3
```

当类定义了多个类型时，它们在头文件中进行匹配。示例：

```cpp
template <typename Type1, typename Type2, typename Type3>
class MultiTypes
{
    ...
};
```

（等待，OCR 文本在关于第 817 页的后半部分有一些奇怪的重复和乱码。我将根据提供的片段清理逻辑流。）

新类实现了一个循环队列。循环队列具有固定数量的 `max_size` 元素。新元素插入到头部，可以访问尾部元素。循环队列只能从头部移除元素。当追加了 `n` 个元素后，下一个元素将再次插入到队列的（物理）第一个位置。循环队列允许插入，直到达到 `max_size` 个元素。只要循环队列至少包含一个元素就可以被移除；尝试从空队列移除元素或向满的循环队列添加另一个元素将导致抛出异常。除了构造构造外，循环队列必须提供一个初始化其对象的构造函数；此构造函数必须管理 `max_size` 个元素的内存，但不能调用默认构造函数（暗示了 `new` 运算符的位置）。循环队列应该提供值语义以及移动构造函数。

### 22.1.2 非类型参数

函数模板要么是类型参数要么是非类型参数。类也定义非类型参数。和函数模板一样，它们必须是整数常量。

假设我们扩展类模板的设计，使其定义第二个（非类型）参数 `size_t Size`。我们的意图是在构造函数中使用该参数定义一个具有 `Size` 个元素的数组。`CirQue` 类现在变为（仅显示相关的构造函数）：

```cpp
template <typename Data, size_t Size>
class CirQue
{
    // ... 数据成员
public:
    CirQue(Data const (&arr)[Size]);
    ...
};

template <typename Data, size_t Size>
CirQue<Data, Size>::CirQue(Data const (&arr)[Size])
{
    d_max(Size);
    d_size(0);
    d_operator(new(Size * sizeof(Data)));
    d_front(d_data);
    d_back(d_data);
    std::copy(arr, arr + Size, back_inserter(*this));
}
```

遗憾的是，这并满足我们的需求，因为非类型参数的值不会被编译器推导。当要求编译以下 `main` 函数时，它会报告模板参数数量的实际匹配：

```cpp
int main()
{
    int arr[30];
    CirQue<int> ap{ arr };
}
```
