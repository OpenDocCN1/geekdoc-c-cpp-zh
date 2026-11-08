
```cpp
int main()
{
  std::stack<int> stack;
  for (int i {}; i < 10; ++i)
    stack.push(i);

  std::cout << "The elements coming off the top of the stack:   ";
  while (!stack.empty())
  {
    std::cout << stack.top() << ' ';
    stack.pop();  // pop() is a void function!
  }
  std::cout << std::endl;

  std::queue<int> queue;
  for (int i {}; i < 10; ++i)
    queue.push(i);

  std::cout << "The elements coming from the front of the queue: ";
  while (!queue.empty())
  {
    std::cout << queue.front() << ' ';
    queue.pop();  // pop() is a void function!
  }
  std::cout << std::endl;
}
```

该程序展示了两个适配器的典型用法，先是栈，然后是队列。尽管以相同顺序向两者添加了同样的十个元素，输出结果证实它们会以相反的顺序被取出。

```
The elements coming off the top of the stack:  9 8 7 6 5 4 3 2 1 0
The elements coming from the front of the queue: 0 1 2 3 4 5 6 7 8 9
```

请注意，pop() 函数不返回任何元素。因此，通常必须先使用 top() 或 front() 访问这些元素，具体取决于你使用的是哪个适配器。（毫不意外，顺便说一下，各种序列容器的所有 pop_front() 和 pop_back() 成员也是如此。）

`std::stack<>` 和 `std::queue<>` 只提供少量成员函数——即示例中用到的那些。两者都有常规的 size()、empty() 和 swap() 函数，但也就这些了。正如我们所说，这些适配器的接口是专门为某一种特定用途量身定制的，且仅适用于该用途。

> **提示**  容器适配器通常用于管理表示需要按特定顺序执行的任务的元素。如果所有独立任务都同时堆积起来，那是不可行的。如果调度的是独立任务或连续任务，那么 queue<> 往往是最自然的数据结构。此时任务只需按照请求的顺序执行即可。如果这些任务表示其他已调度或已挂起任务的子任务，那么通常希望所有子任务先完成，再启动或恢复它们的父任务。此时 stack<> 是最简单的方法（注意，C++ 执行函数时也是如此——使用调用栈）。

因此，FIFO 和 LIFO 对大多数简单的任务调度应用都很有用；对于更复杂的场景，可能需要基于优先级的调度。这正是 `std::priority_queue<>` 所提供的，它是我们接下来将简要介绍的容器适配器。

## 优先队列

最后一个容器适配器是 `std::priority_queue<>`，它和 `queue<>` 一样由同一个 `<queue>` 模块定义。你可以把优先队列比作现实夜店中的排队方式；也就是说，某些客人群体可以比其他人先进场。优先级更高的客人——VIP、漂亮女士，甚至夜店老板的傻侄子——会比优先级较低的客人优先。另一个类比是本地超市或公交站的排队，残疾人士和孕妇可以插队。

与其他适配器类似，元素通过 push() 添加到 `priority_queue<>`，并通过 pop() 取出。要访问队列中的下一个元素，请使用 top()。元素离开 `priority_queue<T>` 的顺序由比较仿函数决定。默认情况下使用 `std::less<T>` 仿函数（见第 19 章）。你可以用自己的比较仿函数覆盖它。关于如何使用优先队列的更多细节，请参阅标准库参考。

> **警告**  在日常说法中，通常是具有*最高*优先级的元素优先。然而，在 `priority_queue<>` 中，队列的前端（或者更确切地说，`top()`）默认会是使用 `<` 比较时*最低*的元素。要让具有最高优先级的元素首先上升到 `top()`，可以通过 `std::greater<>` 覆盖默认的比较仿函数。为此，按如下方式实例化模板：`std::priority_queue<T, std::vector<T>, std::greater<T>>`（第一个可选模板类型参数决定底层序列容器）。

## 关联容器

C++ 标准库提供两种所谓的关联容器：集合和映射。我们现在依次讨论两者。

### 集合

集合是一种容器，其中每个元素最多出现一次。向集合中添加第二个与已存储的任一元素相等的元素不会产生任何效果。用一个简单示例最容易说明这一点：

```cpp
// Ex20_03.cpp - Working with sets
import <iostream>;
import <set>;       // For the std::set<> container template

void printSet(const std::set<int>& my_set);  // Print the contents of a set to std::cout

int main()
{
    std::set<int> my_set;

    // Insert elements 1 through 4 in arbitrary order:
    my_set.insert(1);
    my_set.insert(4);
    my_set.insert(3);
    my_set.insert(3);   // Elements 3 and 1 are added twice
    my_set.insert(1);
    my_set.insert(2);

    printSet(my_set);

    std::cout << "The element 1 occurs " << my_set.count(1) << " time(s)" << std::endl;

    my_set.erase(1);    // Remove the element 1 once
    printSet(my_set);

    my_set.clear();     // Remove all elements
    printSet(my_set);
}

void printSet(const std::set<int>& my_set)
{
  std::cout << "There are " << my_set.size() << " elements in my_set: ";
  for (int element : my_set)        // A set, like all containers, is a range
    std::cout << element << ' ';
  std::cout << std::endl;
}
```

执行这段代码会产生以下输出：

```
There are 4 elements in my_set: 1 2 3 4
The element 1 occurs 1 time(s)
There are 3 elements in my_set: 2 3 4
There are 0 elements in my_set:
```

集合容器没有“push”或“pop”成员。相反，你总是通过 insert() 添加元素，并通过 erase() 再次移除它们。你可以添加任意数量的元素，并以任意顺序添加。然而，正如 Ex20_03 清楚展示的那样，第二次添加同一元素确实不会产生任何效果。即使在示例中你两次将值 1 和 3 添加到 my_set，输出也清楚表明这两个元素在容器中只存储一次。

你经常会使用集合容器来管理或收集一组无重复元素。除此之外，它们的主要优势在于集合非常擅长快速检查是否包含给定元素。比方说，这比普通的无序 vector<> 要好得多。这并不奇怪，因为检查是否已经包含某个元素正是集合为了剔除重复项所需要做的事情。要检查给定元素是否包含在集合中，可以使用它的 count() 成员（对于集合容器始终返回 0 或 1；见 Ex20_03）、它的 contains() 成员（返回布尔值；C++20 新增）或它的 find() 成员（返回迭代器）。在让你彻底了解迭代器之后，我们会进一步讨论 find() 函数。

标准库提供两种通用集合容器：`std::set<>` 和 `std::unordered_set<>`。本质上，两者提供完全相同的功能。例如，你可以把 Ex20_03 中的 `std::set<>` 替换为 `std::unordered_set<>`，示例（几乎）仍会以相同方式工作。不过，它们在内部使用非常不同的数据结构来组织数据，尽管目标相同：快速确定是否要插入新元素以及插入到哪里。现在我们更详细地看一下这两种集合——有序集合和无序集合。

> **提示**  除了 `set<>` 和 `unordered_set<>` 之外，标准库还提供 `std::multiset<>` 和 `std::unordered_multiset<>`。与集合容器不同，多重集合容器（也称为包或 msets）可以多次包含同一元素（因此对于这些容器，`count()` 可能返回大于 1 的数字）。它们的关键特性仍然是：多重集合在确定给定元素是否存储在容器中以及存储在哪里方面非常快。

### 有序集合

正如 `unordered_set<>` 这个名字已经透露的那样，常规 `set<>` 的元素始终是有序的。这一点从 Ex20_03 中也显而易见。尽管你以某种任意顺序添加了元素 1 到 4，输出清楚证实容器会以某种方式组织其元素，使它们变得有序。这是有充分理由的：对数据排序可以让你更容易快速找到给定元素——只要想象一下，如果字典中的所有单词都以某种任意顺序打乱，你要找到单词 *反复无常的* 的定义需要多长时间！

> **注意**  对于那些了解数据结构的人来说，`std::set<>` 通常由某种平衡树数据结构（通常是*红黑树*）作为底层支持。除了这能为你带来对数复杂度的 `insert()`、`erase()`、`find()` 和 `count()` 操作之外，通常你几乎不需要了解这些实现细节。

默认情况下，`set<>` 使用 `<` 运算符对所有元素排序。因此，要存储在 `std::set<T>` 中，类 `T` 的元素应重写 `operator<` 或 `operator<=>`（见第 13 章）。不过，我们说的是“默认情况下”，因为你可以通过指定 `set<>` 应使用哪个函数来覆盖其元素排序方式。例如，你可以将 Ex20_03 中 my_set 的定义替换为以下内容：

```
std::set<int, std::greater<>> my_set;
```

然后，my_set 的元素会从最高到最低排序。要打印该集合，你还必须相应地更新 `printSet()` 的签名。要使用 `std::greater<>`，你可能还需要先导入 `<functional>` 模块。

`std::set<>` 类模板的第二个类型参数是可选的（默认是 `std::less<T>`）。你可以指定任意仿函数类型，只要它的二元函数调用运算符比较两个 `T` 元素，并在作为第一个参数传入的元素应排在作为第二个参数传入的元素之前时返回 true。通常，`set<>` 会默认构造相应类型的仿函数，但如有需要，你也可以自己将一个仿函数传给 `set<>` 的构造函数。

