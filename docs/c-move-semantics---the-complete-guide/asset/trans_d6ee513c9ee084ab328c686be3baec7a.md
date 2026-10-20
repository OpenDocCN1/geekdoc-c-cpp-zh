

例如，假设你有一个包含以下整数值的序列：

1 2 3 4 5 4 3 2 1

调用算法 `std::remove()` 并传入值 2 来移除所有值为 2 的元素，会将序列修改为：

1 3 4 5 4 3 1 2 1

所有不等于 2 的元素都会被移动到前面，而新的末尾（即“最后一个”元素之后的位置）返回的是元素 2 的位置。

如果可能，这些算法会进行移动。也就是说，它们将值被移走的元素留在 moved-from 状态。在本例中，如果元素是字符串，最后一个 2 不会被触碰，但最后一个 1 会被移动到 2 之前，从而使最后一个元素处于 moved-from 状态。

因此，这些算法也可能使元素处于 moved-from 状态。实际上，以下算法会产生 moved-from 状态：

- `std::remove()` 和 `std::remove_if()`
- `std::unique()`

让我们看一个完整的示例。考虑一个这样的类，我们可以查看一个元素是否处于 moved-from 状态：

lib/email.hpp

```
#include <iostream>
#include <cassert>
#include <string>

// class for email addresses
// - asserts that each email address has a @
// - except when in a moved-from state
class Email {
private:
    std::string value;        // email address
    bool movedFrom{false};    // special moved-from state
public:
    Email(const std::string& val)
    : value{val} {
        assert(value.find('@') != std::string::npos);
    }
    Email(const char* val)    // enable implicit conversions for string literals
    : Email{std::string(val)} {
    }

    std::string getValue() const {
        assert(!movedFrom);  // or throw
        return value;
    }
}
```

```cpp
// implement move operations to signal a moved-from state:
Email(Email&& e) noexcept {
    value{std::move(e.value)}, movedFrom{e.movedFrom} {
        e.movedFrom = true;
    }
}
Email& operator=(Email&& e) noexcept {
    value = std::move(e.value);
    movedFrom = e.movedFrom;
    e.movedFrom = true;
    return *this;
}
// enable copying:
Email(const Email&) = default;
Email& operator=(const Email&) = default;
// print out the current state (even if it is a moved-from state):
friend std::ostream& operator<<(std::ostream& strm, const Email& e) {
    return strm << (e.movedFrom ? "MOVED-FROM" : e.value);
};
```

通过实现移动构造函数和移动赋值运算符，我们设置了一个成员 `movedFrom`，并在输出运算符中对其求值。

现在，让我们将此类的一些元素放入 vector 中，并使用算法 `std::remove_if()` 移除一些元素。在本例中，我们移除所有以 ".de" 结尾的电子邮件地址：

```cpp
#include "email.hpp"
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

int main()
{
    std::vector<Email> coll{ "tom@domain.de", "jill@company.com",
        "sarah@domain.de", "hana@company.com" };
    // remove all email addresses ending with ".de":
    auto newEnd = std::remove_if(coll.begin(), coll.end(),
        [] (const Email& e) {
            auto&& val = e.getValue();
            return val.size() > 2 &&
                val.substr(val.size()-3) == ".de";
        });
    // ...
```

```
val.substr(val.size()-3) == ".de";
});

// print elements up to the new end:
std::cout << "remaining elements:\n";
for (auto pos = coll.begin(); pos != newEnd; ++pos) {
    std::cout << "  " << *pos << "\n";
}

// print all elements in the container:
std::cout << "all elements:\n";
for (const auto& elem : coll) {
    std::cout << "  " << elem << "\n";
}
}
```

程序输出如下：

remaining elements:
    "jill@company.com"
    "hana@company.com"
all elements:
    "jill@company.com"
    "hana@company.com"
    "sarah@domain.de"
    "MOVED-FROM"

在“移除”以 ".de" 结尾的元素后，新的末尾是第二个元素之后的位置。然而，容器中仍然有第三个元素，它完全未被移动，还有第四个元素，它处于新的 moved-from 状态，因为它的内容被移动赋值给了第二个元素（而第二个元素之前又被移动到了第一个元素）。

使用这些 moved-from 对象时要小心，正如关于 moved-from 状态的章节所讨论的。

## 14.3 移动迭代器

通过使用移动迭代器（同样在 C++11 中引入），你可以在其他算法中使用移动语义，甚至通常在所有接受输入范围的地方（例如构造函数中）使用移动语义。

但是，使用这些迭代器时要小心。在遍历容器或范围的元素时，每次访问元素都会使用 `std::move()`。这可能会明显更快，但会使元素处于有效但未指定的状态。你不应该两次使用同一个元素。

### 14.3.1 算法中的移动迭代器

在算法中使用移动迭代器通常只有在算法保证只使用每个元素一次时才有意义。因此，算法应满足以下条件：

- 要求源的输入迭代器类别和目标的输出迭代器类别
- 或者保证每个元素只使用一次（例如，`std::for_each()` 算法就有这样的保证）

对于带可调用对象的算法，通过允许指定详细的功能，元素会以 `std::move()` 方式传递给可调用对象。在可调用对象内部，你可以决定如何处理它们：

- 按值接受参数，以始终移动/窃取值或资源
- 按右值/通用引用接受参数，以决定移动/窃取哪个值或资源

例如：

lib/foreachmove.cpp

```
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

template<typename T>
void print(const std::string& name, const T& coll)
{
    std::cout << name << " (" << coll.size() << " elems): ";
    for (const auto& elem : coll) {
        std::cout << " \"" << elem << "\"";
    }
    std::cout << "\n";
}

void process(std::string s)  // gets moved value from rvalues
{
    std::cout << "- process(" << s << ")\n";
    ...
}

int main()
{
    std::vector<std::string> coll{"don't", "vote", "for", "liars"};
    print("coll", coll);

    // move away only the elements processed:
    std::for_each(std::make_move_iterator(coll.begin()),
                  std::make_move_iterator(coll.end()),
                  [] (auto&& elem) {
                      if (elem.size() != 4) {
```

```
process(std::move(elem));
}
});

print("coll", coll);
}
```

在这个程序中，我们将所有大小为 4 的元素移动到辅助函数 `process()`：

```
// move away only the elements processed:
std::for_each(std::make_move_iterator(coll.begin()),
    std::make_move_iterator(coll.end()),
    [] (auto&& elem) {
        if (elem.size() != 4) {
            process(std::move(elem));
        }
    });
```

为此，我们通过通用引用获取由移动迭代器标记为 `std::move()` 的元素，并将其通过 `std::move()` 传递给 `process()`。因为 `process()` 按值接受参数，所以值基本上被移走了。

因此，所有大小不为 4 的元素在容器 `coll` 中都变成了 moved-from 对象。程序的输出如下（? 表示我们不知道值）：

```
coll (4 elems): "don't" "vote" "for" "liars"
- process(don't)
- process(for)
- process(liars)
coll (4 elems): "?" "vote" "?" "?"
```

通常，最后一行如下：

```
coll (4 elems): "" "vote" "" ""
```

如你所见，这里使用了辅助函数 `std::make_move_iterator()`，这样在声明迭代器时就不需要指定元素类型。从 C++17 开始，类模板实参推导（CTAD）允许直接声明 `std::move_iterator` 类型，而无需指定元素类型：

```
std::for_each(std::move_iterator{coll.begin()},
    std::move_iterator{coll.end()},
    [] (auto&& elem) {
        if (elem.size() != 4) {
            process(std::move(elem));
        }
    });
```

