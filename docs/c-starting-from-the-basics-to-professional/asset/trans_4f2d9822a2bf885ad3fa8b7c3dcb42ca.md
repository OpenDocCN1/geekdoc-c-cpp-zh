

这个基本的仿函数类只有一个成员：一个函数调用运算符。这里要记住的主要事情是，函数调用运算符用 `operator()` 表示，并且它的实际参数列表只在初始的一对空括号之后指定。除此之外，这与其他任何运算符函数都一样。

有了这个类定义，你就可以创建自己的第一个函数对象，然后像调用真正的函数一样调用它，如下所示：

```
Less less;                        // 创建一个“小于”仿函数...
const bool is_less = less(5, 6);  // ... 然后“调用”它
std::cout << (is_less ? "5 is less than 6" : "Huh?") << std::endl;
```

当然，被“调用”的并不是对象本身，而是它的函数调用运算符函数。如果你喜欢自虐和让代码变得晦涩难懂，你也可以把 `less(5, 6)` 写成 `less.operator()(5, 6)`。

诚然，创建一个仿函数仅仅为了紧接着调用它并不是很有用。如果你把仿函数用作回调函数，事情就会变得更有趣一些。为了演示这一点，你首先得泛化 Ex19_02 中的 `findOptimum()` 模板，因为目前它只接受函数指针作为其回调参数。当然，专门为 `Less` 类型创建一个额外的重载，会违背一开始就使用带回调的高阶函数的初衷。而且也不存在一个能涵盖所有函数对象类类型的单一类型。因此，泛化 `findOptimum()` 这类函数的最常见方式是声明第二个模板类型参数，并将其用作 `compare` 参数的类型：

```
// Optimum.cpp - 一个用于确定给定向量中最优元素的函数模板
export module optimum;
import <vector>;

export template <typename T, typename Comparison>
const T* findOptimum(const std::vector<T>& values, Comparison compare)
{
    if (values.empty()) return nullptr;

    const T* optimum = &values[0];
    for (size_t i {1}; i < values.size(); ++i)
    {
        if (compare(values[i], *optimum))
            optimum = &values[i];
    }
    return optimum;
}
```

因为 `Comparison` 是一个模板类型参数，现在你可以用任意类型的 `compare` 参数来调用 `findOptimum()`。当然，只有在 `compare` 参数是一个可以用两个 `T&` 参数调用的类函数值时，模板的实例化才能编译通过。而你已经知道，有两类参数可能符合这个要求：

-   `bool (*)(const T&, const T&)` 类型的函数指针（或类似类型，比如 `bool (*)(T, T)`）。因此，如果你把这个新的 `findOptimum<>()` 定义插入到 Ex19_02 中，该示例仍然会和之前一样正常工作。
-   像 `Less` 这样具有相应函数调用运算符类型的函数对象。

我们的下一个示例演示了这两种选项：

```cpp
// Ex19_03.cpp
// 练习使用仿函数作为回调函数
import <iostream>;
import optimum;
import less;

template <typename T>
bool greater(const T& one, const T& other) { return one > other; }

int main()
{
    Less less;

    std::vector numbers{ 91, 18, 92, 22, 13, 43 };
    std::cout << "Minimum element: " << *findOptimum(numbers, less) << std::endl;
    std::cout << "Maximum element: " << *findOptimum(numbers, greater<int>) << std::endl;
}
```

## 标准函数对象

你可以通过向标准库中的许多模板提供一等函数来自定义它们，就像你在示例 Ex19_02 和 Ex19_03 中对 `findOptimum()` 所做的那样。对于常规函数，你大多可以使用普通的函数指针，但对于内建运算符，这就不行了。你不能创建指向内建运算符的指针。当然，快速定义一个函数（如 Ex19_02 中）或仿函数类（Ex19_03 中的 `Less`）来模拟运算符的行为是很容易的，但每次都针对每个运算符这样做很快就会变得非常繁琐。

当然，这也没有逃过标准库设计者的注意。因此，标准库的 `<functional>` 模块定义了一系列函数对象类模板，每个模板对应一个你可能想要传给其他模板的内建运算符。例如，类模板 `std::less<>` 从根本上类似于 Ex19_03 中的 `Less` 模板。在添加了对 `<functional>` 模块的导入之后，你就可以把 Ex19_03 中 `less` 变量的定义替换为下面这个：

```cpp
std::less<int> less;    // 创建一个“小于”仿函数
```

> **提示** 从 C++14 开始，使用 `<functional>` 模块的函数对象类型的推荐方式实际上是省略类型参数，例如下面这样：

```cpp
std::less<> less;       // 创建一个“小于”仿函数
```

`<functional>` 定义的模板采用了更高级的模板编程技术，以确保在没有显式类型参数的情况下定义的仿函数通常与传统方式定义的仿函数行为完全相同，除非在涉及隐式转换的特定情况下。函数对象类型 `std::less<>` 可能比 `std::less<int>` 类型的函数对象产生更高效的代码（或者，举一个更常见的例子，比 `std::less<std::string>` 类型更高效）。不过，详细解释这一点会让我们偏离主题太远。请相信我们：如果你总是简单地省略类型参数，就能保证编译器在所有情况下都能生成最优代码。此外，这还能让你少打一些字，所以这明显是双赢！

表 19-1 列出了完整的模板集合。一如既往，所有这些类型都定义在 `std` 命名空间中。

*表 19-1. `<functional>` 模块提供的函数对象类模板*

| | |
|---|---|
| 比较运算 | `less<>`, `greater<>`, `less_equal<>`, `greater_equal<>`, `equal_to<>`, `not_equal_to<>` |
| 算术运算 | `plus<>`, `minus<>`, `multiplies<>`, `divides<>`, `modulus<>`, `negate<>` |
| 逻辑运算 | `logical_and<>`, `logical_or<>`, `logical_not<>` |
| 位运算 | `bit_and<>`, `bit_or<>`, `bit_xor<>`, `bit_not<>` |

我们可以使用 `std::greater<>` 来替换 Ex19_03 中的 `greater<>` 函数模板。这难道不是很棒吗？

```cpp
std::vector numbers{ 91, 18, 92, 22, 13, 43 };
std::cout << "Minimum element: " << *findOptimum(numbers, std::less<>) << std::endl;
std::cout << "Maximum element: " << *findOptimum(numbers, std::greater<>) << std::endl;
```

这一次，我们在函数调用表达式内部直接创建了 `std::less<>` 和 `std::greater<>` 函数对象作为临时对象，而不是先将它们存储在命名变量中。你可以在 Ex19_03A 中找到这个程序的变体。

## 参数化函数对象

也许你已经注意到，事实上，到目前为止你见过的所有函数对象都没有比普通函数指针更强大。如果定义一个普通函数要容易得多，那为什么还要费尽周折去定义一个带有函数调用运算符的类呢？肯定，函数对象应该不止于此吧？

确实如此。函数对象只有在你开始添加更多成员（无论是变量还是函数）时才会变得真正有趣。基于我们一直用的同一个 `findOptimum()` 示例，假设你想搜索的不是最小或最大的数字，而是最接近某个用户提供的值的数字。使用函数和函数指针，没有干净的方法来实现这一点。想想看：如果只有指针，回调函数体如何能访问用户输入的值？没有干净的方法能把这个值传递给函数。然而，如果你使用类函数对象，你可以通过将任何你想要的信息存储在对象的成员变量中来传递它。最简单的方法是我们直接向你展示如何做到这一点：

```cpp
// Nearer.cpp
// 一个函数对象类，根据两个值与构造仿函数时提供的某个第三个值的接近程度来比较它们
module;             // 全局模块片段，用于包含传统 C 头文件（参见第 11 章）
```

