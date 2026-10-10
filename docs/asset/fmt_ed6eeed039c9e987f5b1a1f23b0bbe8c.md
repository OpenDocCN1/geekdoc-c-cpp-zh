
```
// https://godbolt.org/TPWc5nexg
#include <system_error> // error_code, errc
#include <string>
void create_dir(const std::string& pathname, std::error_code& ec);
void run() {
    std::error_code ec;
    create_dir("/some/path", ec);
    if(ec == std::errc::file_exists) { // 特指 -
    } else if(!ec) { // 成功 -
    } else { // 失败 -
    }
}
```

**列表 28.35** “`error_code`”与“`error_condition`”的比较。

为了启用比较，重载了运算符 `==` 的自由函数。

```cpp
bool operator==(const error_code& lhs, const error_code& rhs) noexcept;
bool operator==(const error_code& lhs, const error_condition& rhs) noexcept;
bool operator==(const error_condition& lhs, const error_code& rhs) noexcept;
bool operator==(const error_condition& lhs, const error_condition& rhs) noexcept;
```

# 列表 28.36 `operator==()` 的重载（简写）。

这间接确保了 `error_code` `EEXIST` 和 `ERROR_ALREADY_EXISTS` 都可以与 `error_condition` `errc::file_exists` 进行等效比较。

实现部分负责将特定系统的 `error_codes` 映射到通用的 `error_condition` 错误类别。

# 作为类常量的枚举值

`enum class errc` 的定义如下。

```cpp
enum class errc {
  address_family_not_supported,
  address_in_use,
  // ...
  value_to_large,
  wrong_protocol_type,
};
```

# 列表 28.37 `enum class errc` 的定义

当我们随后应用比较 `ec == errc::file_exists` 时，似乎发生了从 `errc` 元素到 `error_condition` 实例的隐式转换。几乎如此，但不完全是：为了整个系统具有可扩展性，`ec` 的 `error_category` 必须以某种方式被考虑。由于错误值存在重叠，66 在文件操作中代表一个意思，而在内存操作中代表完全不同的意思。这通过 `error_category` 机制解决了。此外，`errc` 代表 `error_condition` 的一组常量。但库也支持反向方法——即将表示 `error_code` 的枚举与 `error_condition` 实例进行比较。

因此，等效检查需要两个步骤：

- 1. 决定 `errc` 代表特定错误码的枚举还是通用的错误条件。

- 2. 将值与 `error_category` 关联。

对于步骤 1，使用了 `is_error_code_enum` 和 `is_error_condition_enum` 类型特质。默认情况下，`is_error_code_enum<E>::value` 和 `is_error_condition_enum<E>::value` 产生 `false`。标准库现在特化了 `is_error_condition_enum`，并定义了 `is_error_condition_enum<errc>::value == true`。

```cpp
template {}
struct is_error_condition_enum<errc> : true_type {};
```

列表 28.38 针对 "`errc`" 的 "`is_error_condition_enum`" 特化。

隐式转换随后可以通过 `error_condition` 构造函数的模板化来实现——即通过 `template <class E> error_condition(E e)`。当我们写 `ec == errc::file_exists` 时，编译器选择了 `bool operator==(const error_code& a, const error_condition& b)` 重载，因为构造函数提供了一种将枚举转换为 `error_condition` 的方法。这使得我们很容易用给 `error_code` 测试特定的 `error_condition`——即使它仅由枚举元素表示。

# 通往错误类别的路径

现在是步骤 2。通过构造函数的转换了适当的 `error_condition`。在其中调用了自由函数 `make_error_condition()`。它也对 `errc` 进行了重载：

```cpp
error_condition make_error_condition(errc c) noexcept {
    return error_condition(
        static_cast<int>(c),
        generic_category());
}
error_condition make_error_condition(io_errc c) noexcept /*...*/ */
error_condition make_error_condition(future_errc c) noexcept /*...*/ */
```

**列表 28.39** 在 "`make_error_condition`" 的重载中，`errc` 是之一。另外两个是 `io_errc`（见）和 `future_errc`（见）。

例如，库代码可能如下所示，尝试连接线程：

```cpp
int osSpecificCode = pthread_detach(thread, 0);
if (osSpecificCode != 0)
    throw system_error(
        error_code(osSpecificCode, system_category()),
        "thread::detach failed"
    );
```

# 28.4 错误类别

有两个主要的错误类别：

- `generic_category`

- `system_category`

例如，库代码可能如下，尝试连接线程：

```cpp
int osSpecificCode = pthread_detach(thread, 0);
if (osSpecificCode != 0)
    throw system_error(
        error_code(osSpecificCode, system_category()),
        "thread::detach failed"
    );
```

同样，继续支持移植的 `error_category`。

# 28.5 自定义代码

如果你想使用自定义错误码，建议按如下方式进行：

- 定义带有你的错误码的枚举。

- 然后在项目中使用 `make_error_code`。

- 为你的枚举创建 `make_error_condition` 的重载。

- 特化模板 `is_error_condition_enum` 使标准库知道你支持它。

- 最后一步映射到 `error_condition` 是可选的。

# 28.5.6 "system_error" 异常

倾向于将错误作为异常传播的使用了同名头文件中大型聚合异常类 `system_error`。该类再次传输了：

- `error_code`，由一个 `int` 细节和一个 `error_category` 组成；以及

- 错误消息。

[PAGE 1533]

你会在用户代码中处理这种情况：

```cpp
// https://godbolt.org/z/a
#include <thread>
#include <iostream>
#include <system_error>
int main() {
  try {
    std::thread(); // this will fail
  } catch (std::system_error& e) {
    std::cout << "error with code: " << e.code()
              << "message: " << e.what() << '\n';
  }
}
```

对我来说，这输以下内容：

error with code: generic: message: Invalid argument

在标准库中，有许多地方可以抛出 `system_error`。你可以这样处理它们：

```cpp
// https://godbolt.org/z/c
#include <iostream>
#include <system_error>
int main() {
  try {
    std::thread(nullopt); // triggers an exception
  } catch (std::system_error& e) {
    std::cerr << "Error: ";
    if (e.code() == std::errc::invalid_argument) {
      std::cerr << "system\n";
    } else {
      std::cerr << "other\n";
    }
  }
}
```

[1534]

所以你在块中捕获异常。通过将其与 `error_code()` 比较，你可以更精确地检查可移植条件。

[1535]

## 28.6 运行时类型信息："<typeinfo>" 和 "<typeindex>"

`<typeinfo>` 头文件实际上只包含少量内容：

- 运算符 `typeid()`：一个用于确定唯一标识的函数运算符

- 类 `type_info`：`typeid()` 的返回类型

- 在动态类型上下文中发生的异常 `bad_cast` 和 `bad_type`

这有一点小谎言：`typeid()` 类似于 `sizeof()`，因为它不是一个函数而是一个运算符，而且 `typeid` 甚至是一个关键字。然而，在使用 `typeid()` 之前你必须包含 `<typeinfo>` 头文件；否则会报错。因此，你可以将 `typeid()` 视为定义在头文件函数。

通过这个“函数”，你可以获取你作为参数指定的的类型信息，你可以将其用于比较，或者在有限范围内用于调试。该类型可以是类型的名称，也可以是一个表达式。在后的情况下，`typeid()` 返回关于该表达式类型的信息。然而，

[1536]

该表达式不能包含像 `a+b` 这样的计算，甚至是方法或函数调用。

但 `typeid()` 返回什么信息呢？嗯，主要是指向 `type_info` 实例的 `const&`；我们称之为 `ti`。通过 `ti` 可以完成以下操作：

- `size_t ti.hash_code()`：返回一个哈希值，例如用于快速测试不相等性。

- `const char* ti.name()`：返回类型的文本表示。然而，它没有标准的格式，对于程序中的所有类型也不得必须不同，也不保证该文本对于给定的类型总是相同的。因此，它并不可靠（尽管提供了有用信息），因此主要用于诊断。

- `type_index(ti)`：这个来自 `<typeindex>` 头文件的重要函数是根据它们的 `type_info` 引用检查两个类型相等性的方法。

比“哪些可用”更重要的或许是“哪些不可用”：你不能创建或拷贝 `type_info`，也不应该用 `==` 比较它们。不能保证两次调用 `typeid(A)` 的 `ti1` 和 `ti2` 会返回相同的 `type_info`——事实上，即使 `type_info` 重载了 `operator==`，也无法保证 `ti1 == ti2`。

如果你想找出 `ti1` 和 `ti2` 是否代表相同类型，请这样做：`type_index(ti1) == type_index(ti2)`。

[1537]

`typeindex` 还可以作为 `map` 及类似结构的键，而 `type_info` 则做不到。这允许你构建一个具有可靠类型名称的机制，例如。

```cpp
// https://godbolt.org/z/d1G9ez4KW
#include <iostream>
#include <typeinfo>
#include <typeindex>
#include <map>
#include <string>
struct Base {
    virtual ~Base() {}
};
struct DerivedOne : public Base {};
struct DerivedTwo : public Base {};
int main() {
    using std::string; using std::cout; using std::type_index;
    std::map<string, type_index> names = {
    type_index(typeid(int)), "int",
    type_index(typeid(double)), "double",
    type_index(typeid(Base)), "Base",
    type_index(typeid(DerivedOne)), "Derived One",
    type_index(typeid(DerivedTwo)), "Derived Two",
    type_index(typeid(string)), "string",
    type_index(typeid(iterator)), "iterator" // 等等，此逻辑仅用于说明
    };
}
```

（注：map 的 OCR 文本略有乱码，逻辑遵循 `typeid` 到字符串的标准映射）。

[1538]

```
}
}
```

等等，OCR 文本非常混乱。让我们根据提供的文本重新对齐逻辑流。

```cpp
using boost::core::demangled_name;
cout<<demangled_name(BOOST_CORE_TYPEID(i))<<'\n'; // Output: int
cout<<demangled_name(BOOST_CORE_TYPEID(f))<<'\n'; // Output: float
cout<<demangled_name(BOOST_CORE_TYPEID(double))<<'\n'; // Output: double
std::string s;
cout<<demangled_name(BOOST_CORE_TYPEID(s.begin()))<<'\n'; // Output: gnu cxx::normal_iterator<char*, std::cxx::basic_string<char>*>
cout<<demangled_name(BOOST_CORE_TYPEID(name))<<'\n'; // Output: std::map<int, std::string, std::less<int>>
std::allocator<std::pair<int, const, std::string>> alloc;
cout<<demangled_name(BOOST_CORE_TYPEID(666))<<'\n'; // Output: int
```

**Listing 28.42** Boost 的 “`demangled_name`” 对于输出类型名称非常有用。

## 28.7 泛函数对象的辅助类："<functional>"

`<functional>` 中的函数比 `<numeric>` 更多，它们的作用是为了补充标准库的其他部分。你很少会单独包含 `<functional>`。如果你想用 `<algorithm>` 或容器来解决一个“简单”任务，值得看一眼 `<functional>`，那里可能已经有了解决方案。

例如，如果你想对容器中的所有元素求和，可以使用来自 `<numeric>` 的 `accumulate`。但如果你想用 `*` 代替 `+`，你可以：

- 或者写一个 lambda 表达式 `[](auto a, auto b) { return a*b };`

- 或者使用 `<functional>` 中的 `multiplies`，它们的功能正是此的。

`<functional>` 中的许多其他内容也是如此。

我将 `<functional>` 提供的内容（或或少任意地）分类为以下几个领域：

- 函数 `function` 是 C++ 中所有可调用对象的中心点。`bind` 从函数对象创建一个参数少一个参数的新函数对象。`mem_fn` 从方法创建一个函数对象。在此上下文中，还有几个辅助构造结构。

- 用于算术运算（如 `multiplies`）、比较（如 `equal_to`）、逻辑运算（如 `logical_and` 等）和位运算（如 `bit_and` 等）的具体函数对象，你可以用它们代替简单的 lambda。

- 特殊的哈希函数：无序容器（unordered containers）所需的哈希对象在这里为内置类型定义。例如，你会发现模板特化 `hash<int>` 及其所有相关类。这应该是不言自明的，因此我不再详细阐述。

在第 25 章 Listing 25.15 中，有一个 `multiplies` 配合 `<numeric>` 中的 `accumulate` 使用的示例。其他定义的函数对象可以在表 28.11 到表 28.14 中找到。
