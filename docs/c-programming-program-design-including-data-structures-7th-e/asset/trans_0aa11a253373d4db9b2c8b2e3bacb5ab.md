
## 表 21-9 声明 `list` 对象的各种方式

| 语句 | 描述 |
|---|---|
| `list<elementType> listCont;` | 创建空的 `list` 容器 `listCont`。（调用默认构造函数。） |
| `list<elementType> listCont(otherList);` | 创建 `list` 容器 `listCont`，并将其初始化为 `otherList` 的元素。`listCont` 和 `otherList` 类型相同。 |
| `list<elementType> listCont(size);` | 创建大小为 `size` 的 `list` 容器 `listCont`。`listCont` 使用默认构造函数初始化。 |
| `list<elementType> listCont(n, elem);` | 创建大小为 `n` 的 `list` 容器 `listCont`。`listCont` 使用元素 `elem` 的 `n` 个副本初始化。 |
| `list<elementType> listCont(beg, end);` | 创建 `list` 容器 `listCont`。将 `listCont` 初始化为范围 `[beg, end)` 内的元素，即 `beg...end-1` 范围内的所有元素。`beg` 和 `end` 均为迭代器。 |

表 21-5 描述了所有容器共有的操作。表 21-6 描述了所有顺序容器共有的操作。除这些共有操作外，表 21-10 还描述了 list 容器特有的操作。实现该操作的函数名以粗体显示。

在表 21-10 中，`listCont` 是类型为 list 的容器。

## 表 21-10 `list` 容器特有的各种操作

| 表达式 | 描述 |
| --- | --- |
| `listCont.assign(n, elem)` | 赋值 `elem` 的 n 个副本。 |
| `listCont.assign(beg, end)` | 赋值范围 `beg...end-1` 中的所有元素。`beg` 和 `end` 均为迭代器。 |
| `listCont.push_front(elem)` | 在 `listCont` 的开头插入 `elem`。 |
| `listCont.pop_front()` | 从 `listCont` 中删除第一个元素。 |
| `listCont.front()` | 返回第一个元素。（不检查容器是否为空。） |
| `listCont.back()` | 返回最后一个元素。（不检查容器是否为空。） |
| `listCont.remove(elem)` | 删除所有等于 `elem` 的元素。 |
| `listCont.remove_if(oper)` | 删除所有使 `oper` 为真的元素。 |
| `listCont.unique()` | 如果 `listCont` 中的连续元素具有相同值，则删除重复项。 |
| `listCont.unique(oper)` | 如果 `listCont` 中的连续元素具有相同值，则删除使 `oper` 为真的重复项。 |
| `listCont1.splice(pos, listCont2)` | 将 `listCont2` 的所有元素移动到 `listCont1` 中由迭代器 `pos` 指定的位置之前。此操作后，`listCont2` 为空。 |
| `listCont1.splice(pos, listCont2, pos2)` | 将 `listCont2` 中从 `pos2` 开始的所有元素移动到 `listCont1` 中由迭代器 `pos` 指定的位置之前。 |
| `listCont1.splice(pos, listCont2, beg, end)` | 将 `listCont2` 中范围 `beg...end-1` 内的所有元素移动到 `listCont1` 中由迭代器 `pos` 指定的位置之前。`beg` 和 `end` 均为迭代器。 |
| `listCont.sort()` | 对 `listCont` 的元素排序。排序标准为 `<`。 |
| `listCont.sort(oper)` | 对 `listCont` 的元素排序。排序标准由 `oper` 指定。 |
| `listCont1.merge(listCont2)` | 假设 `listCont1` 和 `listCont2` 的元素已排序。此操作将 `listCont2` 的所有元素移动到 `listCont1` 中。此操作后，`listCont1` 中的元素有序。此外，此操作后，`listCont2` 为空。 |
| `listCont1.merge(listCont2, oper)` | 假设 `listCont1` 和 `listCont2` 的元素已按排序标准 `oper` 排序。此操作将 `listCont2` 的所有元素移动到 `listCont1` 中。此操作后，`listCont1` 中的元素按排序标准 `oper` 有序。 |
| `listCont.reverse()` | 反转 `listCont` 中的元素。 |

例 21-8 说明了如何使用 list 容器上的各种操作。

## 例 21-8

```cpp
// List Container Example
#include <iostream>
#include <list>
#include <iterator>
#include <algorithm>

using namespace std;

int main()
{
    list<int> intList1, intList2, intList3, intList4;     // line 1

    ostream_iterator<int> screen(cout, " ");              // line 2

    intList1.push_back(23);                               // line 3
    intList1.push_back(58);                               // line 4
    intList1.push_back(58);                               // line 5
    intList1.push_back(58);                               // line 6
    intList1.push_back(36);                               // line 7
    intList1.push_back(15);                               // line 8
    intList1.push_back(93);                               // line 9
    intList1.push_back(98);                               // line 10
    intList1.push_back(58);                               // line 11
    cout << "Line 12: intList1: ";                        // line 12
    copy(intList1.begin(), intList1.end(), screen);       // line 13
    cout << endl;                                         // line 14

    intList2 = intList1;                                  // line 15

    cout << "Line 16: intList2: ";                        // line 16
    copy(intList2.begin(), intList2.end(), screen);       // line 17
    cout << endl;                                         // line 18

    intList1.unique();                                    // line 19

    cout << "Line 20: After removing the consecutive "
         << "duplicates," << endl
         << "        intList1: ";                         // line 20
    copy(intList1.begin(), intList1.end(), screen);       // line 21
    cout << endl;                                         // line 22

    intList2.sort();                                      // line 23

    cout << "Line 24: After sorting, intList2: ";         // line 24
    copy(intList2.begin(), intList2.end(), screen);       // line 25
    cout << endl;                                         // line 26

    intList3.push_back(13);                               // line 27
    intList3.push_back(23);                               // line 28
    intList3.push_back(25);                               // line 29
    intList3.push_back(136);                              // line 30
    intList3.push_back(198);                              // line 31

    cout << "Line 32: intList3: ";                        // line 32
    copy(intList3.begin(), intList3.end(), screen);       // line 33
    cout << endl;                                         // line 34

    intList4.push_back(-2);                               // line 35
    intList4.push_back(-7);                               // line 36
    intList4.push_back(-8);                               // line 37

    cout << "Line 38: intList4: ";                        // line 38
    copy(intList4.begin(), intList4.end(), screen);       // line 39
    cout << endl;                                         // line 40

    intList3.splice(intList3.begin(), intList4);          // line 41

    cout << "Line 42: After moving the elements of "
         << "intList4 into intList3," << endl
         << "        intList3: ";                         // line 42
    copy(intList3.begin(), intList3.end(), screen);       // line 43
    cout << endl;                                         // line 44

    intList3.sort();                                      // line 45

    cout << "Line 46: After sorting, intList3: ";         // line 46
    copy(intList3.begin(), intList3.end(), screen);       // line 47
    cout << endl;                                         // line 48
    intList2.merge(intList3);                             // line 49

    cout << "Line 50: After merging intList2 and "
         << "intList3, intList2: " << endl
         << "        ";
    copy(intList2.begin(), intList2.end(), screen);       // line 50
    cout << endl;                                         // line 51
    // line 52

    intList2.unique();                                    // line 53

    cout << "Line 54: After removing the consecutive "
         << "duplicates, intList2: " << endl
         << "        ";
    copy(intList2.begin(), intList2.end(), screen);       // line 54
    cout << endl;                                         // line 55
    // line 56

    return 0;
}
```

### 示例运行

```text
Line 12: intList1: 23 58 58 58 36 15 93 98 58
Line 16: intList2: 23 58 58 58 36 15 93 98 58
Line 20: After removing the consecutive duplicates,
         intList1: 23 58 36 15 93 98 58
Line 24: After sorting, intList2: 15 23 36 58 58 58 58 93 98
Line 32: intList3: 13 23 25 136 198
Line 38: intList4: -2 -7 -8
Line 42: After moving the elements of intList4 into intList3,
         intList3: -2 -7 -8 13 23 25 136 198
Line 46: After sorting, intList3: -8 -7 -2 13 23 25 136 198
Line 50: After merging intList2 and intList3, intList2:
         -8 -7 -2 13 15 23 23 25 36 58 58 58 58 93 98 136 198
Line 54: After removing the consecutive duplicates, intList2:
         -8 -7 -2 13 15 23 25 36 58 93 98 136 198
```

大体而言，前一个程序的输出很直观。第 3 行到第 11 行的语句将数字元素 23、58、58、58、36、15、93、98 和 58（按此顺序）插入 intList1。第 15 行的语句将 intList1 的元素复制到 intList2。该语句执行后，intList1 和 intList2 相同。第 19 行的语句删除任何连续出现的相同元素。例如，数字 58 连续出现三次。unique 操作删除了 58 的两个重复出现。请注意，此操作对 intList1 末尾出现的 58 没有影响。

第 23 行的语句对 intList2 排序。第 27 行到第 31 行的语句将 13、23、25、136 和 198 插入 intList3。类似地，第 35 行到第 37 行的语句将 -2、-7 和 -8 插入 intList4。第 41 行的语句使用 splice 操作将 intList4 的元素移动到 intList3 的开头。splice 操作后，intList4 为空。第 45 行的语句对 intList3 排序，第 49 行的语句将 intList2 和 intList3 合并到 intList2 中。合并操作后，intList3 为空。其余语句的含义类似。
