

## 6.3 处理破坏的类不变量

```
}
};
```

在这个类中，我们通常确保成员 val 和成员 sval 只是同一个值的两种不同表示。这意味着在该类的实现和使用中，我们通常期望其状态的 int 表示和字符串表示是一致的。然而，如果我们在这里调用一个移动操作，我们会保留值 val，但 sval 不再保证具有 val 的字符串表示。

考虑以下程序：

```cpp
#include "intstring.hpp"
#include <iostream>

int main()
{
	IntString is1{42};
	IntString is2;
	std::cout << "is1 and is2 before move:\n";
	is1.dump();
	is2.dump();
	is2 = std::move(is1);
	std::cout << "is1 and is2 after move:\n";
	is1.dump();
	is2.dump();
}
```

该程序通常有以下输出（不要忘记，被移动的 string 变为空是典型情况但并非保证）：

```
is1 and is2 before move:
[4/2'42']
[0/'0']
is1 and is2 after move:
[4/2' ']
[4/2'42']
```

也就是说，自动生成的移动操作破坏了我们“两个成员始终相互匹配”的不变量。

这个问题有多大？好吧，至少这是一个可能的陷阱。再次，你可能会争辩说在移动之后我们不应该再使用该值（直到我们再次设置值）。然而，程序员可能会期望像 C++ 标准库对象那样的策略，该策略规定对象处于有效但未指定的状态。

事实是，有了相应的 getter，该类不再保证值作为 int 和 string 匹配，这很可能是一个类不变量（隐式或显式声明）。你可能会认为最坏的后果是值（现在未指定）根据使用方式看起来不同，但使用它没有问题，因为它仍然是一个有效的 int 或 string。

然而，依赖此不变量的代码可能会被破坏。该代码可能假设字符串表示至少有一个数字。例如，如果它搜索第一个或最后一个数字，你肯定会找到一个。对于一个被移动的 string，它通常为空，这不再成立。因此，未双重检查字符串值中是否有任何字符的代码，可能会遇到意外的未定义行为。

再次，如何处理这个问题取决于类的设计者。然而，如果你遵循 C++ 标准库的规则，你应该使被移动的对象保持有效状态，这可能意味着你引入一个表示“我没有任何值”的可能状态。

一般来说，当对象的状态具有以某种方式相互依赖的成员时，你必须明确确保被移动的状态处于有效状态。可能被破坏的例子有：

- 我们对同一个值有不同的表示，但其中一些被移动走了。
- 一个成员例如计数器与成员中的元素数量相对应。
- 一个布尔值声称一个字符串值已被验证，但被验证的值被移动走了。
- 用于所有元素的平均值的缓存值仍然存在，但值（位于容器成员中）被移动走了。

再次注意，在 C++11 之前，该类工作正常，当时不支持移动语义。不变量在切换到 C++11 或更高版本并且使用被移动的对象时被破坏。

### 6.3.3 由于被移动的指针类成员导致不变量被破坏

移动操作破坏不变量的第三个原因与具有指针类语义的成员的对象有关，例如（智能）指针。

考虑以下使用 std::shared_ptr<> 共享整数值的类的示例：

```
class SharedInt {
    private:
        std::shared_ptr<int> sp;
    public:
        explicit SharedInt(int val)
            : sp{std::make_shared<int>(val)} {
        }

        std::string asString() const {
            return std::to_string(*sp);    // OOPS: assume there is always an int value
        }
};
```

该类的对象接收一个初始整数值，可以与该对象的副本共享。只要新对象仅被复制，一切都很好：

```
SharedInt si1{42};
SharedInt si2{si1};            // si1 and si2 share the value 42

std::cout << si1.asString() << '\n';  // OK
```

仅被复制时，SharedInt 成员 sp 总是有为其值分配的内存（来自 std::make_shared<>() 或来自复制具有已分配内存的现有共享指针）。

然而，一旦我们使用移动语义，如果我们仍然使用被移动的对象，就会遇到未定义行为：

```
SharedInt si1{42};
SharedInt si3{std::move(si1)};      // OOPS: moves away the allocated memory in si1

std::cout << si1.asString() << '\n';  // undefined behavior (probably core dump)
```

问题在于类内部，我们没有正确处理值可能被移动走的事实，这可能发生，因为默认生成的移动操作会调用共享指针的移动操作，从而将所有权从原始对象移走。这意味着 SharedInt 的被移动状态使成员 sp 处于不再拥有对象的状态，而其成员函数 asString() 并未正确处理这种情况。

你可能会争辩说对具有被移动状态的对象调用 asString() 没有意义，因为你正在使用未指定的值，但至少标准库对其类型保证被移动的类型处于有效状态，以便你可以调用所有没有约束的操作。在用户定义的类型中不提供相同的保证可能会让类型使用者感到惊讶。

从健壮编程的角度来看（避免惊喜、陷阱和未定义行为），我通常建议你遵循 C++ 标准库的规则。也就是说：移动操作不应使对象进入破坏不变量的状态。

在这种情况下，我们必须做以下之一：

- 通过也正确处理所有可能的被移动状态来修复类的所有损坏操作
- 禁用移动语义，以便在复制对象时没有优化
- 显式实现移动操作
- 调整并记录类的不变量（约束/前置条件）或特定操作（例如“对被移动对象调用 asString() 是未定义行为”）

由于分配内存代价昂贵，在这种情况下最好的修复方法可能是正确处理整数值的所有权可能被移动走的事实。这将创建一个与默认构造函数相同的状态，我们可以通过此更改引入。

以下小节演示了此修复和其他代码修复。

## 修复损坏的成员函数

第一个选项，修复所有损坏的操作，本质上意味着我们扩展类的不变量（所有对象的可能状态），以便所有操作都能处理被移动状态。我们仍然必须做出设计决策。例如，当对被移动对象调用 asString() 时（或更一般地，对共享指针不拥有整数值的对象），我们可以：

- 仍然返回一个后备值：

```
class SharedInt {
    ...
    std::string asString() const {
        return sp ? std::to_string(*sp) : "";
    }
    ...
};
```

- 抛出异常：

```
class SharedInt {
    ...
    std::string asString() const {
        if (!sp) throw ...
        return std::to_string(*sp);
    }
    ...
};
```

- 在调试模式下强制运行时错误：

```
class SharedInt {
    ...
    std::string asString() const {
        assert(sp);
        return std::to_string(*sp);
    }
    ...
};
```

## 禁用移动语义

第二个选项是禁用移动语义，以便只能使用复制语义。我们之前描述了如何禁用移动语义。你必须 user-declare 另一个特殊成员函数。通常，你 =default 复制特殊成员函数：

```
class SharedInt {
    ...
    SharedInt(const SharedInt&) = default;      // disable move semantics
    SharedInt& operator=(const SharedInt&) = default;  // disable move semantics
    ...
};
```
