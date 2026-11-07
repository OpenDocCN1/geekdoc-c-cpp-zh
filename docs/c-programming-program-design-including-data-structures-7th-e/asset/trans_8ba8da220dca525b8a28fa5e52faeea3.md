
### 表 21-18 从集合中插入或删除元素的操作（续）

| 表达式 | 效果 |
|---|---|
| `ct.erase(elem);` | 删除所有值为 `elem` 的元素。返回被删除元素的个数。 |
| `ct.erase(position);` | 删除迭代器 position 所指定位置处的元素。不返回值。 |
| `ct.erase(beg, end);` | 删除从位置 `beg` 开始直到位置 `end-1` 的所有元素。`beg` 和 `end` 都是迭代器。不返回值。 |
| `ct.clear();` | 删除容器 `ct` 中的所有元素。执行此操作后，容器 `ct` 为空。 |

示例 21-9 展示了对 set/multiset 容器的各种操作。

### 示例 21-9

```cpp
#include <iostream>
#include <set>
#include <string>
#include <iterator>
#include <algorithm>
#include <functional>

using namespace std;

int main()
{
        set<int> intSet;                                      //Line 1
        set<int, greater<int> > intSetA;                      //Line 2

        set<int, greater<int> >::iterator intGtIt;             //Line 3

        ostream_iterator<int> screen(cout, " ");              //Line 4

        intSet.insert(16);                                     //Line 5
        intSet.insert(8);                                      //Line 6
        intSet.insert(20);                                     //Line 7
        intSet.insert(3);                                      //Line 8

        cout << "Line 9: intSet: ";                           //Line 9
        copy(intSet.begin(), intSet.end(), screen);            //Line 10
        cout << endl;                                          //Line 11

        intSetA.insert(36);                                    //Line 12
        intSetA.insert(84);                                    //Line 13
        intSetA.insert(30);                                    //Line 14
        intSetA.insert(39);                                    //Line 15
        intSetA.insert(59);                                    //Line 16
        intSetA.insert(238);                                   //Line 17
        intSetA.insert(156);                                   //Line 18

        cout << "Line 19: intSetA: ";
        copy(intSetA.begin(), intSetA.end(), screen);      //Line 20
        cout << endl;                                      //Line 21

        intSetA.erase(59);                                 //Line 22

        cout << "Line 23: After removing 59, intSetA: ";   //Line 23
        copy(intSetA.begin(), intSetA.end(), screen);      //Line 24
        cout << endl;                                      //Line 25

        intGtIt = intSetA.begin();                         //Line 26
        ++intGtIt;                                         //Line 27
        ++intGtIt;                                         //Line 28
        ++intGtIt;                                         //Line 29

        intSetA.erase(intGtIt);                            //Line 30

        cout << "Line 31: After removing the fourth "
             << "element, " << endl
             << "        intSetA: ";                       //Line 31
        copy(intSetA.begin(), intSetA.end(), screen);      //Line 32
        cout << endl;                                      //Line 33

        set<int, greater<int> > intSetB(intSetA);          //Line 34

        cout << "Line 35: intSetB: ";                      //Line 35
        copy(intSetB.begin(), intSetB.end(), screen);      //Line 36
        cout << endl;                                      //Line 37

        intSetB.clear();                                   //Line 38

        cout << "Line 39: After removing all elements, "
             << endl << "        intSetB: ";               //Line 39
        copy(intSetB.begin(), intSetB.end(), screen);      //Line 40
        cout << endl;                                      //Line 41

        multiset<string, greater<string> > namesMultiSet;  //Line 42
        multiset<string, greater<string> >::iterator iter; //Line 43

        ostream_iterator<string> pScreen(cout, " ");       //Line 44

        namesMultiSet.insert("Donny");                     //Line 45
        namesMultiSet.insert("Zippy");                     //Line 46
        namesMultiSet.insert("Goofy");                     //Line 47
        namesMultiSet.insert("Hungry");                    //Line 48
        namesMultiSet.insert("Goofy");                     //Line 49
        namesMultiSet.insert("Donny");                     //Line 50

        cout << "Line 51: namesMultiSet: ";                //Line 51
        copy(namesMultiSet.begin(), namesMultiSet.end(),
             pScreen);                                      //Line 52
        cout << endl;                                       //Line 53

        return 0;
}
```

### 示例运行：

```text
Line 9: intSet: 3 8 16 20
Line 19: intSetA: 238 156 84 59 39 36 30
Line 23: After removing 59, intSetA: 238 156 84 39 36 30
Line 31: After removing the fourth element,
         intSetA: 238 156 84 36 30
Line 35: intSetB: 238 156 84 36 30
Line 39: After removing all the elements,
         intSetB:
Line 51: namesMultiSet: Zippy Hungry Goofy Goofy Donny Donny
```

第 1 行的语句声明 intSet 为一个 set 容器。第 2 行的语句声明 intSetA 为一个 set 容器，其元素按降序排列。第 3 行的语句声明 intGtIt 为一个 set 迭代器。迭代器 intGtIt 可以处理任何元素类型为 int 且按降序排列的 set 容器中的元素。第 4 行的语句声明 screen 为一个输出流迭代器，它输出任何元素类型为 int 的容器中的元素。

第 5 行到第 8 行的语句将 16、8、20 和 3 插入 intSet，第 10 行的语句输出 intSet 的元素。在输出中，参见标有 Line 9 的行；它包含第 9 行到第 11 行语句的输出。

第 12 行到第 18 行的语句将 36、84、30、59、238 和 156 插入 intSetA，第 20 行的语句输出 intSetA 的元素。在输出中，参见标有 Line 19 的行。它包含第 19 行到第 21 行语句的输出。注意，intSetA 的元素按降序出现。

第 22 行的语句从 intSetA 中删除 59。第 26 行的语句执行后，intGtIt 指向 intSetA 的第一个元素。第 27 行的语句将 intGtIt 推进到 intSetA 的下一个元素。第 29 行的语句执行后，intGtIt 指向 intSetA 的第四个元素。第 30 行的语句删除 intGtIt 所指向的 intSetA 元素。第 34 行到第 41 行语句的含义类似。

第 42 行的语句声明 namesMultiSet 为一个 multiset 类型的容器。namesMultiSet 中的元素为 string 类型，并按降序排列。第 43 行的语句声明 iter 为一个 multiset 迭代器。

第 45 行到第 50 行的语句将 Donny、Zippy、Goofy、Hungry、Goofy 和 Donny 插入 `namesMultiSet`。第 52 行的语句输出 `namesMultiSet` 的元素。

## 容器适配器

前面几节讨论了几种类型的容器。除了在通用框架中工作的容器之外，STL 还提供了一些容器来适应特殊情形。这些容器称为**容器适配器**，它们是经过改造的标准 STL 容器，以便在特定环境中工作。三种容器适配器是：

- 栈
- 队列
- 优先队列

容器适配器不支持任何类型的迭代器。也就是说，迭代器不能用于这些类型的容器。接下来两节介绍两种容器适配器：栈和队列。

### 栈

第 17 章详细讨论了数据结构栈。由于栈是一种重要的数据结构，STL 提供了一个类，以便在程序中实现栈。定义栈的类名为 `stack`；包含类 `stack` 定义的的头文件名为 `stack`。表 21-19 定义了栈容器类支持的各种操作。

### 表 21-19 对 `stack` 对象的各种操作

| 操作 | 描述 |
|---|---|
| `size` | 返回栈中元素的实际个数。 |
| `empty` | 如果栈为空，则返回 `true`；否则返回 `false`。 |
| `push(item)` | 将 `item` 的一个副本插入栈中。 |
| `top` | 返回栈顶元素，但不从栈中删除该元素。此操作实现为值返回函数。 |
| `pop` | 删除栈顶元素。 |

