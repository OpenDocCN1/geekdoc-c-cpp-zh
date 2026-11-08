
## 直接抛出标准异常

显然，如果你要抛出标准异常，就只应在与其用途一致的情况下抛出它们。这意味着，例如，你不应抛出 `bad_cast` 异常，因为它们已经有了特定作用。抛出 `std::exception` 类型的对象也不太有用，因为它过于通用；它没有提供一个可以传入描述性字符串的构造函数。最有用的标准异常类是在 `<stdexcept>` 模块中定义、派生自 `logic_error` 或 `runtime_error` 的那些类。举一个熟悉的例子，当作为参数提供的维度无效时，你可以在 `Box` 类构造函数中抛出一个标准的 `out_of_range` 异常：

```cpp
Box::Box(double length, double width, double height)
  : m_length {length}, m_width {width}, m_height {height}
{
    if (length <= 0.0 || width <= 0.0 || height <= 0.0)
        throw std::out_of_range("Zero or negative Box dimension.");
}
```

构造函数体会在任一参数为零或负数时抛出 `out_of_range` 异常。当然，源文件需要包含定义 `out_of_range` 类的 `<stdexcept>` 模块。`out_of_range` 类型是一种 `logic_error`，因此非常适合这种特定用途。这里的另一个候选是更通用的 `std::invalid_argument` 异常类。不过，如果没有一个预定义异常类符合你的需要，你可以自己派生一个异常类。

## 派生自己的异常类

从某个标准异常类派生自己的类的一个主要优点是，你的类会成为同一异常家族的一部分。这使你能够在同一个 catch 块中既捕获标准异常，也捕获自己的异常。例如，如果你的异常类派生自 `logic_error`，那么参数类型为 `logic_error` 的 catch 块既能捕获你的异常，也能捕获以该类为基类的标准异常。以 `exception` 为参数类型的 catch 块总能捕获标准异常——只要你的类以 `exception` 为基类，也能捕获你自己的异常。

你可以通过让 `Trouble` 异常类派生自 `exception` 类，非常简单地将 `Trouble` 异常类及其派生类纳入标准异常家族。只需按如下方式修改类定义：

```cpp
class Trouble : public std::exception
{
public:
    explicit Trouble(std::string_view message = "There's a problem");
    const char* what() const noexcept override;

private:
    std::string m_message;
};
```

这为基类中定义的虚 `what()` 成员提供了自己的实现。由于它是对基类成员的重定义，我们在 `what()` 的声明中添加了 `override`。按照我们的约定，我们还移除了 `virtual` 说明符。不过，更有意思的是，我们添加了 `noexcept` 规范，以表明不会从 `what()` 中抛出异常。事实上，我们必须这样做。任何对 `noexcept` 函数的覆盖也必须为 `noexcept`。还值得一提的是，`noexcept` 必须始终指定在 `const` 之后、`override` 之前。

成员函数的定义必须包含与类定义中该函数相同的异常规范。因此，`what()` 函数变成如下形式（不得重复 `virtual` 或 `override`，但 `noexcept` 要保留）：

```cpp
const char* Trouble::what() const noexcept { return m_message.c_str(); }
```

> **注意**  我们故意没有给 `Trouble` 的构造函数添加 `noexcept` 说明符。这个构造函数不可避免地必须将给定的错误消息复制到相应的 `std::string` 成员变量中。这反过来又不可避免地涉及字符数组的分配。而内存分配在原则上总是可能出错并抛出 `std::bad_alloc` 异常。

举一个更具体的例子，让我们再次回到 `Box` 类定义。对于上一节中定义的构造函数，从 `std::out_of_range` 派生一个异常类可能很有用，这样可以提供一种选择，使 `what()` 能返回更具体的字符串，以标识导致抛出异常的问题。你可以这样做：

```cpp
export module dimension_error;
import <stdexcept>;        // For derived exception classes such as std::out_of_range
import <string>;           // For std::to_string()

export class DimensionError : public std::out_of_range
{
public:
  explicit DimensionError(double value)
    : std::out_of_range("Zero or negative dimension: " + std::to_string(value))
    , m_value{value} {}

  // Function to obtain the invalid dimension value
  double getValue() const noexcept { return m_value; }
private:
  double m_value;
};
```

构造函数提供一个参数，用于指定导致抛出异常的维度值。它用一个新字符串对象调用基类构造函数，该字符串由一条消息和值拼接而成。`to_string()` 函数是定义在 `<string>` 模块中的模板函数；它返回其参数的字符串表示，而参数可以是任意数值类型的值。继承的 `what()` 函数将返回创建 `DimensionError` 对象时传递给构造函数的字符串。这个特定的异常类还添加了一个成员变量来存储无效值，以及一个公有函数来获取它，例如在 catch 块中使用。

下面展示这个异常类如何在 `Box` 类定义中使用：

```cpp
// Box.cpp
export module box;
import <algorithm>;        // For the std::min() function template
import dimension_error;
```

**练习 16-4.** 从图 16-8 中任意挑选若干标准库异常类型，并编写一个程序，使这些异常类型依次被引发（当然，不要自己实际抛出它们）。你应捕获每个异常并输出它们包含的 `what()` 消息，然后再继续触发下一个异常。

**练习 16-5.** 创建一个名为 `readEvenNumber()` 的函数，旨在从 `std::cin` 流中读取一个偶数整数。在某个读取过程开始时，`readEvenNumber()` 内部会发生一次读取，从而产生 `CurveBall` 异常。为此，你可以直接复用练习 16-4 中的代码。然而，正常情况下，该函数会验证用户输入，并在用户正确输入偶数时返回该偶数。然而，如果输入无效，该函数会抛出以下异常之一：

- 如果输入的任何值不是数字，则抛出 `NotANumber` 异常。
- 如果用户输入负数，则抛出 `NegativeNumber` 异常。
- 如果用户输入奇数，函数抛出 `OddNumber` 异常。

你应从 `std::domain_error`（`<stdexcept>` 模块中定义的标准异常类型之一）派生这些新异常类型。它们的构造函数应组合出一个至少包含错误输入值的字符串，然后将该字符串转发给 `std::domain_error` 的构造函数。

提示：在尝试从 `std::cin` 读取一个整数后，你可以使用 `std::cin.fail()` 检查该整数的解析是否成功。如果该成员函数返回 true，则用户输入的字符串不是数字。注意，一旦流处于这种失败状态，在调用 `std::cin.clear()` 之前，你不能再使用该流。此外，用户输入的非数字值仍会留在流中——在提取整数失败时它不会被移除。例如，你可以使用 `<string>` 中定义的 `std::getline()` 函数将其提取出来。把这一切放在一起，你的代码可能包含类似下面的内容：

```cpp
if (std::cin.fail())
{
    std::cin.clear();    // Reset the failure state
    std::string line;    // Read the erroneous input and discard it
    std::getline(std::cin, line);
}
```

一旦辅助函数 `readEvenNumber()` 准备就绪，就用它来实现 `askEvenNumber()`。该函数向 `std::cout` 打印用户指令，然后调用 `readEvenNumber()` 来处理实际输入和输入验证。一旦正确读取到一个数字，`askEvenNumber()` 会礼貌地感谢用户输入该数字，并且消息应包含数字本身。对于 `readEvenNumber()` 抛出的任何 `std::exception`，`askEvenNumber()` 至少应输出其 `what()` 消息。如果异常不是 `domain_error`，则应重新抛出它，因为 `askEvenNumber()` 不知道如何处理它。然而，如果异常是 `domain_error`，则应重试请求输入偶数，除非该异常是 `NotANumber`。如果发生 `NotANumber`，`askEvenNumber()` 将停止请求输入数字并直接返回。
