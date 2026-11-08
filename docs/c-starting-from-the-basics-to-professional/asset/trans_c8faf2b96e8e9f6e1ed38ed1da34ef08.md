
当然，迭代器能做的远不止访问容器的第一个元素。你可能还记得第 6 章讲过，指针支持算术运算 `++`、`--`、`+`、`-` 以及 `+=`、`-=`，你可以用这些运算在数组元素之间移动到下一个（或上一个）元素。使用 `vector<>` 迭代器的方式与此完全相同。下面是一个例子：

```cpp
++my_iter;                         // Move my_iter to the next element
std::cout << *my_iter << std::endl; // b

my_iter += 2;                       // Move my_iter two elements further
std::cout << *my_iter-- << std::endl; // d
std::cout << *my_iter << std::endl;   // c (iterator altered using the post-decrement
                                      // operator in the previous statement)

auto copy( my_iter );               // Create a copy of my_iter (pointing at c)
my_iter += 2;                       // Move my_iter two elements further
std::cout << *copy << std::endl;    // c (copy not affected by moving my_iter)
std::cout << *my_iter << std::endl; // e
std::cout << my_iter - copy << std::endl; // 2
```

这段代码的完整版本见 Ex20_06，到这里它应该已经不言自明了，因为所有这些都与使用指针完全类似。我们示例中的最后一行甚至也是如此，尽管它可能不像其他几行那样显而易见。也就是说，两个 `vector` 迭代器相减会得到一个有符号整数类型的值，表示这两个迭代器之间的距离。

> **提示** 迭代器还提供成员访问运算符（非正式地称为箭头运算符）`->`，用于访问其所指元素的成员变量或成员函数。也就是说，假设 `string_iter` 是一个指向 `std::string` 类型元素的迭代器；那么 `string_iter->length()` 就是 `(*string_iter).length()` 的简写——同样与指针的情况一样。本章后面我们会看到更多具体示例。

## 迭代器的不同类型

上一小节示例中使用的迭代器是所谓的随机访问迭代器。在所有迭代器类别中，随机访问迭代器提供的操作最丰富。标准容器返回的所有迭代器都支持运算符 `++`、`*` 和 `->`，以及 `==` 和 `!=`。但除此之外，还存在一些差异。所有限制都可以从各种容器底层数据结构的性质轻松解释：

- `std::forward_list<>` 的迭代器不支持 `--`、`-=` 或 `-`。原因当然在于，迭代器没有高效的方式回到前一个元素。单链表中每个节点只有一个指向链表中下一个元素的指针。这类迭代器称为*前向迭代器*。其他可能只支持前向迭代器的容器是无序关联容器。

- 另一方面，`std::list<>` 的迭代器确实支持 `--` 递减运算符（包括前置和后置递减）。在双向链表中回到前一个节点是轻而易举的。不过，一次跳转多个元素仍然无法高效完成。为了不鼓励这种用法，`std::list<>` 迭代器不提供例如 `+=`、`-=`、`+` 或 `-` 运算符。有序关联容器的迭代器也有同样的限制，因为遍历其底层树数据结构的节点类似于遍历双向链表的节点。这一类迭代器称为*双向迭代器*——原因显而易见。

- 唯一提供 `+=`、`-=`、`+`、`-` 和 `[]`，以及比较运算符 `<`、`<=`、`>`、`>=` 和 `<=>` 的迭代器是随机访问迭代器。要求提供随机访问迭代器的容器只有随机访问序列容器（`std::vector<>`、`std::array<>` 和 `std::deque<>`）。

> **注意** 只有在查阅标准库参考文档时，了解和理解这些术语才变得重要，尤其是本章后面讨论的泛型算法库部分。每个算法模板的参考文档都会说明它期望哪种类型的迭代器作为输入——前向迭代器、双向迭代器还是随机访问迭代器。

这三类迭代器构成一个层次结构。也就是说，每个随机访问迭代器同时也是有效的双向迭代器，每个双向迭代器同时也是前向迭代器。因此，对于例如需要前向迭代器的算法，你当然也可以传入随机访问迭代器。为完整起见，标准库参考文档在此语境下还可能使用输入迭代器和输出迭代器这两个术语。这些是更偏理论的概念，指的是要求比前向迭代器更少的迭代器。在实践中，标准容器创建的每个迭代器因此始终是有效的输入迭代器或输出迭代器。

> **注意** 三个容器适配器——`std::stack<>`、`std::queue<>` 和 `std::priority_queue<>`——根本不提供任何迭代器——连前向迭代器也没有。它们的元素只能通过 `top()`、`front()` 或 `back()` 函数（视适用情况而定）访问。

## 遍历容器元素

从第 6 章中，你知道如何使用指针和指针算术来遍历数组。例如，要打印数组中的所有元素，可以使用下面的循环：

```cpp
int numbers[] { 1, 2, 3, 4, 5 };
for (int* pnumber {numbers}; pnumber < numbers + std::size(numbers); ++pnumber)
{
    std::cout << *pnumber << ' ';
}
std::cout << std::endl;
```

你可以用完全相同的方式遍历 vector 的所有元素：

```cpp
std::vector numbers{ 1, 2, 3, 4, 5 };  // Deduced type: std::vector<int>
for (auto iter {numbers.begin()}; iter < numbers.begin() + numbers.size(); ++iter)
{
    std::cout << *iter << ' ';
}
std::cout << std::endl;
```

这个循环的问题在于它使用了两个随机访问迭代器独有的操作：`<` 和 `+`。因此，如果 numbers 的类型是例如 `std::list<int>` 或 `std::set<int>`，这个循环就无法编译。因此，表达同一个循环更常规的方式如下：

```cpp
for (auto iter {numbers.begin()}; iter != numbers.end(); ++iter)
{
    std::cout << *iter << ' ';
}
```

这个新循环与我们之前使用的循环等价，只是这一次它适用于任何标准容器。从概念上讲，容器的 `end()` 成员返回的迭代器指向“最后一个元素之后的位置”。因此，一旦迭代器递增到与容器的 `end()` 迭代器相等——也就是说，一旦迭代器递增越过容器的最后一个元素——你就应当明确终止循环。虽然此时会发生什么是未定义的，但解引用指向实际容器边界之外的迭代器不可能有什么好结果。

> **提示** 在 C++ 中，通常使用 `iter != numbers.end()` 而不是 `iter < numbers.end()`，因为前向迭代器和双向迭代器不要求支持通过 `<` 进行比较。通常也应使用 `++iter` 而不是 `iter++`，因为前置递增运算符往往更高效（回想第 13 章，后置递增运算符通常必须先创建并返回迭代器的副本，然后再将其移动到下一个元素）。

下面的示例使用与此完全相同的循环来遍历 `list<>` 中包含的所有元素：

```cpp
// Ex20_07.cpp
// Iterating over the elements of a list<>
#include <iostream>
#include <list>

int main()
{
    std::cout << "Enter a sequence of positive numbers, terminated by -1: ";

    std::list<unsigned> numbers;

    while (true)
    {
        signed number{-1};
        std::cin >> number;
        if (number == -1) break;
        numbers.push_back(static_cast<unsigned>(number));
    }

    std::cout << "You entered the following numbers: ";
    for (auto iter {numbers.begin()}; iter != numbers.end(); ++iter)
    {
        std::cout << *iter << ' ';
    }
    std::cout << std::endl;
}
```

一次可能的会话可能如下所示：

```text
Enter a sequence of positive numbers, terminated by -1: 4 8 15 16 23 42 -1
You entered the following numbers: 4 8 15 16 23 42
```

当然，每个容器本身也是一个范围，而范围可以用于基于范围的 for 循环（参见第 5 章）。因此，例如 Ex20_07 中的 for 循环可以替换为下面这个简单得多的基于范围的 for 循环：

```cpp
for (auto number : numbers)
{
    std::cout << number << ' ';
}
```

> **提示** 要遍历容器中的所有元素，应始终使用基于范围的 for 循环。只有当你明确需要在循环体中进行更高级的处理而访问迭代器，或者只想遍历容器元素的子范围时，才应使用更冗长、更复杂的基于迭代器的循环。

稍后我们会看到循环体需要访问迭代器的示例。

## const 迭代器

到目前为止，我们使用的所有迭代器都是所谓的可变（或非 const）迭代器。你可以通过解引用可变迭代器来修改它所指向的元素，或者对于类类型的元素，通过其成员访问运算符 `->` 来修改。下面是一个例子：

```cpp
// Ex20_08.cpp
// Altering elements through a mutable iterator
import <iostream>;
import <vector>;
import box; // From Ex11_04

int main()
{
    std::vector boxes{ Box{ 1.0, 2.0, 3.0 } }; // A std::vector<Box> containing 1 Box

    auto iter{ boxes.begin() };
    std::cout << iter->volume() << std::endl;  // 6 == 1.0 * 2.0 * 3.0
```
