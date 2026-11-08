
### 访问私有属性

```cpp
class X {
public:
    void f(int n)
        [[ expects: n < m ]] // error; m is private
    {
        [[ assert: n < m ]]; // OK
        // ...
    }
private:
    int m;
};
```

属性 m 是私有的，因此不能作为前置条件的一部分。默认情况下，违反契约会终止程序。

你可以调整这些属性的行为。

### 8.2.1.1 微调属性

适配属性的语法相当精细：`[[contract-attribute modifier: conditional-expression]]`

- contract-attribute：expects、ensures 和 assert
- modifier：指定契约级别或契约的执行；可能的值是 default、audit 和 axiom
  - default：运行时检查的成本应该很小；它是默认修饰符
  - audit：假定运行时检查的成本很大
  - axiom：谓词在运行时不检查
- conditional-expression：契约的谓词

对于 ensures 属性，还额外有一个可用的标识符：`[[ensures modifier identifier: conditional-expression]]`

该标识符让你可以引用函数的返回值。

### 访问返回值

```cpp
int mul(int x, int y)
    [[expects: x > 0]]        // implicit default
    [[expects default: y > 0]]
    [[ensures audit res: res > 0]] {
    return x * y;
}
```

res 作为标识符是一个任意名称。如示例所示，你可以使用更多同类的契约。

下面让我更深入地探讨契约违规的处理。

### 8.2.1.2 处理契约违规

一次编译有三个断言构建级别：

- off：不检查任何契约
- default：检查默认契约；这是默认值
- audit：检查默认契约和审计契约

当谓词返回 false 而发生契约违规时，会调用违规处理程序。违规处理程序会获得一个类型为 `std::contract_violation` 的值。该值提供有关契约违规的详细信息。

### 类 contract_violation

```cpp
namespace std {
    class contract_violation {
    public:
        uint_least32_t line_number() const noexcept;
        string_view file_name() const noexcept;
        string_view function_name() const noexcept;
        string_view comment() const noexcept;
        string_view assertion_level() const noexcept;
    };
}
```

- line_number：契约违规的行号
- file_name：契约违规的文件名
- function_name：契约违规的函数名
- comment：契约的谓词
- assertion_level：契约的断言级别

## 8.2.2 反射

反射是程序分析和修改自身的能力。反射发生在编译期，因此遵循 C++ 元规则：“不为你不使用的东西付出代价”。[类型特征库] 是用于反射的强大工具，但关于静态反射的提案 P0385 走得更远。

以下代码片段应能让你初步了解反射：

### 反射运算符

```cpp
template <typename T>
T min(const T& a, const T& b) {
  log() << "function: min"
        << get_base_name_v<get_aliased_t<$reflect(T)>>
        << "("
        << get_base_name_v<$reflect(a)> << ": "
        << get_base_name_v<get_aliased_t<get_type_t<$reflect(a)>>>
        << ", " << get_base_name_v<$reflect(b)> << ": "
        << get_base_name_v<get_aliased_t<get_type_t<$reflect(b)>>>
        << " = " << a << ", "
        << ")" << '\n';
  return a < b ? a : b;
}
```

新的反射运算符 `$reflect` 是该示例中的关键表达式。首先，这个新运算符会创建一种特殊的数据类型，它提供关于模板参数 T（第 4 行）以及值 a（第 6 行）和 b（第 9 行）的元信息。得益于函数组合，这些元信息可用于提供更多信息：`get_base_name_v<get_aliased_t<...`（第 7 行和第 10 行）。

当你以参数 min(12.34, 23.45) 调用函数 min 时，会得到以下输出：

```text
function: min<double>(a: double = 12.34, b: double = 23.45)

Calling min(12.34, 23.45)
```

你可能好奇并想知道：通过反射可以获得哪些元信息？以下几点给出了答案：

- 对象：源代码的行号和列号以及文件名
- 类：私有和公有数据成员以及成员函数
- 别名：解析后的别名名称

P0385 提案中的下一个示例展示了反射如何帮助确定类的私有和公有成员。

[26] https://en.cppreference.com/w/cpp/header/type_traits
[27] http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2017/p0385r2.pdf

### 确定类 foo 的公有和私有成员

```cpp
#include <reflect>
#include <iostream>

struct foo {
private:
    int _i, _j;
public:
    static constexpr const bool b = true;
    float x, y, z;
private:
    static double d;
};

template <typename ... T>
void eat(T ... ) { }

template <typename MetaObjects, std::size_t I>
int do_print_data_member(void) {
    using namespace std;
    typedef reflect::get_element_t<MetaObjects, I> metaobj;
    cout << '\n'
        << (reflect::is_public_v<metaobj> ? "public" : "non-public")
        << (reflect::is_static_v<metaobj> ? "static" : "")
        << " "
        << reflect::get_base_name_v<reflect::get_type_t<metaobj>>
        << " "
        << reflect::get_base_name_v<metaobj>
        << '\n';
    return 0;
}

template <typename MetaObjects, std::size_t I>
void do_print_data_members(std::index_sequence<I...>) {
    eat(do_print_data_member<MetaObjects, I>()...);
}

template <typename MetaObjects>
void do_print_data_members(void) {
    using namespace std;

    do_print_data_members<MetaObjects>(
        make_index_sequence<
            reflect::get_size_v<MetaObjects>
```

```text
Public data members of foo
0: public static bool b
1: public float x
2: public float y
3: public float z
All data members of foo
0: non-public int _i
1: non-public int _j
2: public static bool b
3: public float x
4: public float y
5: public float z
6: non-public static double d
```

显示类 foo 的公有和私有成员

## 8.2.3 模式匹配

诸如 `std::tuple`<sup>28</sup> 或 `std::variant`<sup>29</sup> 之类的新数据类型需要处理其元素的新方式。简单的 if 或 switch 条件，或者像 `std::apply`<sup>30</sup> 或 `std::visit`<sup>31</sup> 这样的函数，只能提供基本功能。模式匹配在函数式编程中被大量使用，它允许更高效地处理这些新数据类型。

以下来自关于模式匹配的提案 P1371R2<sup>32</sup> 的代码片段，将经典控制结构与模式匹配进行了比较。模式匹配使用关键字 `inspect` 和 `__` 作为占位符。

- switch 语句

### switch 语句与模式匹配对比

```cpp
switch (x) {
    case 0: std::cout << "got zero"; break;
    case 1: std::cout << "got one"; break;
    default: std::cout << "don't care";
}

inspect (x) {
    0: std::cout << "got zero";
    1: std::cout << "got one";
    __: std::cout << "don't care";
}
```

- if 条件

### if 语句与模式匹配对比

```cpp
if (s == "foo") {
    std::cout << "got foo";
} else if (s == "bar") {
    std::cout << "got bar";
} else {
    std::cout << "don't care";
}

inspect (s) {
    "foo": std::cout << "got foo";
    "bar": std::cout << "got bar";
    __: std::cout << "don't care";
}
```

模式匹配在 `std::tuple`、`std::variant` 或多态上的应用展示了它的威力。

- `std::tuple`

### std::tuple 与模式匹配对比

```cpp
auto& [x, y] = p;
if (x == 0 && y == 0) {
    std::cout << "on origin";
} else if (x == 0) {
    std::cout << "on y-axis";
} else if (y == 0) {
    std::cout << "on x-axis";
} else {
    std::cout << x << ',' << y;
}

inspect (p) {
    [0, 0]: std::cout << "on origin";
    [0, y]: std::cout << "on y-axis";
    [x, 0]: std::cout << "on x-axis";
    [x, y]: std::cout << x << ',' << y;
}
```

- `std::variant`

### std::variant 与模式匹配对比

```cpp
struct visitor {
    void operator()(int i) const {
        os << "got int: " << i;
    }
    void operator()(float f) const {
        os << "got float: " << f;
    }
    std::ostream& os;
};
std::visit(visitor{strm}, v);

inspect (v) {
    <int> i: strm << "got int: " << i;
    <float> f: strm << "got float: " << f;
}
```

- 多态数据类型

