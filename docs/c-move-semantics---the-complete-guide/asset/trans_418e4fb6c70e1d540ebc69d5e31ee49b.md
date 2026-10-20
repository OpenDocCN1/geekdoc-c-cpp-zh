

### 实现移动语义

第三种选择是实现移动操作，使其不破坏类的不变量。

为此，我们必须决定被移动后的对象应该处于什么状态。为了支持 asString() 无需检查值是否存在即可调用 operator*，我们始终需要提供一个值。例如，我们可以有一个静态的“被移动后的值”，并将其赋给那些值被移走的对象：

```cpp
#include <memory>
#include <string>

class SharedInt {
private:
    std::shared_ptr<int> sp;
    // special "value" for moved-from objects:
    inline static std::shared_ptr<int> movedFromValue{std::make_shared<int>(0)};
public:
    explicit SharedInt(int val)
        : sp{std::make_shared<int>(val)} {}
    std::string asString() const {
        return std::to_string(*sp); // OOPS: unconditional deref
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

注意，我们必须 =default 复制特殊成员函数，因为当我们声明了用户自定义的移动特殊成员函数时，它们会被删除。

### 6.4  小结

-   对于每个类，明确被移动后的对象的状态。你必须确保它们至少是可析构的（这通常在不实现特殊成员函数的情况下也能满足）。然而，你的类的使用者可能会期望或要求更多。
-   C++ 标准库函数的要求同样适用于被移动后的对象。
-   生成的移动特殊成员函数可能会使被移动后的对象进入一种违反类不变量的状态。这尤其可能发生在以下情况：
  -   类没有带确定值的默认构造函数（因此没有天然的“被移动后”状态）
  -   成员的值受到限制（如断言）
  -   成员的值相互依赖
  -   使用了具有指针语义的成员（普通指针、智能指针等）
-   如果“被移动后”状态破坏了不变量或使操作无效，你应该使用以下选项之一来修复：
  -   禁用移动语义
  -   修复移动语义的实现
  -   在类内部处理被破坏的不变量，并对外部隐藏它们
  -   通过记录被移动后的对象的约束和前置条件，放宽类的不变量

## 第7章

## 移动语义与 noexcept

当移动语义在 C++11 中即将完成时，我们发现了一个问题：vector 的重分配无法使用移动语义。因此，引入了新的关键字 noexcept。

本章将解释这个问题以及它对 C++ 代码中使用 noexcept 意味着什么。

让我们通过一个小例子来引入这个话题，以说明 noexcept 关键字的作用。

考虑下面的类，它定义了一个带有 string 成员的类型，并实现了复制构造函数和移动构造函数，以便让这些构造函数的调用可见：

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

现在让我们创建并初始化一个 Person 的 vector，然后当存在一个 Person 时再插入它：

basics/person.cpp

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

我们首先将初始值复制到 vector 中（因为容器的 std::initializer_list<> 构造函数按值接受传入的参数）。因此，vector 通常会为三个元素分配内存（在图中，我使用了字符串值的简写）：

![](img/c6f2c4fe3e0701d95a17354ad517147a_126_0.png)

这里重要的是接下来发生的事情：我们使用 push_back() 插入第四个元素，这会产生以下后果：

-   因为 vector 内部需要更多内存，它会分配新内存（比如说，能容纳六个元素），移入第四个字符串（我们创建一个临时 Person，并通过 push_back() 将其移入 vector），但也会将已有元素复制到新内存：

  ![](img/c6f2c4fe3e0701d95a17354ad517147a_126_1.png)

-   在此操作结束时，vector 会销毁旧元素，释放旧内存，并更新其成员：

  ![](img/c6f2c4fe3e0701d95a17354ad517147a_126_2.png)

问题是，为什么 vector 不使用移动构造函数将元素从旧内存移动到新内存？

### 强异常安全保证

vector 重分配不使用移动语义的原因是我们为 push_back() 提供的强异常处理保证：当 vector 重分配过程中抛出异常时，C++ 标准库保证将 vector 回滚到其先前的状态。也就是说，push_back() 提供了一种类似事务的保证：要么成功，要么没有影响。

C++ 标准在 C++98 和 C++03 中能够提供这一保证，因为那时 C++ 只能复制元素。如果在复制元素过程中出现问题，源对象仍然可用。处理异常的内部代码只需销毁到目前为止已创建的副本，并释放新内存，从而将 vector 恢复到先前的状态（C++ 标准库假设并要求析构函数不会抛出异常；否则，它将无法回滚）。

重分配是移动语义的绝佳位置，因为我们从一处将元素移动到另一处。因此，从 C++11 开始，我们希望在此使用移动语义。然而，这样做就会遇到麻烦：如果在重分配过程中抛出异常，我们可能无法回滚。新内存中的元素已经“偷走”了旧内存中元素的值。因此，只销毁新元素是不够的；我们必须将它们移回去。但我们怎么知道移回去不会失败呢？

你可能会说移动构造函数不应该抛出异常。对于 string 来说这可能是正确的（因为我们只是移动整数值和指针），但由于我们要求被移动后的对象处于有效状态，这个状态可能需要内存，这意味着如果我们内存不足，移动就可能会抛出异常（例如，Visual C++ 的基于节点的容器就是这样实现的）。

我们也不能放弃这一保证，因为程序可能已经利用这一特性来避免创建 vector 的备份，而丢失数据可能至关重要（安全问题）。而不再支持 push_back() 对 C++11 的接受来说将是一场噩梦。

最终的决定是：只有当元素类型的移动构造函数保证不抛出异常时，才在重分配时使用移动语义。

### 7.1.2 带 noexcept 的移动构造函数

因此，当我们保证 Person 类的移动构造函数永不抛出异常时，我们的小示例程序的行为会发生变化：

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
```

