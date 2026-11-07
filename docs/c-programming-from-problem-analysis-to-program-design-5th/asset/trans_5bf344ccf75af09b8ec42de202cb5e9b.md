
与其他容器类一样，类 `list` 也包含若干构造函数。因此，在声明 `list` 对象时，可以通过多种方式初始化它。表 H-9 展示了声明和初始化 `list` 对象的各种方式。

### 表 H-9 声明 `list` 对象的各种方式

| 语句 | 描述 |
|---|---|
| `list<elementType> listCont;` | 创建一个空的 list 容器 `listCont`。（调用默认构造函数。） |
| `list<elementType> listCont(otherList);` | 创建 list 容器 `listCont`，并将其初始化为 `otherList` 的元素。`listCont` 和 `otherList` 类型相同。 |
| `list<elementType> listCont(size);` | 创建大小为 `size` 的 list 容器 `listCont`。`listCont` 使用默认构造函数初始化。 |
| `list<elementType> listCont(n, elm);` | 创建大小为 `n` 的 list 容器 `listCont`。`listCont` 使用元素 `elm` 的 `n` 个副本初始化。 |
| `list<elementType> listCont(beg, end);` | 创建 list 容器 `listCont`。`listCont` 初始化为范围 `[beg, end)` 中的元素，即范围 `beg...end-1` 中的所有元素。`beg` 和 `end` 都是迭代器。 |

表 H-5 描述了所有容器共有的操作，表 H-6 描述了所有序列容器共有的操作。除这些共有操作外，表 H-10 描述了 list 容器特有的操作。实现该操作的函数名以粗体显示。（假设 `listCont`、`listCont1` 和 `listCont2` 是 `list` 类型的容器。）

### 表 H-10 `list` 容器特有的各种操作

| 表达式 | 描述 |
|---|---|
| `listCont.assign(n, elem)` | 将 `elem` 的 `n` 个副本赋值给容器。 |
| `listCont.assign(beg, end)` | 将范围 `beg...end-1` 中的所有元素赋值给容器。`beg` 和 `end` 都是迭代器。 |
| `listCont.push_front(elem)` | 在 `listCont` 的开头插入 `elem`。 |
| `listCont.pop_front()` | 从 `listCont` 中移除第一个元素。 |
| `listCont.front()` | 返回第一个元素。（不检查容器是否为空。） |
| `listCont.back()` | 返回最后一个元素。（不检查容器是否为空。） |
| `listCont.remove(elem)` | 移除所有等于 `elem` 的元素。 |
| `listCont.remove_if(oper)` | 移除所有使 `oper` 为真的元素。 |
| `listCont.unique()` | 如果 `listCont` 中连续元素具有相同的值，则移除重复项。 |
| `listCont.unique(oper)` | 如果 `listCont` 中连续元素具有相同的值，则移除其中使 `oper` 为真的重复项。 |
| `listCont.sort()` | 对 `listCont` 的元素进行排序。排序标准是 `<`。 |
| `listCont.sort(oper)` | 对 `listCont` 的元素进行排序。排序标准由 `oper` 指定。 |

### 表 H-10 `list` 容器特有的各种操作（续）

| 表达式 | 描述 |
|---|---|
| `listCont1.merge(listCont2)` | 假设 `listCont1` 和 `listCont2` 的元素已排序。此操作将 `listCont2` 的所有元素移动到 `listCont1` 中。此操作后，`listCont1` 中的元素已排序。此外，此操作后，`listCont2` 为空。 |
| `listCont1.merge(listCont2, oper)` | 假设 `listCont1` 和 `listCont2` 的元素已按排序标准 `oper` 排序。此操作将 `listCont2` 的所有元素移动到 `listCont1` 中。此操作后，`listCont1` 中的元素按排序标准 `oper` 排序。 |
| `listCont.reverse()` | `listCont` 的元素被反转。 |

示例 H-7 说明了如何在 list 容器上使用各种操作。

### 示例 H-7

```cpp
//List Container Example
#include <iostream>
#include <list>
#include <iterator>
#include <algorithm>

using namespace std;

int main()
{
    list<int> intList1, intList2, intList3, intList4; //Line 1

    ostream_iterator<int> screen(cout, " ");          //Line 2

    intList1.push_back(23);                            //Line 3
    intList1.push_back(58);                            //Line 4
    intList1.push_back(58);                            //Line 5
    intList1.push_back(58);                            //Line 6
    intList1.push_back(36);                            //Line 7
    intList1.push_back(15);                            //Line 8
    intList1.push_back(93);                            //Line 9
    intList1.push_back(98);                            //Line 10
    intList1.push_back(58);                            //Line 11

    cout << "Line 12: intList1: ";                  //Line 12
    copy(intList1.begin(), intList1.end(), screen);  //Line 13
    cout << endl;                                    //Line 14

    intList2 = intList1;                             //Line 15

    cout << "Line 16: intList2: ";                  //Line 16
    copy(intList2.begin(), intList2.end(), screen);  //Line 17
    cout << endl;                                    //Line 18

    intList1.unique();                               //Line 19

    cout << "Line 20: After removing the consecutive "
         << "duplicates, " << endl
         << "             intList1: ";               //Line 20
    copy(intList1.begin(), intList1.end(), screen);  //Line 21
    cout << endl;                                    //Line 22

    intList2.sort();                                 //Line 23

    cout << "Line 24: After sorting, intList2: ";   //Line 24
    copy(intList2.begin(), intList2.end(), screen);  //Line 25
    cout << endl;                                    //Line 26

    intList3.push_back(13);                          //Line 27
    intList3.push_back(25);                          //Line 28
    intList3.push_back(23);                          //Line 29
    intList3.push_back(198);                         //Line 30
    intList3.push_back(136);                         //Line 31

    cout << "Line 32: intList3: ";                  //Line 32
    copy(intList3.begin(), intList3.end(), screen);  //Line 33
    cout << endl;                                    //Line 34

    intList3.sort();                                 //Line 35

    cout << "Line 36: After sorting, intList3: ";   //Line 36
    copy(intList3.begin(), intList3.end(), screen);  //Line 37
    cout << endl;                                    //Line 38

    intList2.merge(intList3);                        //Line 39

    cout << "Line 40: After merging intList2 and "
         << "intList3, intList2: " << endl
         << "                 ";                      //Line 40
    copy(intList2.begin(), intList2.end(), screen);  //Line 41
    cout << endl;                                      //Line 42

    return 0;
}
```

### 示例运行：

```text
Line 12: intList1: 23 58 58 58 36 15 93 98 58
Line 16: intList2: 23 58 58 58 36 15 93 98 58
Line 20: After removing the consecutive duplicates,
         intList1: 23 58 36 15 93 98 58
Line 24: After sorting,
         intList2: 15 23 36 58 58 58 58 93 98
Line 32: intList3: 13 25 23 198 136
Line 36: After sorting, intList3: 13 23 25 136 198
Line 40: After merging intList2 and intList3, intList2:
         13 15 23 23 25 36 58 58 58 58 93 98 136 198
```

前面程序的输出大部分都很直观。第 3 行至第 11 行的语句按此顺序将数字元素 23、58、58、58、36、15、93、98 和 58 插入 intList1。第 15 行的语句将 intList1 的元素复制到 intList2。执行该语句后，intList1 和 intList2 完全相同。第 19 行的语句移除任何连续出现的相同元素。例如，数字 58 连续出现三次。该操作移除了 58 的两次出现。注意，此操作对出现在 intList1 末尾的 58 没有影响。

第 23 行的语句对 intList2 排序。第 27 行至第 31 行的语句将 13、25、23、198 和 136 插入 intList3。第 35 行的语句对 intList3 排序，第 39 行的语句将 intList2 和 intList3 合并到 intList2 中。合并操作后，intList3 为空。其余语句的含义类似。

## 迭代器

迭代器类似指针。通常，迭代器指向容器（序列容器或关联容器）中的元素。因此，借助迭代器，我们可以依次访问容器中的每个元素。

迭代器上最常见的两个操作是 ++（递增运算符）和 *（解引用运算符）。假设 cntItr 是某个容器的迭代器。语句：

```cpp
++cntItr;
```

会使 cntItr 前进，使其指向容器中的下一个元素。类似地，语句：

```cpp
*cntItr;
```

返回 cntItr 所指向的容器元素的值。
