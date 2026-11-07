
例如，假设你有如下整数序列：

1 2 3 4 5 4 3 2 1

调用算法 `std::remove()` 并传入值 2，以移除所有值为 2 的元素，序列会被修改为：

1 3 4 5 4 3 1 2 1

所有值不为 2 的元素都会被移到前面，而新的末尾（即“最后一个”元素之后的位置）返回的是值为 2 的元素的位置。

如果可能的话，这些算法会移动元素。也就是说，它们会把值被移走的元素留在 moved-from 状态。在这个例子中，如果元素是字符串，最后一个 2 将不会被触碰，但最后一个 1 会在 2 之前被向前移动，因此最后一个元素会处于 moved-from 状态。

因此，这些算法也可能让元素处于 moved-from 状态。实际上，以下算法会创建 moved-from 状态：

- `std::remove()` 和 `std::remove_if()`
- `std::unique()`

让我们看一个完整的例子。考虑一个类，我们可以从中看出某个元素是否处于 moved-from 状态：

*lib/email.hpp*

```cpp
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
      : Email{std::string{val}} {
    }

    std::string getValue() const {
        assert(!movedFrom);   // or throw
        return value;
    }

    // implement move operations to signal a moved-from state:
    Email(Email&& e) noexcept
        : value{std::move(e.value)}, movedFrom{e.movedFrom} {
        e.movedFrom = true;
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
    }
};
```

通过实现移动构造函数和移动赋值运算符，我们设置了一个成员 `movedFrom`，并在输出运算符中对它进行求值。

现在，让我们把这个类的一些元素放入一个 `vector` 中，并使用算法 `std::remove_if()` 移除一些元素。在这里，我们移除所有以“.de”结尾的电子邮件地址：

*lib/removeif.cpp*

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
                                 [](const Email& e) {
                                     auto val = e.getValue();
                                     return val.size() > 2 &&
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

程序的输出如下：

```text
remaining elements:
  "jill@company.com"
  "hana@company.com"
all elements:
  "jill@company.com"
  "hana@company.com"
  "sarah@domain.de"
  "MOVED-FROM"
```

在“移除”以“.de”结尾的元素之后，新的末尾是第二个元素之后的位置。然而，在容器中，你仍然有第三个元素，它完全没有被移动，以及第四个元素，它处于新的 moved-from 状态，因为它被移动赋值给了第二个元素（第二个元素之前又被移动到了第一个元素）。

在使用这些 moved-from 对象时请务必小心，正如关于 moved-from 状态的章节所讨论的那样。

## 14.3 移动迭代器

通过使用*移动迭代器*（也是在 C++11 中引入的），你甚至可以在其他算法中，以及一般在任何接受输入范围的地方（例如在构造函数中）使用移动语义。

然而，使用这些迭代器时务必小心。在遍历容器或范围的元素时，每次访问元素都会使用 `std::move()`。这可能明显更快，但会让元素处于有效但未指定的状态。你不应该重复使用同一个元素。

### 14.3.1 算法中的移动迭代器

在算法中使用移动迭代器通常只有在算法保证每个元素只使用一次时才有意义。因此，算法应当：

- 要求源使用*输入迭代器*类别，目标使用*输出迭代器*类别
- 或者保证每个元素只使用一次（例如，`std::for_each()` 算法就是这样规定的）

对于带有可调用对象的算法，在允许指定具体功能时，元素会通过 `std::move()` 传递给可调用对象。在可调用对象内部，你可以决定如何处理它们：

- 按值接收参数，从而总是移动/窃取值或资源
- 按值/万能引用接收参数，以决定移动/窃取哪个值或资源

例如：

`lib/foreachmove.cpp`

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

template<typename T>
void print(const std::string& name, const T& coll)
{
    std::cout << name << " (" << coll.size() << " elems): ";
    for (const auto& elem : coll) {
        std::cout << "\"" << elem << "\" ";
    }
    std::cout << "\n";
}

void process(std::string s) // gets moved value from rvalues
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
                          process(std::move(elem));
                      }
                  });

    print("coll", coll);
}
```

在这个程序中，我们将所有大小为 4 的元素移动到辅助函数 `process()`：

```cpp
// move away only the elements processed:
std::for_each(std::make_move_iterator(coll.begin()),
              std::make_move_iterator(coll.end()),
              [] (auto&& elem) {
                  if (elem.size() != 4) {
                      process(std::move(elem));
                  }
              });
```

为此，我们通过万能引用来接收这些被移动迭代器用 `std::move()` 标记的元素，并将其通过 `std::move()` 传递给 `process()`。由于 `process()` 按值接收参数，该值基本上就被移走了。

因此，所有大小不为 4 的元素都会变成容器 `coll` 中的 moved-from 对象。所以，该程序的输出如下（? 表示我们不知道具体的值）：

```text
coll (4 elems):  "don't" "vote" "for" "liars"
- process(don't)
- process(for)
- process(liars)
coll (4 elems):  "?" "vote" "?" "?"
```

通常，最后一行如下：

```text
coll (4 elems):  "" "vote" "" ""
```

如你所见，这里使用了辅助函数 `std::make_move_iterator()`，这样在声明迭代器时就无需指定元素类型了。自 C++17 起，*类模板实参推导（CTAD）* 允许直接声明 `std::move_iterator` 类型，而无需指定元素类型：

```cpp
std::for_each(std::move_iterator{coll.begin()},
              std::move_iterator{coll.end()},
              [] (auto&& elem) {
                  if (elem.size() != 4) {
                      process(std::move(elem));
                  }
              });
```

