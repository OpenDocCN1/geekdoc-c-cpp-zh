

## 7.2.2 noexcept 与特殊成员函数

特殊成员函数可能会自动生成 noexcept 条件。

### 复制和移动特殊成员函数的 noexcept

按规则，当特殊成员函数被生成但未实现时，会生成 noexcept 条件。³ 在这种情况下，如果所有基类和非静态成员对应的操作保证不抛出异常，那么这些操作也保证不抛出异常。

例如：

`basics/specialnoexcept.cpp`

```cpp
#include <iostream>
#include <type_traits>

class B
{
    std::string s;
};

int main()
{
    std::cout << std::boolalpha;
    std::cout << std::is_nothrow_default_constructible<B>::value << '\n';
    std::cout << std::is_nothrow_copy_constructible<B>::value << '\n';
    std::cout << std::is_nothrow_move_constructible<B>::value << '\n';
    std::cout << std::is_nothrow_copy_assignable<B>::value << '\n';
    std::cout << std::is_nothrow_move_assignable<B>::value << '\n';
}
```

程序的输出如下：

```text
true
false
true
false
true
```

生成的复制构造函数和复制赋值运算符可能会抛出异常，因为复制 `std::string` 可能会抛出异常。然而，生成的默认构造函数、移动构造函数和移动赋值运算符保证不抛出异常，因为 `std::string` 类的默认构造函数、移动构造函数和移动赋值运算符也保证不抛出异常。⁴

³ 这也适用于默认构造函数、默认化的 `operator<` 或 `operator==` 等“伪”特殊成员函数（自 C++20 起可用），甚至适用于所有继承的构造函数。

⁴ 对于字符串的移动赋值运算符，只有在字符串使用相同或可互换的分配器时，noexcept 保证才成立。

注意，即使这些特殊成员函数是用 `=default` 用户声明的，也会生成 noexcept 条件。因此，如果我们按如下方式声明类 B，也会得到相同的效果：

```cpp
class B
{
    std::string s;
public:
    B(const B&) = default;                     // 自动生成 noexcept 条件
    B(B&&) = default;                          // 自动生成 noexcept 条件
    B& operator= (const B&) = default;         // 自动生成 noexcept 条件
    B& operator= (B&&) = default;              // 自动生成 noexcept 条件
};
```

当你有一个默认化的特殊成员函数时，你可以显式指定一个与生成条件不同的 noexcept 保证。例如：

```cpp
class C
{
    ...
public:
    C(const C&) noexcept = default;          // 保证不抛出异常（自 C++20 起可行）
    C(C&&) noexcept(false) = default;        // 指定可能抛出异常（自 C++20 起可行）
    ...
};
```

在 C++20 之前，如果生成的 noexcept 条件与指定的条件相矛盾，定义的函数会被删除。

### 析构函数的 noexcept

按规则，析构函数默认总是保证不抛出异常。这适用于生成的析构函数和实现的析构函数。

例如：

```cpp
class B
{
    std::string s;
public:
    ...
    ~B() {                                // 自动总是声明为 ~B() noexcept
    }
};
```

使用 noexcept(false)，你可以声明它们不提供此保证，但这通常毫无意义，因为 C++ 标准库的若干保证基于析构函数从不抛出异常这一事实。

## 7.3 类层次结构中的 `noexcept` 声明

我们看到，尤其是当我们需要实现移动构造函数时，应该用 `noexcept` 保证来声明它。一般来说，遵循 C++ 标准的规则，当所有基类和所有成员类型在移动赋值时不抛出异常，我们应该声明它不抛出异常。

通用模式如下：

```cpp
class Base {

};

class Drv : public Base {
  MemType member;

  ...
  // 移动构造函数：
  Drv(Drv&&) noexcept(std::is_nothrow_move_constructible_v<Base> &&
                      std::is_nothrow_move_constructible_v<MemType>);

};
```

这里，如果基类 `Base` 和成员类型 `MemType` 保证不抛出异常，类 `Drv` 的移动构造函数就保证不抛出异常。

移动赋值运算符可能使用相同的模式，但请注意，在多态类型中，移动赋值运算符无论如何都应该被删除，这意味着通常不需要在派生类中实现它们。

### 7.3.1 检查抽象基类中的 `noexcept` 移动构造函数

注意，类型特征 `std::is_nothrow_move_constructible<>` 并不总是如预期那样工作。对于抽象基类，它总是返回 false，因为它还检查你是否可以用移动构造函数创建该类型的对象，而抽象类型不可能做到这一点。

因此，使用标准类型特征无法表述一个在所有情况下都有效的声明：“如果抽象基类保证不抛出异常，则我保证不抛出异常”。通常，你可能需要知道基类移动构造函数是否可能抛出异常。

为了使你能够检查一个类的移动构造函数是否保证不抛出异常，你可以实现以下辅助类型特征（这里为 C++20 实现）。⁵ 但是，请注意，你必须为每个纯虚函数提供实现：

`poly/isnothrowmovable.hpp`

```cpp
// type trait to check whether a base class guarantees not to throw
// in the move constructor (even if the constructor is not callable)
#ifndef IS_NOTHROW_MOVABLE_HPP
#define IS_NOTHROW_MOVABLE_HPP

#include <type_traits>

template<typename Base>
struct Wrapper : Base {
  using Base::Base;
  // implement all possibly wrapped pure virtual functions:
  void print() const {}
  ...
};

template<typename T>
static constexpr inline bool is_nothrow_movable_v
  = std::is_nothrow_move_constructible_v<Wrapper<T>>;

#endif //IS_NOTHROW_MOVABLE_HPP
```

⁵ 感谢 Daniel Krügler 提供此解决方案。

现在，你甚至可以检查抽象基类的移动构造函数是否是 noexcept。以下程序演示了标准类型特征与用户自定义类型特征的不同行为：

`poly/isnothrowmovable.cpp`

```cpp
#include "isnothrowmovable.hpp"
#include <iostream>

class Base {
  std::string id;
  ...
public:
  virtual void print() const = 0;  // 纯虚函数（强制抽象基类）
  ...
  virtual ~Base() = default;
protected:
  // 受保护的复制和移动语义（也强制抽象基类）：
  Base(const Base&) = default;
  Base(Base&&) = default;
  // 禁用赋值运算符（因为切片问题）：
  Base& operator= (Base&&) = delete;
  Base& operator= (const Base&) = delete;
};

int main()
{
  std::cout << std::boolalpha;
  std::cout << "std::is_nothrow_move_constructible_v<Base>: "
            << std::is_nothrow_move_constructible_v<Base> << '\n';
  std::cout << "is_nothrow_movable_v<Base>:              "
            << is_nothrow_movable_v<Base> << '\n';
}
```

