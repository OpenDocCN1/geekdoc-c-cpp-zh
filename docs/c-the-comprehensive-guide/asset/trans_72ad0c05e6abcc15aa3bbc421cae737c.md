
```cpp
public:
  explicit Year(int v) : value_(v) {}
  std::ostream& print(std::ostream& os) const;
  Year& advance(const Year& other);
  bool equals(const Year& other) const;
  bool less_than(const Year& other) const;
};
std::ostream& Year::print(std::ostream& os) const {
  return os << value_;
}
std::ostream& operator<<(std::ostream& os, const Year& year) {
  return year.print(os);
}
Year& Year::advance(const Year& other) {
  value_ += other.value_;
  return *this;
}
bool Year::equals(const Year& other) const {
  return value_ == other.value_;
}
bool Year::less_than(const Year& other) const {
  return value_ < other.value_;
}
```

**清单 12.27** “Year” 不再有 “value()”，并且需要其他方法。

同样的操作对 Month 和 Day 也同样适用。然而，你需要考虑*设计*问题：超出有效范围的计算会发生什么，例如 `Month{12}.advance(Month{1})`？那么 Date 呢？如果你从 2024-12-31 向前移动一天，会发生什么？

你需要澄清一些技术问题，这些问题有时没有对错之分，但你需要决定一种清晰的实现方式。具体选择哪种方式在很大程度上取决于需求。

一个相当合理的要求可能是 `Date::advance()` 始终返回一个有效日期。为了实现这一点，可以借助 `Date::normalize()` 工具函数：它会检查部分 Year、Month 和 Day 数据的合理性，并在必要时进行修正。这意味着部分数据本身不应被修正，因为它可能需要整个日期的上下文。

## 流式编程（Fluent Programming）

我建议 `advance()` 应该通过 `*this` 返回当前对象。此外，请考虑下面的清单。

```cpp
Year year{2024};
year.advance(Year{1}).advance(Year{3});
cout << year; // Output: 2028
```

**清单 12.28** 如果 “advance” 返回对象本身，那么之后你可以继续调用另一个方法。

这与 `operator<<(ostream& os, ...)` 的做法类似。在这种做法中，你以 `return os` 结束实现。这允许你在一个表达式中将多个 `<<` 链接在一起，正如你在本书中经常看到的那样。

这种设计编程接口的方式被称为**流式 API（Fluent API）**。通过从每个函数返回对象引用，你可以直接链式调用下一个方法。这使得源代码非常易读，尤其是对于拥有许多方法的大型复杂类。你甚至可以更深入地使用这一概念，让多个类以这种方式协作。

清单 12.29 展示了一个示例草图，让你了解这可能意味着什么。如你所见，这种表示与这里要生成的 HTML 页面的结构非常相似。让这种结构反映在程序代码中是有好处的。

```cpp
Page page = Html().body()
    .h1("Heading")
    .table().border(0)
        .tr()
            .td().css("head").text("Dog Breed").end()
            .td().text("Poodle").end()
        .end()
    .end()
    .toPage();
```

**清单 12.29** 流式编程接口有时能让代码变得清晰。

## 用 “const” 标记方法

你有没有注意到，我在 `print`、`equals` 和 `less_than` 的方法签名后面写了 `const`？这是必要的，用来表明该方法不会改变当前实例的值。这使你的程序具有 *const 正确性*，我将在第 13 章 13.10 节详细讨论。

### 12.11.5 为类型提供局部名称

让我们回到一个仍然存在 `value()` 方法的 Year 版本。这可能是一个合理的设计决策。

有时，类中使用的类型属于你的*接口*。这意味着用户需要知道该类型并正确使用它，才能恰当地使用这个类。

例如，用户需要用 `int` 初始化 Year 的构造函数。他们需要知道并使用这个类型，以避免编译器进行其他隐式类型转换来生成所需的 `int`。此外，`value()` 的返回值有意使用相同的类型。因此，使用返回值的表达式也必须具有匹配的类型——否则你必须接受另一次转换。

```cpp
// https://godbolt.org/z/hbsbMsGr1
class Year {
    int value_;                       // actually internally used type
public:
    explicit Year(int v) : value_{v} {} // type becomes part of the interface
    int value() { return value_; }      // also in the return
};
int main() {
    Year year{ 2024 };                 // type int
    int val = year.value();             // matching type
}
```

**清单 12.30** 内部类型 “int” 已成为类接口的一部分。

但是，如果你作为 Year 类的开发者，后来发现 `long` 是封装值的更好类型，那该怎么办？那么编写 `main()` 的开发者就不得不调整他们所有使用 Year 的代码——即使那个开发者就是你自己。

然而，你和用户可以共同采取预防措施。将相应的类型*显式地*作为类接口的一部分，而不是简单地将本质上是内部的类型暴露给外部。为此，可以在类中定义一个局部但公开的类型别名，并在所有相关位置使用它。

```cpp
// https://godbolt.org/z/EYjo8E8Gn
class Year {
public:
    using value_type = int;             // introduce type alias
    value_type value_;                  // actually internally used type
public:
    explicit Year(value_type v) : value_{v} {}
    value_type value() { return value_; }
};
int main() {
    Year year{ 2024 };                  // rely on compiler conversion here
    Year::value_type val = year.value(); // use it
}
```

**清单 12.31** 借助 “using”，你可以引入类型别名，从而更容易维护与类型本身相关的接口。

正如你在 `Year::value_type` 中看到的那样，你需要使用*作用域运算符* `::` 从 `Year` 中访问 `value_type`。

这样，你总能适当地声明接收 `value()` 返回值的变量。

然而，我想指出，这实际上只是实际使用类型的别名。这意味着，你仍然可以凭借对类的内部了解写出 `int val = year.value();`，而编译器不会报错。如果你拥有这样的专门知识，就应该避免使用它。尽可能多地使用公开暴露的类型别名。这会让你的代码更加灵活。它还表明，你选择该类型是出于特定原因——为了匹配所使用的类——而不仅仅是因为你特别喜欢 `int` 或因为它是 32 位的。

标准库中的类也为你提供了这种机制。如果你忘记了 vector 的元素类型，可以使用 `vector` 局部的 `value_type` 类型别名。也许更有用的是 `size_type`，它表示 `size()` 及类似方法的返回类型。

```cpp
// https://godbolt.org/z/zdMfoa7Y
#include <vector>
#include <set>
#include <iostream>
using std::vector; using std::set; using std::cout;
using vector_t = vector<unsigned long long>; // Your own type alias
int main() {
    vector_t huge{ 12ULL, 10'000'000'000ULL, 9ULL, 0ULL, };
    vector_t::size_type sz = huge.size();
    vector_t::value_type ululu = huge[1];
    for(vector_t::iterator it = huge.begin(); it != huge.end(); ++it)
        *it *= 2; // double
    // sort via set
    set<vector_t::value_type> sorted{huge.begin(), huge.end()};
    for(vector_t::value_type val : sorted)
        cout << val << " ";
    cout << "\n";
}
```

清单 12.32 标准库还包含许多有用的类型别名。

因此，使用标准库的内部类型时，你总是安全的。通过引入自定义的 `vector_t` 类型别名，我想说明我所说的“忘记”元素类型是什么意思。通过将 `vector_t` 作为 `vector<unsigned long long>` 的名称，`unsigned long long` 在某种程度上被隐藏了。现在，编写 `vector_t::value_type` 甚至比滚动回文件开头查看当时 `vector` 的确切元素类型更加容易。
