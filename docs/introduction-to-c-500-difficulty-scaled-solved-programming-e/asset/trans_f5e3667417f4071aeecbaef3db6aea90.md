

# 848 C++ 简介

```cpp
/* 如果我们想声明迭代器变量，可以写
list<int>::iterator it; 为了简单起见，我们使用 auto 关键字。 */
lst.insert(lst.begin(), arr, arr+5);
cout << "List after insert: ";
for(auto it = lst.begin(); it != lst.end(); ++it)
    cout << *it << ' ';

/* 我们也可以使用 for-range 循环。
for(const auto& it : lst)
    cout << it << ' ';*/

lst.remove(2);
cout << "\nlist after remove: ";
for_each(lst.begin(), lst.end(), show);
lst.unique();
cout << "\nlist after unique: ";
for_each(lst.begin(), lst.end(), show);

lst.pop_front();
lst.push_back(6);
lst.push_back(5);
lst.push_front(7);
lst.sort();
cout << "\nlist after sorting: ";
for_each(lst.begin(), lst.end(), show);

return 0;

void show(int k)
{
    cout << k << ' ';
}
```

`insert()` 将元素插入到迭代器指示的位置。`remove()` 删除所有与参数相等的元素。`unique()` 删除所有连续的重复元素。它在每组相同的元素中只保留第一个元素。`pop_front()` 删除列表的第一个元素。`push_front()` 在列表开头添加元素，而 `push_back()` 则将元素添加到当前元素的末尾。`sort()` 对列表进行排序。如果我们先使用 `sort()` 后使用 `unique()`，则每个元素只会出现一次。程序使用了两种方式来显示列表：迭代器和 `for_each()`。最后，程序显示了：

```
List after insert: 2 2 1 3 1 1
List after remove: 3 1 3 1 1
List after unique: 3 3 1
List after sorting: 1 1 3 5 6 7
```

注意，我们之前看到的非成员函数 `sort()` 需要随机访问迭代器，我们无法使用它。因此，我们使用 list 的成员函数 `sort()`。

# 容器适配器 (Container Adaptors)

容器适配器构建在容器之上，并根据自身的需求调整其功能。容器适配器为封装容器提供一组有限的服务，并针对特定用途定制。例如，`stack` 容器虽然基于 `deque`，但它只允许在栈顶插入和删除元素。它们没有迭代器，也不支持使用索引符号进行访问。标准的容器适配器有 `queue`、`priority_queue` 和 `stack` 模板类。让我们简单了解一下它们。

# queue 模板类

`queue` 模板类实现了一个 FIFO（先进先出）队列，其中元素被插入到队列末尾并从头部提取。该实现支持队列的基本功能。我们可以在队列末尾添加元素、删除第一个元素、查找第一个和最后一个元素的值、检查队列是否为空以及查找存储元素的数量。不支持对元素进行访问，也不支持遍历队列。使用 `queue` 必须包含 `<queue>` 头文件。让我们来看一个示例：

```cpp
#include <iostream> // 示例 26.10
#include <queue>
int main() {
    std::queue<int> q;

    q.push(1);
    q.push(2);
    std::cout << " Front: " << q.front();
    std::cout << " End: " << q.back();
    q.pop();
    std::cout << " Size: " << q.size();
    return 0;
}
```

`push` 将元素添加到队列的末尾。`front()` 返回第一个元素的值，`back()` 返回最后一个元素的值。`pop()` 返回第一个元素，`size()` 返回队列中元素的数量。因此，程序显示：Front: 1 End: 3 Size: 2

# priority_queue 模板类

`priority_queue` 模板类与 `queue` 类似。它们的主要区别在于在 `priority_queue` 中，元素根据某些优先级进行排序。默认优先级基于使用 `<` 运算符对元素进行比较。存储在队列前面的元素是最大的。例如：

```cpp
priority_queue<int> q;
q.push(20);
q.push(10);
q.push(30);
int i = q.top();
```

`top()` 返回队列的第一个元素，即 30。如果我们想更改排序顺序，可以将所需的方法作为第三参数添加。第二个参数表示用于存储元素的底层容器的类型。例如，如果我们写：

```cpp
priority_queue<int, vector<int>, greater<int>> q;
```

排序将是降序的。因此，第一个元素将是 10。我们稍后会讨论 `greater<>`。

# stack 类类

`stack` 类实现了一个 LIFO（后进先出）栈，元素仅从容器的一端进行插入和提取。该实现支持栈的基本功能，我们可以在栈顶添加元素、从栈顶删除元素、查找栈顶元素的值。使用 `stack` 必须包含 `<stack>` 头文件。让我们来看一个示例：

```cpp
#include <iostream> // 示例 26.11
#include <stack>
int main() {
    std::stack<int> s;

    s.push(10);
    s.push(20);
    s.push(30);
    std::cout << "Top: " << s.top() << endl;
    s.pop();
    std::cout << "Top: " << s.top() << endl;
    std::cout << "Size: " << s.size() << endl;
    return 0;
}
```

`push` 将元素添加到栈的顶部。`top()` 返回栈顶元素的值。`pop()` 从栈顶删除元素。`size()` 返回栈中元素的数量。因此，程序显示：Top: 30 Top: 20 Size: 2

# 关联容器 (Associative Containers)

关联容器设计用于按排序顺序存储元素。当我们需要快速搜索时，它们非常有用。它们通常使用平衡二叉搜索树实现。`set` 容器存储元素，其中每个元素都是唯一的。同样，`map` 容器存储键值对，其中每个键都是唯一的。标准的关联容器有 `set`、`multiset`、`map` 和 `multimap`。

# set 类

`set` 容器存储元素，其中每个元素都是唯一的。元素按排序存储。默认情况下，`set` 使用 `<` 运算符对元素进行排序。`set` 支持双向迭代器。让我们来看一个示例：

```cpp
#include <iostream>
#include <string>
#include <set>
#include <algorithm>
using namespace std;

void show(const string& s);

int main() {
    set<string> s = {"car", "the", "get", "sea", "sky"};
    set<string>::iterator it;

    cout << "Set after init: " << endl;
    for (it = s.begin(); it != s.end(); ++it)
        cout << *it << " ";

    s.insert("new");
    cout << "\nSet after insert: " << endl;
    for_each(s.begin(), s.end(), show);

    it = s.find("sky");
    s.erase(it);
    cout << "\nSet after erase: " << endl;
    for_each(s.begin(), s.end(), show);
    return 0;
}

void show(const string& s) {
    cout << s << endl;
}
```

当我们创建一个 `set` 对象时，需要指定它包含的键的类型（例如 `string`）。`insert()` 将参数插入容器中。`find()` 返回一个指向参数存储位置的迭代器（如果找到）。`erase()` 删除迭代器指示的元素。

# map 模板类

`map` 容器包含由键值和关联映射数据组合成的元素。它在应用程序中非常有用

