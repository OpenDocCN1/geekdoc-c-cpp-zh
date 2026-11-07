
![](img/7ef3d1ca55bdc192f1cc0929179f3d21_129_0.png)

这意味着最终 vector 只需释放旧内存并更新其成员：

![](img/7ef3d1ca55bdc192f1cc0929179f3d21_129_1.png)

### 有条件的 noexcept 声明

然而，用 `noexcept` 标记移动构造函数可以吗？嗯，我们移动名字（一个 `std::string`），并向标准输出流写入一些内容。如果在那里抛出异常，就违反了不抛出的保证。在这种情况下，程序在运行时会调用 `std::terminate()`，它通常调用 `std::abort()` 来表明程序异常结束（并且常常生成核心转储）。

因此，如果字符串成员和输出操作都不抛出，我们就应给出不抛出的保证。引入关键字 `noexcept` 是因为你可以用它来指定有条件的不抛出保证。它看起来如下（完整示例见 *basics/personcond.hpp*）：

```cpp
class Person {
 private:
   std::string name;
 public:
   ...
   Person(Person&& p)
      noexcept(std::is_nothrow_move_constructible_v<std::string>
                  && noexcept(std::cout << name))
      : name{std::move(p.name)} {
         std::cout << "MOVE " << name << '\n';
      }
   ...
}
```

借助 `noexcept(...)`，我们保证：如果括号内的编译期表达式为 true，则不抛出。在这种情况下，要给出保证，我们需要满足两件事：

- 使用 `std::is_nothrow_move_constructible_v<std::string>`（在 C++20 之前，必须使用 `std::is_nothrow_move_constructible<std::string>::value`），我们使用标准类型特征（类型函数）来告诉我们 `std::string` 的移动构造函数是否保证不抛出。
- 使用 `noexcept(std::cout << name)`，我们询问对名字调用输出表达式是否保证不抛出。这里，我们把 `noexcept` 用作运算符，它告诉我们执行传入表达式所需的所有对应操作是否保证不抛出。

可以想象，有了这个声明，重新分配将再次使用拷贝构造函数。字符串的移动构造函数确实保证不抛出，但输出运算符不保证。然而，移动构造函数通常不输出任何内容；因此，一般来说，当成员不抛出时，我们可以为整个移动构造函数给出不抛出的保证。

好消息是，如果你不自己实现移动构造函数，编译器会为你检测 `noexcept` 保证。对于所有成员在移动构造函数中都保证不抛出的类，生成的或默认的移动构造函数将整体给出该保证。

考虑以下声明：

*basics/persondefault.hpp*

```cpp
#include <string>
#include <iostream>

class Person {
  private:
    std::string name;
  public:
    Person(const char* n)
      : name{n} {
    }

    std::string getName() const {
      return name;
    }

    // print out when we copy:
    Person(const Person& p)
      : name(p.name) {
        std::cout << "COPY " << name << '\n';
    }
    // force default generated move constructor:
    Person(Person&& p) = default;
    ...
};
```

在这种情况下，我们声明应生成默认移动构造函数：

```cpp
class Person {
    ...
    // force default generated move constructor:
    Person(Person&& p) = default;
    ...
};
```

这意味着我们只在拷贝时打印。当使用生成的移动构造函数时，我们只会看到没有执行拷贝。

现在让我们用通常的程序在最后打印一些 Person 对象：

```cpp
#include "persondefault.hpp"
#include <iostream>
#include <vector>

int main()
{
    std::vector<Person> coll{"Wolfgang Amadeus Mozart",
                             "Johann Sebastian Bach",
                             "Ludwig van Beethoven"};
    std::cout << "capacity: " << coll.capacity() << '\n';
    coll.push_back("Pjotr Iljitsch Tschaikowski");

    std::cout << "name of coll[0]: " << coll[0].getName() << '\n';
}
```

我们得到以下输出：

```text
COPY Wolfgang Amadeus Mozart
COPY Johann Sebastian Bach
COPY Ludwig van Beethoven
capacity: 3
name of coll[0]: Wolfgang Amadeus Mozart
```

我们只看到初始化列表中元素的拷贝。对于其他所有情况，包括重新分配，都使用默认移动构造函数。正如我们所看到的，在重新分配后的内存中，第一个人的名字是正确的。

如果我们完全不指定任何成员函数，行为也相同。这意味着：

- 如果你**实现**了移动构造函数，就应声明它是否以及何时保证不抛出。
- 如果你没有实现移动构造函数，则完全不需要指定任何内容。

如果类的性能或该类对象的重新分配对你很重要，你可能还想在编译期再次检查你的类的移动构造函数是否保证不抛出：

```cpp
static_assert(std::is_nothrow_move_constructible_v<Person>);
```

或者对于 C++17 及之前版本：

```cpp
static_assert(std::is_nothrow_move_constructible<Person>::value, "");
```

### 7.1.3 noexcept 值得吗？

你可能想知道，用或多或少复杂的 `noexcept` 表达式声明移动构造函数是否值得。Howard Hinnant 用一个简单的程序演示了效果（为本书稍作改编）：

```cpp
// basics/movenoexcept.cpp

#include <iostream>
#include <string>
#include <vector>
#include <chrono>

// string wrapper with move constructor:
struct Str
{
    std::string val;

    // ensure each string has 100 characters:
    Str()
      : val(100, 'a') {   // don't use braces here
    }

    // enable copying:
    Str(const Str&) = default;

    // enable moving (with and without noexcept):
    Str (Str&& s) NOEXCEPT
      : val(std::move(s.val)) {
    }
};

int main()
{
    // create vector of 1 Million wrapped strings:
    std::vector<Str> coll;
    coll.resize(1000000);

    // measure time to reallocate memory for all elements:
    auto t0 = std::chrono::steady_clock::now();
    coll.reserve(coll.capacity() + 1);
    auto t1 = std::chrono::steady_clock::now();

    std::chrono::duration<double, std::milli> dt{t1 - t0};
    std::cout << dt.count() << "ms\n";
}
```

我们提供了一个类，它包装一个长度可观的字符串（以避免*小字符串优化*）。注意，我们必须用圆括号初始化该值，因为花括号会把 100 解释为值为 100 的初始字符。

在类中，我们用 `NOEXCEPT` 标记移动构造函数，预处理器可以将其替换为空或 `noexcept`（例如，用 `-DNOEXCEPT=noexcept` 编译）。然后我们测量在 vector 中重新分配 100 万个这种对象需要多长时间。

在几乎所有平台上，用 `noexcept` 声明移动构造函数会使重新分配快最多 10 倍（确保启用了显著的优化级别）。也就是说，一次重新分配（通常由插入新元素强制触发）可能耗时约 20 毫秒而不是 200 毫秒。这意味着我们无法使用该 vector 的时间少了 180 毫秒。这可能带来巨大的好处。²

## 7.2 noexcept 声明的细节

如前所述，引入 `noexcept` 是为了允许指定有条件的不抛出保证。一般来说，在编译期知道函数不会抛出可以改进代码和优化，因为你不必处理因抛出异常而可能需要的清理。请注意，如果违反了 `noexcept` 保证，程序会调用 `std::terminate()`，它通常调用 `std::abort()` 来导致“异常程序终止”（例如，核心转储）。

### 7.2.1 用 noexcept 声明函数的规则

在声明 `noexcept` 条件时，有几条规则适用：

- `noexcept` 条件必须是产生一个可转换为 `bool` 的值的编译期表达式。
- 不能重载仅 `noexcept` 条件不同的函数。
- 在类层次结构中，`noexcept` 条件是所指定接口的一部分。用不 `noexcept` 的函数覆盖基类中 `noexcept` 的函数是错误的（但反过来则不是）。

例如：

```cpp
class Base {
public:
  ...
  virtual void foo(int) noexcept;
  virtual void foo(int);       // ERROR: overload on different noexcept clause only
  virtual void bar(int);
};

class Derived : public Base {
public:
  ...
```

² 请注意，Visual C++ 2015 中有一个 bug，这意味着在重新分配时总是使用 `move`，我们看不到差异。此 bug 已在 Visual C++ 2017 中修复（如果移动构造函数不保证不抛出，这可能会减慢重新分配）。
