
### 表 21-10 列表容器特有的各种操作（续）

| 表达式 | 描述 |
|---|---|
| `listCont1.splice(pos, listCont2)` | `listCont2` 的所有元素被移动到 `listCont1` 中迭代器 `pos` 指定的位置之前。此操作后，`listCont2` 为空。 |
| `listCont1.splice(pos, listCont2, pos2)` | `listCont2` 中从 `pos2` 开始的所有元素被移动到 `listCont1` 中迭代器 `pos` 指定的位置之前。 |
| `listCont1.splice(pos, listCont2, beg, end)` | `listCont2` 中范围 `beg...end-1` 内的所有元素被移动到 `listCont1` 中迭代器 `pos` 指定的位置之前。`beg` 和 `end` 都是迭代器。 |
| `listCont1.sort()` | `listCont1` 的元素被排序。排序准则为 `<`。 |
| `listCont1.sort(oper)` | `listCont1` 的元素被排序。排序准则由 `oper` 指定。 |
| `listCont1.merge(listCont2)` | 假设 `listCont1` 和 `listCont2` 的元素已排序。此操作将 `listCont2` 的所有元素移动到 `listCont1` 中。此操作后，`listCont1` 中的元素已排序。此外，此操作后，`listCont2` 为空。 |
| `listCont1.merge(listCont2, oper)` | 假设 `listCont1` 和 `listCont2` 的元素已按准则 `oper` 排序。此操作将 `listCont2` 的所有元素移动到 `listCont1` 中。此操作后，`listCont1` 中的元素按排序准则 `oper` 排序。 |
| `listCont1.reverse()` | `listCont1` 的元素被反转。 |

例 21-7 说明了如何使用列表容器上的各种操作。

### 例 21-7

```cpp
//list Container Example

#include <iostream>
#include <list>
#include <iterator>
#include <algorithm>

using namespace std;

int main()
{
    list<int> intList1, intList2, intList3, intList4;    //Line 1

    ostream_iterator<int> screen(cout, " ");             //Line 2

    intList1.push_back(23);                               //Line 3
    intList1.push_back(58);                               //Line 4
    intList1.push_back(58);                               //Line 5
    intList1.push_back(58);                               //Line 6
    intList1.push_back(36);                               //Line 8
    intList1.push_back(15);                               //Line 9
    intList1.push_back(93);                               //Line 10
    intList1.push_back(98);                               //Line 11
    intList1.push_back(58);
    cout << "Line 12: intList1: ";                         //Line 12
    copy(intList1.begin(), intList1.end(), screen);          //Line 13
    cout << endl;                                            //Line 14

    intList2 = intList1;                                     //Line 15

    cout << "Line 16: intList2: ";                         //Line 16
    copy(intList2.begin(), intList2.end(), screen);          //Line 17
    cout << endl;                                            //Line 18

    intList1.unique();                                       //Line 19

    cout << "Line 20: After removing the consecutive "
         << "duplicates," << endl
         << "        intList1: ";                           //Line 20
    copy(intList1.begin(), intList1.end(), screen);          //Line 21
    cout << endl;                                            //Line 22

    intList2.sort();                                         //Line 23

    cout << "Line 24: After sorting, intList2: ";           //Line 24
    copy(intList2.begin(), intList2.end(), screen);          //Line 25
    cout << endl;                                            //Line 26

    intList3.push_back(13);                                  //Line 27
    intList3.push_back(23);                                  //Line 28
    intList3.push_back(25);                                  //Line 29
    intList3.push_back(136);                                 //Line 30
    intList3.push_back(198);                                 //Line 31

    cout << "Line 32: intList3: ";                          //Line 32
    copy(intList3.begin(), intList3.end(), screen);          //Line 33
    cout << endl;                                            //Line 34

    intList4.push_back(-2);                                  //Line 35
    intList4.push_back(-7);                                  //Line 36
    intList4.push_back(-8);                                  //Line 37

    cout << "Line 38: intList4: ";                          //Line 38
    copy(intList4.begin(), intList4.end(), screen);          //Line 39
    cout << endl;                                            //Line 40

    intList3.splice(intList3.begin(), intList4);             //Line 41

    cout << "Line 42: After moving the elements of "
         << "intList4 into intList3, " << endl
         << "        intList3: ";                           //Line 42
    copy(intList3.begin(), intList3.end(), screen);          //Line 43
    cout << endl;                                            //Line 44

    intList3.sort();                                         //Line 45
    cout << "Line 46: After sorting, intList3: ";        //Line 46
    copy(intList3.begin(), intList3.end(), screen);       //Line 47
    cout << endl;                                         //Line 48

    intList2.merge(intList3);                             //Line 49

    cout << "Line 50: After merging intList2 and "
         << "intList3, intList2:" << endl                      //Line 50
         << "    " ;                                   //Line 51
    copy(intList2.begin(), intList2.end(), screen);       //Line 52
    cout << endl;                                         //Line 53

    intList2.unique();

    cout << "Line 54: After removing the consecutive "
         << "duplicates, intList2: " << endl             //Line 54
         << "    " ;
    copy(intList2.begin(), intList2.end(), screen);       //Line 55
    cout << endl;                                         //Line 56

    return 0;
}
```

### 示例运行：

```text
Line 12: intList1: 23 58 58 58 36 15 93 98 58
Line 16: intList2: 23 58 58 58 36 15 93 98 58
Line 20: After removing the consecutive duplicates,
         intList1: 23 58 36 15 93 98 58
Line 24: After sorting, intList2: 15 23 36 58 58 58 93 98
Line 32: intList3: 13 23 25 136 198
Line 38: intList4: −2 −7 −8
Line 42: After moving the elements of intList4 into intList3,
         intList3: −2 −7 −8 13 23 25 136 198
Line 46: After sorting, intList3: −8 −7 −2 13 23 25 136 198
Line 50: After merging intList2 and intList3, intList2:
         −8 −7 −2 13 15 23 23 25 36 58 58 58 93 98 136 198
Line 54: After removing the consecutive duplicates, intList2:
         −8 −7 −2 13 15 23 25 36 58 93 98 136 198
```

上述程序的输出大部分都很直观。第 3 行到第 11 行的语句将数字 23、58、58、58、36、15、93、98 和 58（按此顺序）插入 intList1。第 15 行的语句将 intList1 的元素复制到 intList2。该语句执行后，intList1 和 intList2 完全相同。第 19 行的语句删除任何连续出现的相同元素。例如，数字 58 连续出现三次。unique 操作删除其中两次出现的 58。注意，此操作对 intList1 末尾出现的 58 没有影响。

第 23 行的语句对 intList2 排序。第 27 行到第 31 行的语句将 13、23、25、136 和 198 插入 intList3。类似地，第 35 行到第 37 行的语句将 −2、−7 和 −8 插入 intList4。第 41 行的语句使用 splice 操作将 intList4 的元素移动到 intList3 的开头。splice 操作后，intList4 为空。第 45 行的语句对 intList3 排序，第 49 行的语句将 intList2 和 intList3 合并到 intList2 中。合并操作后，intList3 为空。其余语句的含义类似。

例 21-5 到 21-7 进一步说明，迭代器对于高效处理容器元素很重要。在描述关联容器之前，我们先较为详细地讨论迭代器。

## 迭代器

迭代器类似于指针。一般而言，迭代器指向容器（顺序容器或关联容器）的元素。因此，借助迭代器，我们可以依次访问容器的每个元素。

迭代器上最常见的两种操作是 ++（自增运算符）和 *（解引用运算符）。假设 cntItr 是某个容器中的迭代器。语句：

```cpp
++cntItr;
```

使 cntItr 前进，使其指向容器中的下一个元素。类似地，语句：

```cpp
*cntItr;
```

可访问 cntItr 所指向的容器元素。

### 迭代器的类型

迭代器有五种类型：

- 输入迭代器
- 输出迭代器
- 前向迭代器
- 双向迭代器
- 随机访问迭代器

以下各节描述这些迭代器。

### 输入迭代器

输入迭代器具有读访问能力，逐个元素向前步进；因此，它们逐个元素返回值。这些迭代器用于从输入流读取数据。

假设 inputIterator 是一个输入迭代器。表 21-11 描述了可在 inputIterator 上执行的操作。
