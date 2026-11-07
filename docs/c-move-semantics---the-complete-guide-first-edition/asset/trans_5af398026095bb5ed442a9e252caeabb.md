
### 实现移动语义

第三种选择是实现移动操作，使它们不破坏类的不变量。为此，我们必须决定被移动后对象应处于什么状态。为了支持 `asString()` 在不检查值是否存在的情况下调用 `operator*`，我们将不得不始终提供一个值。例如，我们可以有一个静态的移出后值，将其赋给值被移走的对象。⁶

`basics/sharedint.hpp`

```cpp
#include <memory>
#include <string>

class SharedInt {
  private:
    std::shared_ptr<int> sp;
    // special “value” for moved-from objects:
    inline static std::shared_ptr<int> movedFromValue{std::make_shared<int>(0)};

  public:
    explicit SharedInt(int val)
      : sp{std::make_shared<int>(val)} {
    }

    std::string asString() const {
      return std::to_string(*sp);    // OOPS: unconditional deref
    }

    // fix moving special member functions:
    SharedInt (SharedInt&& si)
      : sp{std::move(si.sp)} {
        si.sp = movedFromValue;
    }
    SharedInt& operator= (SharedInt&& si) noexcept {
      if (this != &si) {
        sp = std::move(si.sp);
        si.sp = movedFromValue;
      }
      return *this;
    }

    // enable copying (deleted with user-declared move operations):
    SharedInt (const SharedInt&) = default;
    SharedInt& operator= (const SharedInt&) = default;
};
```

⁶ 注意，内联静态成员仅从 C++17 起才受支持。在 C++17 之前，你必须在单独的 CPP 文件中定义该成员，以遵守*单一定义规则*（ODR）。

注意，我们必须用 = default 声明拷贝特殊成员函数，因为当我们有用户声明的特殊移动成员函数时，这些拷贝特殊成员函数会被删除。

### 6.4 总结

- 对于每个类，明确被移动后对象的状态。你必须确保它们至少可析构（在不实现特殊成员函数时通常如此）。然而，你类的用户可能期望/要求更多。
- C++ 标准库函数的要求也适用于被移动后的对象。
- 生成的特殊移动成员函数可能使被移动后的对象进入破坏类不变量的状态。尤其可能发生在以下情况：
  - 类没有具有确定值的默认构造函数（因此没有自然的被移动后状态）
  - 成员的值有限制（例如断言）
  - 成员的值相互依赖
  - 使用了具有类似指针语义的成员（指针、智能指针等）
- 如果被移动后的状态破坏了不变量或使操作失效，你应使用以下选项之一来修复：
  - 禁用移动语义
  - 修复移动语义的实现
  - 在类内部处理被破坏的不变量，并对外隐藏它们
  - 通过记录被移动后对象的约束和前置条件来放宽类的不变量

## 第 7 章：移动语义与 noexcept

当 C++11 的移动语义接近完成时，我们发现了一个问题：vector 的重新分配无法使用移动语义。因此，引入了新关键字 noexcept。

本章解释该问题，以及这对 C++ 代码中 noexcept 的使用意味着什么。

### 7.1 带与不带 noexcept 的移动构造函数

让我们通过一个小例子来引入这个话题，以引出 noexcept 关键字的动机。

#### 7.1.1 不带 noexcept 的移动构造函数

考虑下面的类，它引入了一个带有 string 成员的类型，并实现了拷贝构造函数和移动构造函数，以便让这些构造函数的调用可见：

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

    // print out when we copy or move:
    Person(const Person& p)
      : name{p.name} {
        std::cout << "COPY " << name << '\n';
    }
    Person(Person&& p)
      : name{std::move(p.name)} {
        std::cout << "MOVE " << name << '\n';
    }
...
};
```

现在让我们创建并初始化一个 Person 的 vector，并在稍后插入一个已存在的 Person：

*basics/person.cpp*

```cpp
#include "person.hpp"
#include <iostream>
#include <vector>

int main()
{
    std::vector<Person> coll{"Wolfgang Amadeus Mozart",
                             "Johann Sebastian Bach",
                             "Ludwig van Beethoven"};
    std::cout << "capacity: " << coll.capacity() << '\n';
    coll.push_back("Pjotr Iljitsch Tschaikowski");
}
```

程序的输出如下：

```text
COPY Wolfgang Amadeus Mozart
COPY Johann Sebastian Bach
COPY Ludwig van Beethoven
capacity: 3
MOVE Pjotr Iljitsch Tschaikowski
COPY Wolfgang Amadeus Mozart
COPY Johann Sebastian Bach
COPY Ludwig van Beethoven
```

我们首先将初始值拷贝到 vector 中（因为容器的 `std::initializer_list<>` 构造函数按值接收传入的参数）。因此，vector 通常会为三个元素分配内存（在图中，我用缩写表示字符串值）：

用于将 vector 恢复到其先前状态的内存（C++ 标准库假定并要求析构函数不抛出异常；否则它就无法回滚）。

重新分配正是移动语义的理想场景，因为我们把元素从一个位置移动到另一个位置。因此，自 C++11 起，我们希望在这里使用移动语义。然而，这样一来我们就麻烦了：如果在重新分配期间抛出异常，我们可能无法回滚。新内存中的元素已经窃取了旧内存中元素的值。因此，仅仅销毁新元素还不够；我们必须将它们移回去。但我们怎么知道将它们移回去不会失败呢？

你可能会认为移动构造函数永远不应抛出异常。对于字符串来说这也许是对的（因为我们只是移动整数值和指针），但由于我们要求被移动后的对象处于有效状态，而这个状态可能需要内存，这意味着如果内存耗尽，移动就可能抛出异常（例如，Visual C++ 的基于节点的容器就是这样实现的）。

我们也不能放弃这一保证，因为程序可能已经利用这一特性来避免为 vector 创建备份，而丢失这些数据可能成为（安全性）关键问题。而不再支持 `push_back()` 对于 C++11 的接受度来说将是一场噩梦。

最终决定是：仅当元素类型的移动构造函数保证不抛出异常时，才在重新分配时使用移动语义。

#### 7.1.2 带 noexcept 的移动构造函数

因此，当我们保证类 `Person` 的移动构造函数永不抛出异常时，我们的小示例程序的行为会发生变化：

`basics/personmove.hpp`

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

    // print out when we copy or move:
    Person(const Person& p)
      : name{p.name} {
        std::cout << "COPY " << name << '\n';
    }
    Person(Person&& p) noexcept  // guarantee not to throw
        : name{std::move(p.name)} {
        std::cout << "MOVE " << name << '\n';
    }
...
};
```

如果我们现在像之前一样使用 Person 对象：

`basics/personmove.cpp`

```cpp
#include "personmove.hpp"
#include <iostream>
#include <vector>

int main()
{
    std::vector<Person> coll{"Wolfgang Amadeus Mozart",
                             "Johann Sebastian Bach",
                             "Ludwig van Beethoven"};
    std::cout << "capacity: " << coll.capacity() << '\n';
    coll.push_back("Pjotr Iljitsch Tschaikowski");
}
```

我们会得到以下输出：

```text
COPY Wolfgang Amadeus Mozart
COPY Johann Sebastian Bach
COPY Ludwig van Beethoven
capacity: 3
MOVE Pjotr Iljitsch Tschaikowski
MOVE Wolfgang Amadeus Mozart
MOVE Johann Sebastian Bach
MOVE Ludwig van Beethoven
```

同样，我们首先将初始值拷贝到 vector 中

![](img/7ef3d1ca55bdc192f1cc0929179f3d21_128_0.png)

然而，正如输出的最后三行所示，vector 现在使用移动构造函数将其元素移动到新重新分配的内存中：
