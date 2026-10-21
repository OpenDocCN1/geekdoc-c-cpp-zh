

初始化和赋值总是使用最佳匹配来选择新的备选类型。如果类型不是完全匹配，可能会出现意外情况。

注意：不允许空 variant、包含引用成员的 variant、包含 C 风格数组成员的 variant，以及包含不完整类型（如 void）的 variant。³

不存在空状态。这意味着对于每个构造的对象，至少必须调用一个构造函数。默认构造函数会使用第一个类型的默认构造函数来初始化它：

```
std::variant<std::string, int> var;        // => var.index() == 0, value == ""
```

如果第一个类型没有定义默认构造函数，那么为 variant 调用默认构造函数将导致编译期错误：

```
struct NoDefConstr {
    NoDefConstr(int i) {
        std::cout << "NoDefConstr::NoDefConstr(int) called\n";
    }
};
```

```
std::variant<NoDefConstr, int> v1;    // ERROR: can't default construct first type
```

辅助类型 std::monostate 提供了处理这种情况的能力，也提供了模拟空状态的能力。

## std::monostate

为了支持第一个类型没有默认构造函数的 variant，C++ 标准库提供了一个特殊的辅助类型：std::monostate。std::monostate 类型的对象始终具有相同的状态。因此，它们比较起来总是相等。它们的目的就是表示一个备选类型，使 variant 不持有任何其他类型的值。

也就是说，结构体 std::monostate 可以作为第一个备选类型，使 variant 类型可以默认构造。例如：

```
std::variant<std::monostate, NoDefConstr, int> v2;    // OK
std::cout << "index: " << v2.index() << '\n';          // prints 0
```

在某种程度上，你可以将此状态解释为表示空状态的信号。⁴

有多种方法可以检查 monostate，这些方法也展示了你可以对 variant 调用的其他一些操作：

```
if (v2.index() == 0) {
    std::cout << "has monostate\n";
}
if (!v2.index()) {
    std::cout << "has monostate\n";
}
if (std::holds_alternative<std::monostate>(v2)) {
```

³ 这些特性可能会在以后添加，但对于 C++17 来说，还没有足够的经验来支持它。

⁴ 原则上，std::monostate 可以作为任何备选类型，不仅仅是第一个。然而，这个备选类型并不能帮助 variant 成为默认可构造的。

```
std::cout << "has monostate\n";
}
if (std::get_if<0>(&v2)) {
    std::cout << "has monostate\n";
}
if (std::get_if<std::monostate>(&v2)) {
    std::cout << "has monostate\n";
}
```

get_if<>() 接受一个指向 variant 的指针，如果当前备选类型是 T，则返回指向当前备选类型的指针；否则返回 nullptr。这一点与 get<T>() 不同，get<T>() 接受一个 variant 的引用，如果提供的类型正确，则按值返回当前备选类型，但在所有其他情况下会抛出异常。

和往常一样，你可以赋值另一个备选类型的值，甚至可以赋值 monostate，再次表示空状态：

```
v2 = 42;
std::cout << "index: " << v2.index() << '\n';  // index: 1

v2 = std::monostate{};
std::cout << "index: " << v2.index() << '\n';  // index: 0
```

## 从 variant 派生

你可以从 variant 派生。例如，你可以定义一个从 std::variant<> 派生的聚合类，如下所示：

```
class Derived : public std::variant<int, std::string> {
};
```

```
Derived d = {{"hello"}};
std::cout << d.index() << '\n';      // prints: 1
std::cout << std::get<1>(d) << '\n'; // prints: hello
d.emplace<0>(77);                  // initializes int, destroys string
std::cout << std::get<0>(d) << '\n'; // prints: 77
```

## 16.3 std::variant<> 类型与操作

本节详细介绍 std::variant<> 的类型和操作。

### 16.3.1 std::variant<> 的类型

在头文件 `<variant>` 中，C++ 标准库定义了类 std::variant<>，如下所示：

```
namespace std {
    template<typename Types...> class variant;
}
```

也就是说，std::variant<> 是一个可变参数类模板（这是 C++11 引入的特性，允许你处理任意数量的类型）。

此外，定义了以下类型和对象：

-   类模板 std::variant_size
-   类模板 std::variant_alternative
-   值 std::variant_npos
-   类型 std::monostate
-   异常类 std::bad_variant_access，派生自 std::exception。

Variant 还使用两个变量模板 std::in_place_type<> 和 std::in_place_index<>，它们有自己的类型 std::in_place_type_t 和 std::in_place_index_t，定义在头文件 `<utility>` 中。

### 16.3.2 std::variant<> 的操作

表 std::variant 操作列出了为 std::variant<> 提供的所有操作。

| 操作 | 效果 |
|---|---|
| constructors | 创建一个 variant 对象（可能调用底层类型的构造函数） |
| destructor | 销毁一个 variant 对象 |
| = | 赋值一个新值 |
| emplace<T>() | 销毁旧值，并将新值赋给类型为 T 的备选类型 |
| emplace<Idx>() | 销毁旧值，并将新值赋给索引为 Idx 的备选类型 |
| valueless_by_exception() | 返回 variant 是否因异常而没有值 |
| index() | 返回当前备选类型的索引 |
| swap() | 交换两个对象之间的值 |
| ==, !=, <, <=, >, >= | 比较 variant 对象 |
| hash<> | 用于计算哈希值的函数对象类型 |
| holds_alternative<T>() | 返回是否存在类型为 T 的值 |
| get<T>() | 返回类型为 T 的备选类型的值 |
| get<Idx>() | 返回索引为 Idx 的备选类型的值 |
| get_if<T>() | 返回指向类型为 T 的备选类型值的指针，或返回 nullptr |
| get_if<Idx>() | 返回指向索引为 Idx 的备选类型值的指针，或返回 nullptr |
| visit() | 对当前备选类型执行操作 |

表 16.1. std::variant<> 的操作

## 构造

默认情况下，variant 的默认构造函数会调用第一个备选类型的默认构造函数：

```
std::variant<int, int, std::string> v1;  // sets first int to 0, index()=0
```

备选类型会被值初始化，这意味着对于基础类型，它是 0、false 或 nullptr。

如果传入一个值用于初始化，将使用最佳匹配的类型：

```
std::variant<long, int> v2{42};
std::cout << v2.index() << '\n';  // prints 1
```

然而，如果两个类型匹配程度相同，调用将产生歧义：

```
std::variant<long, long> v3{42};          // ERROR: ambiguous
std::variant<int, float> v4{42.3};        // ERROR: ambiguous
std::variant<int, double> v5{42.3};       // OK
std::variant<int, long double> v6{42.3};  // ERROR: ambiguous
```

```
std::variant<std::string, std::string_view> v7{"hello"}; // ERROR: ambiguous
std::variant<std::string, std::string_view, const char*> v8{"hello"}; // OK
std::cout << v8.index() << '\n';  // prints 2
```

若要传递一个以上的值进行初始化，必须使用 in_place_type 或 in_place_index 标签：

```
std::variant<std::complex<double>> v9{3.0, 4.0};      // ERROR
std::variant<std::complex<double>> v10{{3.0, 4.0}};  // ERROR
std::variant<std::complex<double>> v11{std::in_place_type<std::complex<double>>, 3.0, 4.0};
std::variant<std::complex<double>> v12{std::in_place_index<0>, 3.0, 4.0};
```

你也可以使用 in_place_index 标签来解决初始化过程中的歧义或覆盖优先级：

```
std::variant<int, int> v13{std::in_place_index<1>, 77};  // init 2nd int
std::variant<int, long> v14{std::in_place_index<1>, 77};  // init long, not int
std::cout << v14.index() << '\n';  // prints 1
```

你甚至可以传递一个初始化器列表，后面跟随额外的参数：

```
// initialize variant with a set with lambda as sorting criterion:
auto sc = [] (int x, int y) {
    return std::abs(x) < std::abs(y);
};
std::variant<std::vector<int>, std::set<int,decltype(sc)>> v15{std::in_place_index<1>, {4, 8, -7, -2, 0, 5}, sc};
```

然而，这仅在所有初始值完全匹配容器的元素类型时才能工作。否则，你必须显式传递一个 std::initializer_list<>：

```
// initialize variant with a set with lambda as sorting criterion:
```

