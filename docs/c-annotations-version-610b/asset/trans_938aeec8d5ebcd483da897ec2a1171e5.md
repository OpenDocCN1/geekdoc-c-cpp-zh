

```cpp
{
    d_data.push_back(
        d_isPolymorphic ?
            obj.clone()
        :
            new Type(obj)
    );
}
```

其意图是：如果 `Type` 是多态类，则使用类 `Type` 的 `clone` 成员函数；如果 `Type` 是值类，则使用标准拷贝构造函数。

遗憾的是，该方案通常会失败，因为值类不定义 `clone` 成员函数，而多态基类应删除其拷贝构造函数（参见第 7.5 节）。编译器并不关心值类从不会调用 `clone`，也不关心拷贝构造函数只在值类中可用而在多态类中不可用。它只是有一些代码需要编译，而由于缺少成员，它无法完成编译。就这么简单。

### 22.2.2.1 定义重载成员

模板元编程可以解决这个问题。我们知道类模板成员函数只有在被使用时才会实例化，因此我们的计划是设计重载的 `add` 成员函数，其中只有一个会被调用（并因此被实例化）。我们的选择将基于一个额外的（除 `Type` 本身之外的）模板非类型参数，该参数指示我们将把 `Storage` 用于多态类还是非多态类。我们的 `Storage` 类开头如下：

```cpp
template <typename Type, bool isPolymorphic>
class Storage
```

最初定义了两个重载版本的 `add` 成员：一个用于存储多态对象的 `Storage` 对象（使用 `true` 作为其模板非类型实参），另一个用于存储值类对象（使用 `false` 作为其模板非类型实参）。

不幸的是，我们遇到了一个小问题：函数不能根据实参值重载，只能根据实参类型重载。但这个小问题可以解决。认识到类型是由模板名称及其模板实参的组合定义的，我们可以利用第 22.2.1.1 节中关于如何将整数值转换为类型的知识，将值 `true` 和 `false` 转换为类型。

我们将提供一个（私有）`add` 成员，带有一个 `IntType<true>` 参数（实现多态类），以及另一个（私有）`add` 成员，带有一个 `IntType<false>` 参数（实现非多态类）。

除了这两个私有成员之外，还定义第三个（公有）成员 `add`，它通过提供一个由 `Storage` 的模板非类型参数构造的 `IntType` 实参，来调用适当的私有 `add` 成员。

以下是三个 `add` 成员的实现：

```cpp
// declared in Storage’s private section:

template <typename Type, bool isPolymorphic>
void Storage<Type, isPolymorphic>::add(Type const &obj, IntType<true>)
{
    d_data.push_back(obj.clone());
}

template <typename Type, bool isPolymorphic>
void Storage<Type, isPolymorphic>::add(Type const &obj, IntType<false>)
{
    d_data.push_back(new Type(obj));
}

// declared in Storage’s public section:

template <typename Type, bool isPolymorphic>
void Storage<Type, isPolymorphic>::add(Type const &obj)
{
    add(obj, IntType<isPolymorphic>());
}
```

相应的 `add` 成员会被实例化并调用，因为基本值可以转换为类型。因此，每个可能的模板非类型值都被用来定义重载的类模板成员函数。

由于类模板成员只有在使用时才会被实例化，所以重载的私有 `add` 成员中只有一个会被实例化。由于另一个从不会被调用（因此也从不被实例化），所以可以避免编译错误。

### 22.2.2.2 类结构作为模板参数的函数

一些软件工程师在考虑使用指针来存储值类对象副本的 `Storage` 类时有所保留。他们的论点是，值类对象完全可以按值存储，而不是按指针存储。他们更愿意按值存储值类对象，而按指针存储多态类对象。

这种区分在模板元编程中经常出现，下面的 `struct IfElse` 可用于根据一个 bool 选择值来获得两种类型之一。

首先定义该模板的*泛型形式*：

```cpp
template<bool selector, typename FirstType, typename SecondType>
struct IfElse
{
    typedef FirstType type;
};
```

然后定义一个偏特化。该特化表示一个特定的选择值（例如 `false`），并让其余类型保持开放以便进一步指定：

```cpp
template<typename FirstType, typename SecondType>
struct IfElse<false, FirstType, SecondType>
{
    typedef SecondType type;
};
```

前一个（泛型）定义将 `FirstType` 与 `IfElse::type` 类型定义关联起来，后一个定义（针对逻辑值 `false` 进行偏特化）将 `SecondType` 与 `IfElse::type` 类型定义关联起来。

`IfElse` 模板允许我们定义其数据组织取决于模板参数的类模板。使用 `IfElse`，`Storage` 类可以定义指针来存储多态类类型对象的副本，并定义*值*来存储值类类型对象：

```cpp
template <typename Type, bool isPolymorphic>
class Storage
{
    typedef typename IfElse<isPolymorphic, Type *, Type>::type
        DataType;

    std::vector<DataType> d_data;

private:
    void add(Type const &obj, IntType<true>);
    void add(Type const &obj, IntType<false>);
public:
    void add(Type const &obj);
};

template <typename Type, bool isPolymorphic>
void Storage<Type, isPolymorphic>::add(Type const &obj, IntType<true>)
{
    d_data.push_back(obj.clone());
}

template <typename Type, bool isPolymorphic>
void Storage<Type, isPolymorphic>::add(Type const &obj, IntType<false>)
{
    d_data.push_back(obj);
}

template <typename Type, bool isPolymorphic>
void Storage<Type, isPolymorphic>::add(Type const &obj)
{
    add(obj, IntType<isPolymorphic>());
}
```

上述示例使用 IfElse 的 type，IfElse 将其定义为 FirstType 或 SecondType。IfElse 的 type 定义了用于 Storage 的 vector 数据类型的实际数据类型。

这个例子中值得注意的结果是，Storage 类的*数据组织*现在取决于其模板实参。由于 `isPolymorphic == true` 情形使用与 `isPolymorphic == false` 情形不同的数据类型，重载的私有 `add` 成员可以立即利用这一差异。例如，`add(Type const &obj, IntType<false>)` 使用直接拷贝构造将 `obj` 的副本存储到 `d_data` 中。

也可以从多个类型中进行选择，因为 IfElse 结构体可以嵌套。要认识到，使用 IfElse 从不会对最终可执行程序的大小或执行时间产生任何影响。最终程序只包含适当的类型，该类型取决于最终选择的类型。

### 22.2.2.3 一个说明性示例

下一个示例将 `MapType` 定义为一种 map，其键类型或值类型可以是普通类型或指针，它说明了这种方法：

```cpp
template <typename Key, typename Value, int selector>
class Storage
{
    typedef typename IfElse<
                    selector == 1,              // if selector == 1:
                    map<Key, Value>,            // use map<Key, Value>

                    typename IfElse<
```

## 22.3 用户定义字面量（C++11，4.7）

除了第 11.12 节讨论的字面量运算符之外，C++11 标准还提供了一种函数模板字面量运算符，匹配以下原型：

```cpp
template <char ...Chars>
Type operator "" _identifier()
```

这个可变参数非类型参数函数模板不定义参数，而只是一个可变参数非类型参数列表。

它的实参必须是一个 int 常量，定义 unsigned long long int 参数的字面量运算符也期望如此。该 int 常量的所有字符都作为单独的 char 非类型模板实参传递给该字面量运算符。

例如，如果 `_NM2km` 是一个字面量运算符函数模板，则可以像 `80_NM2km` 这样调用它。随后该函数模板实际上会以 `_NM2km<'8', '0'>()` 的形式被调用。如果这个函数模板只使用模板元编程技术并且只处理整数数据，那么它的操作可以完全在编译期执行。为说明这一点，我们假设 NM2km 只处理并返回无符号值。

函数模板 `_NM2km` 可以将其实参转发给一个类模板，后者定义一个枚举常量值，并执行所需的计算。以下是可变参数字面量运算符函数模板 `_NM2km` 的实现：

```cpp
size_t constexpr operator "" _NM2km()
{
    return static_cast<size_t>(          // forward Chars to NM2km
           NM2km<0, Chars ...>::value * 1.852);
}
```

类模板 NM2km 定义了三个非类型参数：acc 累加值，c 是可变参数非类型参数中的第一个字符，而 `...Chars` 表示剩余的非类型参数，它们包含在一个非类型参数包中。由于在每次递归调用中，c 都是来自原始非类型参数包的下一个字符，因此将当前值乘以 10 再加上下一个字符的值，作为下一次累加值连同由 `Chars ...` 表示的参数包剩余元素一起传递给其递归调用：

```cpp
template <size_t acc, char c, char ...Chars>
struct NM2km
{
    enum
    {
        value = NM2km<10 * acc + c - '0', Chars ...>::value
    };
};
```

最终，参数包为空。对于这种情况，有一个 NM2km 的偏特化可用：

```cpp
template <size_t acc, char c>   // empty parameter pack
struct NM2km<acc, c>
{
    enum
    {
        value = 10 * acc + c - '0'
    };
};
```

