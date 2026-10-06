
`remove()` 函数从列表中移除匹配特定元素。使用上一个片段定义的 `numbers` 列表，你可以通过以下语句移除所有等于 22 的元素：

```cpp
numbers.remove(22);
```

`assign()` 函数用两个迭代器指定的对象序列副本或指定次数副本来替换列表的内容。这里有一个示例：

```cpp
int data[] = {10, 22, 4, 56, 89, 77, 13, 9};
list<int> numbers(begin(data), end(data));
numbers.assign(10, 99);                // 用 10 份 99 替换内容
numbers.assign(data + 1, data + 4);    // 用 22 4 56 替换内容
```

`assign()` 函数有两个此处所示的重载版本。第一个版本的参数是替换元素的数量和替换元素本身。第二个版本的参数是迭代器或两个指针，以你已经看到的方式指定序列。

`unique()` 函数将消除列表中相邻的重复元素，如果你先对内容进行排序，应用该函数可以确保所有元素都是唯一的。这里有一个示例：

```cpp
int data[] = {10, 22, 4, 10, 89, 22, 89, 10};
list<int> numbers(begin(data), end(data)); // 10 22 4 10 10 22 89 89
```

```cpp
numbers.sort();
numbers.unique(); // 4 10 10 10 22 22 89 89
 // 4 10 22 89
```

每个操作的结果显示在注释中。

`splice()` 函数允许你从一个列表中移除部分内容并插入另一个列表。显然，两个列表必须存储相同类型的元素。这里是你使用 `splice` 函数的最简单方法：

```cpp
int data[] = {1, 2, 3, 4, 5, 6, 7, 8}; // 1 2 3
list<int> numbers(begin(data), end(data));
```

```cpp
// function_object.h
// 用于识别负值的一元谓词
#pragma once
#include <functional>

template <class T> class is_negative : public std::unary_function<T, bool>
{
public:
    result_type operator()(argument_type& value)
    {
        return value < 0;
    }
};
```

该谓词适用于任何数值类型。该基类模板对于该谓词非常有用，它标准化了参数和返回类型的表示，这在你想让你的函数对象与函数适配器配合使用时是非常重要的。函数适配器允许函数对象与更复杂的函数结合使用。你应该能够看到如何以其他方式定义用于过滤的一元谓词——例如，选择偶数或奇数，或者给定数字的倍数，或者落入给定范围内的数字。

如果你不关心你的谓词是否与函数适配器配合，可以非常容易地在使用基类模板的情况下定义模板：

```cpp
// 用于识别负值的一元谓词
#pragma once
template <class T> struct is_negative
{
public:
    bool operator()(T& value)
    {
        return value < 0;
    }
};
```

这里不需要 `#include <functional>` 指令，因为你没有使用基类模板。这个定义简单且易于理解，但我包含了原始版本，仅仅是为了展示如何在更通用的语境下使用你的谓词，特别是如果你想将其与函数适配器配合使用时。我将使用第一个版本创建示例，但你可以使用任何一个，或者尝试都使用。

为了让示例更有趣，我将包含用于向列表输入数据以及写入列表内容的函数模板。以下是使用你的谓词的程序：

```cpp
// Ex10_0.cpp
// 使用 remove_if() 函数处理列表

#include <iostream>
#include <list>
#include "function_object.h"

using std::cin;
using std::cout;
using std::endl;
using std::list;

// 列出列表内容的模板函数
template <class T>
void listlist(const list<T>& data) {
    for (auto t : data)
        cout << t << " ";
    cout << endl;
}

// 从 cin 读取数据并存储在列表中的模板函数
template <class T>
void loadlist(list<T>& data) {
    T value = T();
    while (cin >> value && value != T()) // 读取非零值
        data.emplace_back(std::move(value));
}

int main() {
    // 处理整数
    list<int> numbers;
    cout << "输入用空格分隔的非零整数。输入 0 结束...";
    cout << endl;
    loadlist(numbers);
    cout << "列表包含：" << endl;
    listlist(numbers);
    listlist(numbers);
    numbers.remove_if(is_negative<int>());

    cout << "应用 remove_if() 函数后，列表包含：";
    cout << endl;
    listlist(numbers);

    // 处理浮点值
    list<double> values;
    cout << "输入用空格分隔的非零浮点值（有些是负数！）";
    cout << "输入 0 结束。" << endl;
    loadlist(values);
    cout << "列表包含：" << endl;
    listlist(values);
    values.remove_if(is_negative<double>());
    cout << "应用 remove_if() 函数后，列表包含：" << endl;
    listlist(values);

    return 0;
}
```

# 序列容器 | 543

这里是该程序的示例输出：

- 输入用空格分隔的非零整数。输入 0 结束。

23 -4 -5 66 67 89 -1 22 34 -34 78 62 -9 99 -19 0

列表包含：

23 -4 -5 66 67 89 -1 22 34 -34 78 62 -9 99 -19

应用 remove_if() 函数后，列表包含：

23 66 89 22 34 78 62 99

- 输入用空格分隔的非零值。输入 0 结束。

2.5 -3.1 5.5 100 -99

列表包含：

2.5 -3.1 5.5 100 -99

应用 remove_if() 函数后，列表包含：

2.5 5.5 100

## 工作原理

输出显示谓词检查了 `int` 和 `double` 类型的值。`remove_if` 函数将谓词应用到列表中的每个元素，并删除谓词返回 `true` 的元素。

`loadlist` 模板函数的体看起来如下：

```cpp
T value = T();
while (cin >> value) { // 读取非零值
    data.emplace_back(std::move(value));
}
```

局部变量定义为 `value`，它是模板的参数，因此它将是你任何想要实例化的类型。输入位于 `while` 循环中，直到你输入零为止，此时 `while` 循环中的条件为假。对 `value` 的右值引用使用 `emplace_back()`。

（注：此处原文中提到局部变量定义为 `t`，但代码中使用的是 `value`，翻译时保持代码逻辑一致）。

跟踪元素的数量。如果你需要知道元素的数量，可以使用 `<algorithm>` 头文件中的 `distance()` 函数获取：

```cpp
cout << "Size = " << distance(begin(words), end(words)) << endl;
```

参数是指定你想要的第一个元素和最后一个元素的迭代器。

## 使用其他序列容器

剩余的序列容器是通过我在在本章开头介绍的容器适配器实现的。我将简要讨论它们中的每一个，并用示例说明它们的操作。

## 队列容器

`queue<T>` 容器通过适配器实现了先进先出（FIFO）的存储机制。你只能向 `deque` 的末尾添加元素，或从头部删除元素。以下是创建队列的一种方式：

```cpp
queue<string> names;
```

这创建了一个存储 `string` 类型元素的队列。默认情况下，`queue<T>` 适配器类使用 `deque<T>` 作为基础，但你可以指定不同的序列容器作为基类，只要它支持 `front()`、`back()`、`push_back()` 和 `pop_front()` 操作。这些函数用于操作队列。队列可以基于 `list` 或 `vector`。你通过第二个模板参数指定底层容器。以下是创建一个基于 `list` 的队列的方法：

```cpp
queue<string, list<string>> names;
```

适配器模板的第二个参数指定了要使用的底层序列容器。适配器类充当底层容器的封装器，本质上将你可以执行的操作范围限制在下表描述的操作中。

| FUNCTION | DESCRIPTION |
| --- | --- |
| back() | 返回队列末尾元素的引用。该函数有两个版本，返回 `const` 引用，另一个返回非 `const` 引用。如果队列为空，返回的值未定义。 |
| front() | 返回队列头部元素的引用。该函数有两个版本，返回 `const` 引用，另一个返回非 `const` 引用。如果队列为空，返回的值未定义。 |
| push() | 将参数指定的元素添加到队列的末尾。 |
| pop() | 移除队列头部的元素。 |
| size() | 返回队列中元素的数量。 |
| empty() | 如果队列为空则返回 true，否则返回 false。 |

注意，表格中没有函数可以为队列容器提供迭代器。访问队列内容的唯一方法是通过 `back()` 或 `front()` 函数。

## 尝试使用队列容器

在这个示例中，我们连续读取一个或多个格言，将它们存储在队列中，然后检索这些格言并输出它们：

```cpp
// Ex10_08.cpp
// 练习队列容器

#include <iostream>
#include <queue>
#include <string>

using std::cin;
using std::cout;
using std::endl;
using std::queue;
using std::string;

int main() {
    queue<string> sayings;
    string saying;
    cout << "Enter one or more sayings. Press Enter to end." << endl;
    while (true) {
        getline(cin, saying);
        if (saying.empty()) {
            break;
        }
        sayings.push(saying);
    }

    cout << "There are " << sayings.size()
         << " sayings in the queue." << endl;
    cout << "The sayings that you entered:" << endl;
    while (!sayings.empty()) {
        cout << sayings.front() << endl;
        sayings.pop();
    }

    return 0;
}
```

以下是该程序的输出示例：

- Enter one or more sayings. Press Enter to end.

- At first you don't succeed, give up.

- A preposition is something you should never end a sentence.

- The bigger they are, the harder they hit.

- A rich man is just a poor man with money.

- Wherever you go, there you are.

- Common sense is not so common.

你输入的队列中有 6 个格言：

- At first you don't succeed, give up.

- A preposition is something you should never end a sentence.

- The bigger they are, the harder they hit.

- A rich man is just a poor man with money.

- Wherever you go, there you are.

- Common sense is not so common.

## 工作原理

你首先创建一个存储 `string` 对象的队列容器：

```cpp
queue<string> sayings;
```

你从标准输入流中读取格言，并在 `while` 循环将它们存储在队列容器中：

```cpp
while (true) {
    getline(cin, saying);
    if (saying.empty())
        break;
    sayings.push(saying);
}
```

这个版本的 `getline()` 函数从 `cin` 读取文本到 `string` 对象 `saying` 中，直到识别到换行符。默认终止符是换行符，如果你想覆盖这一点，可以在 `getline()` 的第三个参数中指定字符。循环继续，直到 `empty()` 函数返回 true，这表示输入了空行。当输入不为空时，将其存储在队列中。

```cpp
cout << "There are " << sayings.size()
     << " sayings in the queue." << endl;

cout << "The sayings that you entered:" << endl;

while (!sayings.empty()) {
    cout << sayings.front() << endl;
    sayings.pop();
}
```

## 优先级容器

优先级队列 容器通过适配器实现了最大堆存储机制。默认情况下，最大的元素始终位于头部。你可以向队列添加元素并移除最大的元素。以下是创建优先级队列的一种方式：

```cpp
priority_queue<int> numbers;
```

这创建了一个存储 `int` 类型元素的优先级队列。默认情况下，`priority_queue<T>` 适配器类使用 `vector<T>` 作为基础，但你可以指定不同的序列容器作为基类，只要它支持 `push()` 和 `pop()` 操作。这些函数用于操作优先级队列。适配器类充当底层容器的封装器，本质上将你可以执行的操作范围限制在下表描述的操作中。

| FUNCTION | DESCRIPTION |
| --- | --- |
| top() | 返回头部元素的引用。该函数有两个版本，返回 `const` 引用，另一个返回非 `const` 引用。如果队列为空，返回的值未定义。 |
| push() | 将参数指定的元素添加到队列。 |
| pop() | 移除头部元素。 |
| size() | 返回队列中元素的数量。 |
| empty() | 如果队列为空则返回 true，否则返回 false。 |

注意，表格中没有函数可以为优先级队列容器提供迭代器。访问优先级队列内容的唯一方法是通过 `top()` 或 `pop()` 函数。

## 尝试使用优先级队列容器

在这个示例中，我们在容器中存储 `Person` 对象，这次 `Person` 类被定义为持有 `string` 类型的名称：

```cpp
// Person.h
// 一个定义人的人的类
#pragma once

#include <iostream>
#include <string>

using std::cout;
using std::endl;
using std::string;

class Person {
public:
    Person(const string& first, const string& second)
    {
```
