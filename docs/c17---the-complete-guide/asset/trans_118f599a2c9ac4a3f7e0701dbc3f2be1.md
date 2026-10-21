
```cpp
template<typename T>
const T& spaceBefore(const T& arg) {
    std::cout << ' ';
    return arg;
}

template<typename First, typename... Args>
void print (const First& firstarg, const Args&... args) {
    std::cout << firstarg;
    (std::cout << ... << spaceBefore(args)) << '\n';
}
```

这里，

`(std::cout << ... << spaceBefore(args))`

是一个折叠表达式，展开为：

`std::cout << spaceBefore(arg1) << spaceBefore(arg2) << ...`

因此，对于参数包 `args` 中的每个元素，该表达式会调用一个辅助函数，该函数在返回传入的参数之前打印一个空格字符，并将其写入 `std::cout`。为了确保这不适用于第一个参数，我们添加了一个不使用 `spaceBefore()` 的额外首参数。

注意，参数包输出的求值要求所有左侧输出在实际元素调用 `spaceBefore()` 之前完成。得益于 `operator <<` 和函数调用的定义求值顺序，自 C++17 起这得到了保证。

我们也可以在 `print()` 内部使用 lambda 来定义 `spaceBefore()`：

```cpp
template<typename First, typename... Args>
void print (const First& firstarg, const Args&... args) {
    std::cout << firstarg;
    auto spaceBefore = [](const auto& arg) -> const auto& {
        std::cout << ' ';
        return arg;
    };
    (std::cout << ... << spaceBefore(args)) << '\n';
}
```

如果不能将其全部合并到一条语句中，C++ 就不是 C++ 了：

```cpp
template<typename First, typename... Args>
void print (const First& firstarg, const Args&... args) {
    std::cout << firstarg;
    (std::cout << ... << [](const auto& arg) -> decltype(auto) {
        std::cout << ' ';
        return arg;
    }(args)) << '\n';
}
```

不过，实现 `print()` 的一个更简单的方法是使用一个 lambda 同时打印空格和参数，然后将其传递给一元折叠：

```cpp
template<typename First, typename... Args>
void print(First first, const Args&... args) {
    std::cout << first;
    auto outWithSpace = [](const auto& arg) {
        std::cout << ' ' << arg;
    };
    (... , outWithSpace(args));
    std::cout << '\n';
}
```

通过使用以 `auto` 声明的额外模板参数，我们可以使 `print()` 更加灵活，从而可以对分隔符进行参数化，使其可以是字符、字符串或任何其他可打印类型。

## 11.2.2 支持的运算符

除 `.`、`->` 和 `[]` 之外，你可以在折叠表达式中使用所有二元运算符。

### 折叠函数调用

折叠表达式还可以与逗号运算符一起使用，将多个函数调用合并为一条语句。也就是说，你现在可以简单地实现：

```cpp
template<typename... Types>
void callFoo(const Types&... args)
{
    ...
    (... , foo(args));        // calls foo(arg1), foo(arg2), foo(arg3), ...
}
```

以便对所有传入的参数调用函数 `foo()`。

或者，如果需要支持移动语义：

```cpp
template<typename... Types>
void callFoo(Types&&... args)
{
    ...
    (... , foo(std::forward<Types>(args)));   // calls foo(arg1), foo(arg2), ...
}
```

为了确保该代码在调用函数返回具有重载逗号运算符的类型的值时安全，你应该将返回类型强制转换为 `void`：

```cpp
template<typename... Types>
void callFoo(Types&&... args)
{
    ...
    (... , (void)foo(std::forward<Types>(args)));   // calls foo(arg1), foo(arg2), ...
}
```

请注意，由于逗号运算符的性质，我们使用左折叠还是右折叠运算符通常无关紧要。函数总是从左到右调用。对于

`(foo(args) , ...);`

括号只是将调用分组，使得第一个 `foo()` 调用与接下来的两个 `foo()` 调用的结果组合如下：

`foo(arg1) , (foo(arg2) , foo(arg3));`

然而，由于逗号运算符的求值顺序通常是从左到右，第一次调用仍然发生在括号内两个调用组成的组之前，而在括号内部，中间的调用仍然发生在最右边的调用之前。²

² 通过重载逗号运算符，你可以改变其求值顺序，这可能会影响左折叠和右折叠的调用顺序。

然而，由于左折叠表达式与“原生”求值顺序相匹配，如果你使用折叠表达式进行多次函数调用，仍然建议使用左折叠表达式。

### 组合哈希函数

使用逗号运算符进行折叠表达式的另一个示例是组合哈希值。可以这样做：

```cpp
template<typename T>
void hashCombine (std::size_t& seed, const T& val)
{
    seed ^= std::hash<T>()(val) + 0x9e3779b9 + (seed<<6) + (seed>>2);
}

template<typename... Types>
std::size_t combinedHashValue (const Types&... args)
{
    std::size_t seed = 0;            // initial seed
    (... , hashCombine(seed,args));  // chain of hashCombine() calls
    return seed;
}
```

通过调用

`combinedHashValue ("Hi", "World", 42);`

中间的语句展开为：

`hashCombine(seed,"Hi"), hashCombine(seed,"World"), hashCombine(seed,42);`

有了这些定义，我们可以很容易地为诸如 `Customer` 这样的类型定义一个新的哈希函数对象，以用于 unordered set 或作为 unordered map 的键：

```cpp
struct CustomerHash
{
    std::size_t operator() (const Customer& c) const {
        return combinedHashValue(c.getFirstname(), c.getLastname(),
            c.getValue());
    }
};

std::unordered_set<Customer, CustomerHash> coll;
std::unordered_map<Customer, std::string, CustomerHash> map;
```

### 基类的折叠函数调用

折叠函数调用甚至可以用于更复杂的表达式。例如，你可以折叠逗号运算符来调用可变数量基类的成员函数：

`tmp/foldcalls.cpp`

```cpp
#include <iostream>

// template for variadic number of base classes
template<typename... Bases>
class MultiBase : private Bases...
{
public:
    void print() {
        // call print() of all base classes:
        (... , Bases::print());
    }
};

struct A {
    void print() { std::cout << "A::print()\n"; }
```

```cpp
}
int getValue() const {
    return value;
}
...
// traverse helpers:
static constexpr auto left = &Node::subLeft;
static constexpr auto right = &Node::subRight;

// traverse tree, using fold expression:
template<typename T, typename... TP>
static Node* traverse (T np, TP... paths) {
    return (np ->* ... ->* paths);    // np ->* paths1 ->* paths2 ...
};
```

这里，

`(np ->* ... ->* paths)`

使用折叠表达式从 `np` 开始遍历 `paths` 的可变元素，可以按如下方式使用：

`tmpl/foldtraverse.cpp`

```cpp
#include "foldtraverse.hpp"
#include <iostream>

int main()
{
    // init binary tree structure:
    Node* root = new Node{0};
    root->subLeft = new Node{1};
    root->subLeft->subRight = new Node{2};
    ...
    // traverse binary tree:
    Node* node = Node::traverse(root, Node::left, Node::right);
    std::cout << node->getValue() << '\n';
    node = root ->* Node::left ->* Node::right;
    std::cout << node->getValue() << '\n';
    node = root -> subLeft -> subRight;
    std::cout << node->getValue() << '\n';
}
```

当调用

`Node::traverse(root, Node::left, Node::right);`

时，折叠表达式的调用展开为：

