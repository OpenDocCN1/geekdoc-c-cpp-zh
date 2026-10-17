
```cpp
#include <algorithm>
#include <vector>
#include <iterator>
#include <iostream>

using namespace std;

int main() {
    int intArray[] = {5, 6, 8, 3, 40, 
                      36, 98, 29, 75};

    vector<int> vecList(9);

    ostream_iterator<int> screen(cout, ", ");

    cout << "Line 4: intArray: "; copy(intArray, intArray + 9, screen);
    cout << endl;

    copy(intArray, intArray + 9, vecList.begin());

    cout << "Line 8: vecList: "; copy(vecList.begin(), vecList.end(), screen);
    cout << endl;

    copy(intArray+1, intArray);
    cout << "Line 12: After shifting the elements "
         << " one position to the left, " << endl
         << " intArray: ";
    copy(intArray, intArray + 9, screen);
    cout << endl;

    copy(vecList.rbegin() + 2, vecList.rend(),
         vecList.rbegin());
    cout << "Line 16: After shifting the elements "
         << " down by two positions," << endl
         << " vecList: ";

    copy(vecList.begin(), vecList.end(), screen); //Line 17
    cout << endl;

    return 0;
}
```

# 运行结果

Line 4: intArray: 5 6 8 3 40 36 98 29 75

Line 8: vecList: 5 6 8 3 40 36 98 29 75

Line 12: After shifting the elements one position to the left,

intArray: 6 8 3 40 36 98 29 75

Line 16: After shifting the elements down by two positions,

vecList: 5 5 6 8 3 40 36 98

# 序列容器：deque

本节描述了 `deque` 容器。`deque` 容器被实现为动态数组，使得可以在两端插入元素。因此，`deque` 可以向任何方向扩展。元素也可以在中间插入。在开头或末尾插入元素是很快的，但在中间插入元素是非常耗时的，因为队列中的元素需要进行移动。

定义容器的类名为 `deque`。此外，类 `deque` 的定义以及用于在 `deque` 对象上实现各种操作的函数包含在头文件 `deque` 中。因此，要在程序中使用 `deque`，程序必须包含以下语句：

```cpp
#include <deque>
```

`deque` 类包含几个构造函数。因此，在声明 `deque` 对象时，可以用多种方式进行初始化。表 H-7 描述了声明 `deque` 对象的各种方式。

| 语句 | 描述 |
| --- | --- |
| `deque<elementType> deque;` | 创建一个空的 `deque` 容器 `deg`。调用默认构造函数。 |
| `deque<elementType> deque(otherDeque);` | 创建 `deque` 容器 `deg` 并将其初始化为 `otherDeque` 的元素：`deg` 和 `otherDeque` 类型相同。 |

# 表 H-7 声明 deque 对象的各种方式（续接）

| 语句 | 描述 |
|---|---|
| `deque<elementType> deque(size);` | 创建大小为 `size` 的 `deque` 容器。 |
| `deque<elementType> deque(elem);` | 创建包含一个 `elem` 元素的 `deque` 容器。 |
| `deque<elementType> deque(beg, end);` | 创建范围范围 `[beg, end)` 的 `deque` 容器，`beg` 和 `end` 是迭代器。 |

# 表 H-8 deque 对象可以执行的操作

| 表达式 | 描述 |
|---|---|
| `deque.assign(n, elem)` | 赋值 n 个 `elem`。 |
| `deque.assign(beg, end)` | 赋值范围 `[beg, end)` 中的元素。 |
| `deque.push_front(elem)` | 在开头插入 `elem`。 |
| `deque.push_back(elem)` | 在末尾插入 `elem`。 |
| `deque.pop_front()` | 删除第一个元素。 |
| `deque.pop_back()` | 删除最后一个元素。 |
| `deque.at(index)` | 返回索引为 `index` 处的元素。 |
| `deque[index]` | 返回索引为 `index` 处的元素。 |
| `deque.front()` | 返回第一个元素。 |
| `deque.back()` | 返回最后一个元素。 |

# 示例 H-6

H-6 演示了如何在程序中使用 `deque` 容器。

```cpp
//deque
#include <iostream>
#include <deque>
#include <algorithm>
#include <iterator>

using namespace std;

int main() {
    deque<int> intDeg;
    ostream_iterator<int> screen(cout, " ");

    intDeg.push_back(13);
    intDeg.push_back(75);
    intDeg.push_back(28);
    intDeg.push_back(35);

    cout << "Line 7: intDeg: " << endl;
    copy(intDeg.begin(), intDeg.end(), screen);
    cout << endl;

    intDeg.push_front(0);
    intDeg.push_back(100);

    cout << "Line 12: After adding two more " << endl;
    cout << "elements, one at the front " << endl;
    cout << "and at the back, " << endl;
    cout << "intDeg: " << endl;
    copy(intDeg.begin(), intDeg.end(), screen);
    cout << endl;

    intDeg.pop_front();
    intDeg.pop_back();

    cout << "Line 17: After removing two more " << endl;
    cout << "elements, one from the front " << endl;
    cout << "and from the back, " << endl;
    cout << "intDeg: " << endl;
    copy(intDeg.begin(), intDeg.end(), screen);
    cout << endl;

    return 0;
}
```

# 表 H-10 list 容器的各种特定操作

| 表达式 | 描述 |
| --- | --- |
| `listCont.assign(n, elem)` | 赋值 n 个 elem 的拷贝。 |
| `listCont.assign(beg, end)` | 赋值范围 beg...end-1 内的所有元素。beg 和 end 均为迭代器。 |
| `listCont.push_front(elem)` | 在 `listCont` 的头部插入 `elem`。 |
| `listCont.pop_front()` | 从 `listCont` 中删除第一个元素。 |
| `listCont.front()` | 返回第一个元素。 不检查容器是否为空。 |
| `listCont.back()` | 返回最后一个元素。 不检查容器是否为空。 |
| `listCont.remove(elem)` | 删除所有等于 `elem` 的元素。 |
| `listCont.remove_if(oper)` | 删除所有满足 `oper` 条件为真的元素。 |
| `listCont.unique()` | 如果 `listCont` 中的连续元素具有相同的值，则删除重复项。 |
| `listCont.unique(oper)` | 如果 `listCont` 中的连续元素具有相同的值，且满足 `oper` 为真，则删除重复项。 |
| `listCont.sort()` | 对 `listCont` 的元素进行排序。排序标准为 `<`。 |
| `listCont.sort(oper)` | 对 `listCont` 的元素进行排序。排序标准由 `oper` 指定。 |

# 表 H-10 list 容器的各种特定操作（继续）

| 表达式 | 描述 |
| --- | --- |
| `listCont1.merge(listCont2)` | 假设 `listCont1` 和 `listCont2` 的元素是有序的。此操作将 `listCont2` 的所有元素移动到 `listCont1`。执行此操作后，`listCont1` 中的元素是有序的。此外，执行此操作后，`listCont2` 为空。 |
| `listCont1.merge(listCont2, oper)` | 假设 `listCont1` 和 `listCont2` 的元素根据排序标准 `oper` 有序的。此操作将 `listCont2` 的所有元素移动到 `listCont1`。执行此操作后，`listCont1` 中的元素根据排序标准 `oper` 有有序。 |
| `listCont.reverse()` | 将 `listCont` 的元素进行反转。 |

示例 H-7 展示了如何在 `list` 容器上使用各种操作。

# 示例 H-7

```cpp
//List Container Example
#include <iostream>
#include <list>
#include <iterator>
#include <algorithm>

using namespace std;

int main() {
    list<int> listInt1;
    listInt1.push_back(15);
    listInt1.push_back(93);
    listInt1.push_back(98);
    listInt1.push_back(58);

    cout << "Line 12: intList1: ";
    copy(listInt1.begin(), listInt1.end(), cout);
    cout << endl;

    list<int> listInt2 = listInt1;

    cout << "Line 16: intList2: ";
    copy(listInt2.begin(), listInt2.end(), cout);
    cout << endl;

    listInt1.unique();

    cout << "Line 20: After removing the consecutive duplicates"
         << " intList1: ";
    copy(listInt1.begin(), listInt1.end(), cout);
    cout << endl;

    listInt2.sort();

    cout << "Line 24: After sorting, intList2: ";
    copy(listInt2.begin(), listInt2.end(), cout);
    cout << endl;

    list<int> listInt3;
    listInt3.push_back(13);
    listInt3.push_back(25);
    listInt3.push_back(23);
    listInt3.push_back(198);
    listInt3.push_back(136);

    cout << "Line 32: intList3: ";
    copy(listInt3.begin(), listInt3.end(), cout);
    cout << endl;

    listInt3.sort();

    cout << "Line 36: After sorting, intList3: ";
    copy(listInt3.begin(), listInt3.end(), cout);
    cout << endl;

    listInt2.merge(listInt2);

    cout << "Line 40: After merging intList2 and "
         << "intList3, intList2: " << endl << " ";

    copy(listInt2.begin(), listInt2.end(), cout); //Line 41
    cout << endl; //Line 42

    return 0;
}
```

# 运行结果

Line 12: intList: 23 58 58 58 36 15 93 58

Line 16: intList2: 23 58 58 36 15 93 98 58

Line 20: After removing the consecutive duplicates,

intList: 23 58 36 15 93 98 58

Line 24: After sorting, intList2: 15 23 36 58 58 58 93 98

Line 32: intList3: 13 23 25 136 198

Line 36: After sorting, intList3: 13 23 25 136 198

Line 40: After merging intList2 and intList3, intList2:

13 15 23 25 36 52 58 58 93 98 198

在很大程度上，上述程序的输出是直观的。第 3 行到第 11 行的语句插入了元素 23, 58, 58, 58, 36, 15, 93, 58。

```cpp
int main() {
    stack<int> intStack;
    intStack.push(16);
    intStack.push(8);
    intStack.push(20);
    intStack.push(3);

    cout << "Line 6: The top element of " << "intStack: " << intStack.top() << endl;

    cout << "Line 8: After the pop operation, " << "the top element of intStack: " << intStack.top() << endl;

    cout << "Line 9: intStack elements: ";

    while (!intStack.empty()) {
        cout << intStack.top() << " " << ";"
        intStack.pop();
    }

    cout << endl;
    return 0;
}
```

# 示例

Line 6: The top element of intStack: 3

Line 8: After the pop operation, the top element of intStack: 20

Line 9: intStack elements: 20 8 16

# 队列 (QUEUE)

第 19 章详细讨论了队列这种数据结构。因为队列是一种重要的数据结构，STL 提供了一个类在程序中实现队列。定义队列的类名为 `queue`，包含 `queue` 类定义的头文件名称也为 `queue`。表 H-12 定义了队列容器类支持的各种操作。

1288 | 附录 H：标准模板库 (STL)

# 表 H-12 队列对象的各种操作

| 操作 | 描述 |
|---|---|
| `size` | 返回队列中元素的实际数量。 |
| `empty` | 如果队列为空则返回 true，否则返回 false。 |
| `push(item)` | 将 `item` 的拷贝插入队列中。 |
| `front` | 返回队列中的下一个即第一个元素，但不从队列中移除该元素。该操作被实现为一个返回值的函数。 |
| `back` | 返回队列中的最后一个元素，但不从队列中移除该元素。该操作被实现为一个返回值的函数。 |
| `pop` | 移除队列中的下一个元素。 |
