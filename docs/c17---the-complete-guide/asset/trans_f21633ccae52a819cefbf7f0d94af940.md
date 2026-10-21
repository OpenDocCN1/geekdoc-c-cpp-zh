

## 从迭代器推导类型

为了能够从定义初始化范围的迭代器中推导出元素类型，容器有一个推导指引，例如针对 `std::vector<>` 的如下推导指引：

```
// 让 std::vector<> 从初始化迭代器推导元素类型：
namespace std {
    template<typename Iterator>
    vector(Iterator, Iterator)
        -> vector<typename iterator_traits<Iterator>::value_type>;
}
```

这允许，例如：

```
std::set<float> s;
std::vector v1(s.begin(), s.end());    // 正确，推导出 std::vector<float>
```

注意，这里使用带括号的初始化非常重要。如果你使用花括号：

```
std::vector v2{s.begin(), s.end()};    // 注意：不会推导出 std::vector<float>
```

这两个参数会被当作初始化列表的元素（根据重载解析规则，其优先级更高）。也就是说，它等价于：

```
std::vector<std::set<float>::iterator> v2{s.begin(), s.end()};
```

这意味着我们初始化一个包含两个元素的 vector，第一个元素指向源容器第一个元素，第二个元素表示最后一个元素之后的位置。

另一方面，考虑：

```
std::vector v3{"hi", "world"};    // 正确，推导出 std::vector<const char*>
std::vector v4("hi", "world");    // 糟糕：致命的运行时错误
```

声明 `v3` 也是用两个元素（两个字符串字面量）初始化 vector，而第二个声明会导致致命的运行时错误，但愿能导致核心转储。问题是字符串字面量会转换为字符指针，而字符指针是合法的迭代器。因此，我们传递了两个不指向同一对象的迭代器。换句话说：我们传递了一个无效范围。我们推导出 `std::vector<const char>`，但根据两个字面量在内存中的位置，我们可能得到一个 `bad_alloc` 异常，或者因为完全没有距离而得到核心转储，或者得到存储在两者之间的某些未定义字符的范围。

总而言之，使用花括号始终是初始化 vector 元素的最佳方式。唯一的例外是传递单个 vector 时（此时优先使用拷贝构造函数）。当传递其他内容时，最好使用括号。

无论如何，对于像 `std::vector<>` 和其他 STL 容器这样具有复杂构造函数的类型，强烈建议不要使用类模板参数推导，而是显式指定元素类型。

## std::array<> 的推导

一个更有趣的例子是 `std::array<>` 类。为了能够同时推导元素类型和元素个数：

```
std::array a{42, 45, 77};    // 正确，推导出 std::array<int,3>
```

定义了以下推导指引（间接地）：

```
typename Allocator = allocator<pair<const Key, T>>
map(initializer_list<pair<const Key, T>>,
    Compare = Compare(),
    Allocator = Allocator())
-> map<Key, T, Compare, Allocator>;
}
```

所有参数均按值传递，因此这个推导指引使得传递的比较器或分配器的类型能够按前文讨论的方式发生退化。然而，我们天真地使用了相同的参数类型，这意味着初始化列表使用了 const 键类型。结果，下面的代码无法工作（正如 Ville Voutilainen 在 http://wg21.link/lwg3025 中指出的）：

```
std::pair elem1{1,2};
std::pair elem2{3,4};
...
std::map m1{elem1, elem2};    // 使用原始 C++17 推导指引时出错
```

因为 `elem1` 和 `elem2` 被推导为 `std::pair<int,int>`，而要求 pair 中第一个类型为 const 类型的推导指引不匹配。因此，你仍然必须这样写：

```
std::map<int,int> m1{elem1, elem2};  // 正确
```

因此，在推导指引中，必须去掉 const：

```
namespace std {
template<typename Key, typename T,
        typename Compare = less<Key>,
        typename Allocator = allocator<pair<const Key, T>>>
map(initializer_list<pair<Key, T>>,
    Compare = Compare(),
    Allocator = Allocator())
-> map<Key, T, Compare, Allocator>;
}
```

然而，为了仍然支持比较器和分配器的退化，我们还必须为具有 const 键类型的 pair 重载推导指引。否则，当传递具有 const 键类型的 pair 时，构造函数将被用于类模板参数推导，这意味着传递 const 键和非 const 键的 pair 时推导结果会略有不同。

## 智能指针没有推导指引

请注意，C++ 标准库中的某些地方没有推导指引，尽管你可能期望它们存在。

你可能期望 shared 和 unique 指针有推导指引，这样就不必写：

```
std::shared_ptr<int> sp{new int(7)};
```

而可以直接写：

```
std::shared_ptr sp{new int(7)};      // 不支持
```

这不能自动工作，因为相应的构造函数是一个模板，这意味着没有隐式推导指引适用：

```
namespace std {
    template<typename T> class shared_ptr {
        public:
            ...
            template<typename Y> explicit shared_ptr(Y* p);
            ...
    };
}
```

`Y` 是与 `T` 不同的模板参数，这意味着从构造函数推导出 `Y` 并不意味着我们能推导出类型 `T`。这是为了能够调用类似下面的代码：

```
std::shared_ptr<Base> sp{new Derived(...)};
```

提供相应的推导指引很简单：

```
namespace std{
    template<typename Y> shared_ptr(Y*) -> shared_ptr<Y>;
}
```

然而，这也意味着在分配数组时会使用该指引：

```
std::shared_ptr sp{new int[10]};      // 糟糕：会推导出 shared_ptr<int>
```

正如在 C++ 中经常遇到的那样，我们陷入了令人讨厌的 C 语言问题：指向单个对象的指针和指向对象数组的指针具有或退化为相同的类型。

这个问题看起来很危险，因此 C++ 标准委员会决定不支持它。

对于单个对象，你仍然必须调用：

```
std::shared_ptr<int> sp1{new int};      // 正确
auto sp2 = std::make_shared<int>();      // 正确
```

对于数组：

```
std::shared_ptr<std::string> p(new std::string[10],
    [](std::string* p) {
        delete[] p;
    });
```

或者，使用为原始数组实例化共享指针的新特性，直接写：

```
std::shared_ptr<std::string[]> p{new std::string[10]};
```

## 9.3 补充说明

类模板参数推导最早由 Michael Spertus 在 2007 年于 http://wg21.link/n2332 提出。该提案在 2013 年由 Michael Spertus 和 David Vandevoorde 在 http://wg21.link/n3602 重新讨论。最终被接受的形式由 Michael Spertus、Faisal Vali 和 Richard Smith 在 http://wg21.link/p0091r3 中拟定，并经过 Michael Spertus、Faisal Vali 和 Richard Smith 在 http://wg21.link/p0512r0、Jason Merrill 在 http://wg21.link/p0620r0 以及 Michael Spertus 和 Jason Merrill 在 http://wg21.link/p702r1（作为针对 C++17 的缺陷报告）中的修改。

标准库中对类模板参数推导的支持由 Michael Spertus、Walter E. Brown 和 Stephan T. Lavavej 在 http://wg21.link/p0433r2 和 http://wg21.link/p0739r0（作为针对 C++17 的缺陷报告）中添加。

## 第 10 章

## 编译期 if

使用 `if constexpr(...)` 语法，编译器使用编译期表达式在编译时决定使用 if 语句的 then 分支还是 else 分支（如果有的话）。另一个分支（如果有）会被丢弃，意味着不会生成代码。这并不意味着被丢弃的部分被完全忽略。它仍然会像未使用的模板代码一样被检查。

例如：

tmp l/ifcomptime.hpp

```
#include <string>

template<typename T>
std::string asString(T x)
{
    if constexpr(std::is_same_v<T, std::string>) {
        return x;        // 如果无法转换为 string，则该语句无效
    }
    else if constexpr(std::is_arithmetic_v<T>) {
        return std::to_string(x); // 如果 x 不是数值，则该语句无效
    }
    else {
        return std::string(x);    // 如果无法转换为 string，则该语句无效
    }
}
```

通过使用 `if constexpr`，我们在编译期决定是直接返回传入的字符串，对传入的整型或浮点值调用 `to_string()`，还是使用构造函数将传入参数转换为 `std::string` 类型。无效的调用会被丢弃，因此以下代码能够编译（如果使用普通的运行时 if 则无法编译）：

