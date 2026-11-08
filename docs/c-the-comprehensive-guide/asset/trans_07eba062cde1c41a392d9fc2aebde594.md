
最后的两个 `for` 循环通过为每两个数组调用 `compare` 来成对比较数组 a、b 和 c。然后 `compare` 将所有比较运算符的结果以文本形式写出，因此你会得到如下输出（此处节选）：

```
{10 10 10 10 } compared with {10 10 10 10 } is <=, >=, ==,
{10 10 10 10 } compared with {20 5 5 5 } is <=, >=, !=,
{10 10 10 10 } compared with {10 10 5 21 } is >, >=, !=,
{20 5 5 5 } compared with {10 10 10 10 } is >, >, !=,
{20 5 5 5 } compared with {20 5 5 5 } is <=, >=, ==,
{20 5 5 5 } compared with {10 10 5 21 } is >, >=, !=,
{10 10 5 21 } compared with {10 10 10 10 } is <, <=, !=,
{10 10 5 21 } compared with {20 5 5 5 } is <, <=, !=,
{10 10 5 21 } compared with {10 10 5 21 } is <=, >=, ==
```

## 24.6.5 “deque”

*双端队列*与向量非常相似。它放弃了连续存放元素的保证，因此不提供 data、capacity，也没有 reserve。然而，除了向量已有的功能之外，它还能在前端以 O(1) 时间高效地添加和移除元素，使用 `push_front`、`emplace_front`、`pop_front`，从 C++23 开始还有 `append_range` 和 `prepend_range`。

对 deque 能做的最明显的事情之一——也是它名字的由来——是在一端添加元素，同时在另一端移除元素。这就是*先进先出*（FIFO）原则。

```cpp
// https://godbolt.org/z/Ee5AnM9as
#include <deque>
#include <iostream>
#include <string>
#include <cctype>    // toupper
#include <iomanip>   // boolalpha
using namespace std;

bool isPalindrome(string_view word) {
    // check from both ends simultaneously
    deque<char> deq{};
    for(char ch : word) {
        deq.push_back(toupper(ch));    // uppercase
    }
    auto ok = true;
    while(deq.size()>1 && ok) {
        if(deq.front() != deq.back()) {
            ok = false;
        }
        deq.pop_front();                         // Hello deque!
        deq.pop_back();
    }
    return ok;
}

int main() {
    cout << boolalpha; // Print 'true' and 'false' instead of '1' and '0'
    cout << isPalindrome("Abrakadabra") << '\n';    // false
    cout << isPalindrome("Kajak") << '\n';          // true
    cout << isPalindrome("EvilOlive") << '\n';      // true
    cout << isPalindrome("Aibohphobia") << '\n';    // true
    cout << isPalindrome("Madam") << '\n';          // true
    cout << isPalindrome("") << '\n';               // true
}
```

**清单 24.39** 我们从前后成对移除元素并进行比较。

*回文*是正读反读都相同的单词。该程序检查单词是否具有此属性。在循环中，`isPalindrome` 检查首字母和末字母是否相同，持续进行直到发现差异。然后它从两端各移除一个字母，这正是 `pop_front` 发挥作用的地方，而它只在 deque 中可用。

是的，使用索引循环我们本可以在 `word` 中直接读取和比较，但这样我可以简洁地演示 deque。而使用 C++20 的范围，它甚至更优雅：

```cpp
namespace rs = std::ranges; namespace vs = std::ranges::views;
bool isPalindrome(const string_view word) {
    return rs::equal(word, word | vs::reverse, rs::equal_to{}, ::toupper,
        ::toupper);
}
```

`equal` 是一个范围算法，`reverse` 是一个视图。`equal_to` 本来就是默认参数，但两个 `toupper` 投影在比较之前应用于范围中的元素。

deque 的典型应用包括：

- 一个调度器，将新任务添加到队列后端，并从队列前端移除已完成的任务。
- 一个有限长度的撤销历史，已执行的操作插入到前端，当需要撤销时从那里移除，同时在后端丢弃元素以限制历史的深度。
- 使用正则表达式进行模式匹配的文本搜索，或通过模拟非确定性有限自动机来实现。非确定性转移被放入双端队列中进行处理。

我将介绍 deque 的所有方法以及最有用的自由函数和其他工具。其中许多与 `vector` 类似，在这些情况下我会简要说明。你可以在第 24.6.3 节中找到关于 `vector` 相应特性的直接可迁移的详细讨论。

`deque` 不像 `vector` 那样为其容量提供接口。因此，`reserve` 和 `capacity` 方法不像在 `vector` 中那样可用。

因为 deque 在其他方面与 vector 非常相似，请参考那里的示例。为了省去你翻阅页面的麻烦，我在清单 24.40 中包含了 deque 的一些关键操作。

```cpp
// https://godbolt.org/z/d3ExcWP4a
#include <deque>
#include <iostream>
#include <iterator> // ostream_iterator
#include <algorithm> // copy
using namespace std;
ostream& operator<<(ostream& os, int val) { return os << val << '\n'; }
int main() {
    deque<int> d{4, 6};              // Create deque<int> with elements
    // Insertion
    d.push_front(3);                 // at the front: efficient
    d.insert(d.begin()+2, 5);        // in the middle: slow
    d.push_back(7);                  // at the end: efficient
    // Access
    cout << d.front();               // from the front: efficient
    cout << d[3];                    // in the middle: efficient
    cout << d.back();                // from the end: efficient
    // Size
    cout << d.size();                // read size
    d.resize(4);                     // resize (or extend)
    // Iterators
    copy(d.begin(), d.end(), ostream_iterator<int>(cout, " "));
    cout << '\n';                   // Output: 3 4 5 6
    // Remove
    d.pop_front();                  // at the front: efficient
    d.erase(d.begin()+1);            // in the middle: slow
    d.pop_back();                   // at the end: efficient
    d.clear();                      // clear
}
```

**清单 24.40** “deque”能做什么！

请注意我在清单 24.12 之后的方框中对 `<<` 的评论。

### 初始化

初始化 deque 的方式与 vector 完全相同：使用无参默认构造函数、初始化器列表、指定初始大小、一对迭代器，或另一个容器进行复制/移动。从 C++23 开始，还支持使用 `from_range` 进行初始化。

### 赋值

`assign` 方法与 vector 中一样，具有与构造函数相同的选项。使用 `operator=` 可以通过复制和移动重新赋值。使用 `swap`，你可以在 O(1) 时间内交换两个 deque 的内容。从 C++23 开始，`assign_range` 也可用。

### 插入

与 vector 相比，deque 可以高效地在前后两端插入元素：

- **在两端高效追加**
  与 vector 一样，deque 也有用于在尾部追加的 `push_back` 和 `emplace_back`。对于前端，有 `push_front` 和 `emplace_front`，它们同样以 O(1) 最优速度运行。从 C++23 开始，你还可以使用 `append_range` 和 `prepend_range` 高效地追加范围。
- **在任意位置插入**
  这里与 vector 没有区别。使用 `emplace` 或 `insert` 在某个位置插入需要复制或移动许多元素，因此耗时 O(n)。`insert_range` 方法从 C++23 开始可用。

### 删除

与 vector 不同，你可以使用 deque 高效地从前端移除元素：

- **所有元素**
  `clear()` 从 deque 中移除所有元素。
- **最后一个或第一个元素**
  `pop_back()` 对 deque 的作用与 vector 相同；使用 `pop_front()` 以 O(1) 从前端移除。
- **单个任意元素**
  `iterator erase(const_iterator where)` 像在 vector 中一样以 O(n) 删除单个元素。
- **范围**
  `iterator erase(const_iterator from, const_iterator to)` 像在 vector 中一样以 O(n) 删除 `from` 和 `to` 之间的所有元素。

## 24.6.6 “list”

有了 `list`，情况变得更有趣了。虽然许多熟悉的方法再次出现，这些方法我已经通过 `vector` 介绍过，但也有一些有趣的差异。对于某些例子——尤其是与迭代器相关的——你仍然可以参考第 24.6.3 节，但在这里你会看到 `list` 的特殊之处。

`list` 将元素存储在一个双向链表中。这意味着每个元素都独立于其他元素存储在内存中的某个位置。元素不是一次性全部分配，而是逐个分配。例如，如果元素很大，这是一个优势，因为不会同时为许多元素预留空间。然而，对于许多小元素，这可能是一个缺点，因为一次内存请求会消耗系统的内存和时间。

每个元素都带有两个指针，一个指向前驱，另一个指向后继。这是额外的内存，例如 `vector` 并不需要，但它允许你通过简单地将元素“挂在两个元素之间”来在 `list` 中的任何位置插入元素；不需要像 `vector` 那样进行移动操作。即使在结尾或开头追加时，整个容器的内容也不必偶尔移动到一个新的、更大的空间。

链接指针是遍历 `list` 的唯一方式。通过索引直接寻址是不可能的。你可以通过 `begin()` 和 `end()` 获得双向迭代器，然后使用 `++` 和 `--` 遍历元素。因此，从 `list` 生成的范围也只能是双向的，而不能随机访问。

### 初始化

`list` 定义了与 `vector` 和 `deque` 完全相同的构造函数。这意味着你可以使用无参默认构造函数创建空列表，可以进行完整的复制或移动，还可以使用用若干相同值的副本进行初始化、初始化器列表、来自另一个容器的迭代器对，以及从 C++23 开始的 *from_range* 构造函数。`swap` 高效地交换整个列表。

### 赋值

`operator=` 既可以复制也可以移动另一个 `list` 的内容。用于重新初始化的 `assign` 对若干相同元素副本、初始化器列表以及来自另一个容器的迭代器对进行了重载。`assign_range` 从 C++23 开始可用。

### 访问

没有基于索引的访问。最好使用迭代器。直接元素访问仅对 `list` 的两端有效：
