
除了所有顺序容器共有的操作（表21-6）之外，表21-8描述了可用于操作deque容器元素的操作。每条语句还展示了如何使用特定函数。假设`deque`是一个deque容器。

## 表21-8 可对deque对象执行的各种操作

| 表达式 | 描述 |
|---|---|
| `deq.assign(n, elem)` | 赋值elem的n个副本。 |
| `deq.assign(beg, end)` | 赋值范围beg...end-1中的所有元素。 |
| `deq.push_front(elem)` | 在deq的开头插入elem。 |
| `deq.pop_front()` | 从deq中移除第一个元素。 |
| `deq.at(index)` | 返回由index指定位置处的元素。 |
| `deq[index]` | 返回由index指定位置处的元素。 |
| `deq.front()` | 返回第一个元素。（不检查容器是否为空。） |
| `deq.back()` | 返回最后一个元素。（不检查容器是否为空。） |

在C++11中，可以声明deque对象，并使用赋值语句对其进行初始化。例如，参见示例21-7程序中第8行的语句。此外，示例21-7说明了如何在程序中使用deque容器。

## 示例21-7

```cpp
//deque Example
#include <iostream>                              //Line 1
#include <deque>                                 //Line 2
#include <algorithm>                             //Line 3
#include <iterator>                              //Line 4

using namespace std;                             //Line 5

int main()
{
    deque<int> intDeq = { 13, 75, 28, 35 };          //Line 6
    ostream_iterator<int> screen(cout, " ");        //Line 7

    cout << "Line 10: intDeq: ";                     //Line 10
    copy(intDeq.begin(), intDeq.end(), screen);      //Line 11
    cout << endl;                                     //Line 12

    intDeq.push_front(0);                             //Line 13
    intDeq.push_back(100);                            //Line 14

    cout << "Line 15: After adding two more "
         << "elements, one at the front " << endl
         << "        and one at the back, intDeq: "; //Line 15
    copy(intDeq.begin(), intDeq.end(), screen);       //Line 16
    cout << endl;                                     //Line 17

    intDeq.pop_front();                               //Line 18
    intDeq.pop_front();                               //Line 19

    cout << "Line 20: After removing the first "
         << "two elements, " << endl
         << "        intDeq: ";                       //Line 20
    copy(intDeq.begin(), intDeq.end(), screen);       //Line 21
    cout << endl;                                     //Line 22

    intDeq.pop_back();                                //Line 23
    intDeq.pop_back();                                //Line 24

    cout << "Line 25: After removing the last "
         << "two elements, " << endl
         << "        intDeq = ";                       //Line 25
    copy(intDeq.begin(), intDeq.end(), screen);       //Line 26
    cout << endl;                                     //Line 27

    deque<int>::iterator deqIt;                       //Line 28

    deqIt = intDeq.begin();                            //Line 29
    ++deqIt;                      //deqIt points to the //Line 30
                                  //second element

    intDeq.insert(deqIt, 444);  //Insert 444 at the    //Line 31
                               //location deqIt

    cout << "Line 32: After inserting 444, "
         << "intDeq: ";                         //Line 32
    copy (intDeq.begin(), intDeq.end(), screen);  //Line 33
    cout << endl;                                 //Line 34

    intDeq.assign(2, 45);                         //Line 36

    cout << "Line 36: After assigning two "
         << "copies of 45, intDeq: ";             //Line 36
    copy (intDeq.begin(), intDeq.end(), screen);  //Line 37
    cout << endl;                                 //Line 38

    intDeq.push_front(-10);                       //Line 39
    intDeq.push_back(-999);                       //Line 40

    cout << "Line 41: After inserting two "
         << "elements, one at the front, " << endl
         << "         and one at the back, intDeq: "; //Line 41
    copy (intDeq.begin(), intDeq.end(), screen);      //Line 42
    cout << endl;                                     //Line 43

    return 0;                                         //Line 44
}                                                 //Line 45
```

### 示例运行：

```text
Line 10: intDeq: 13 75 28 35
Line 15: After adding two more elements, one at the front
          and one at the back, intDeq: 0 13 75 28 35 100
Line 20: After removing the first two elements,
          intDeq: 75 28 35 100
Line 25: After removing the last two elements,
          intDeq: 75 28
Line 32: After inserting 444, intDeq: 75 444 28
Line 36: After assigning two copies of 45, intDeq: 45 45
Line 41: After inserting two elements, one at the front
          and one at the back, intDeq: -10 45 45 -999
```

第8行的语句声明并初始化一个int类型的deque容器intDeq；也就是说，intDeq的所有元素都是int类型。第9行的语句将screen声明为初始化为标准输出设备的ostream迭代器。第11行的语句输出intDeq的元素。在输出中，参见标记为Line 10的那一行，它包含第10行至第12行语句的输出。

第13行的语句在intDeq的开头插入0；第14行的语句在intDeq的末尾插入100。第16行的语句输出修改后的intDeq。

第18行和第19行的语句使用函数pop_front移除intDeq的前两个元素；第21行的语句输出修改后的intDeq。

## 表21-9 声明list对象的各种方式

| 语句 | 描述 |
|---|---|
| `list<elementType> listCont;` | 创建空的list容器`listCont`。（调用默认构造函数。） |
| `list<elementType> listCont(otherList);` | 创建list容器`listCont`，并将其初始化为`otherList`的元素。`listCont`和`otherList`类型相同。 |
| `list<elementType> listCont(size);` | 创建大小为`size`的list容器`listCont`。`listCont`使用默认构造函数初始化。 |
| `list<elementType> listCont(n, elm);` | 创建大小为`n`的list容器`listCont`。`listCont`使用元素`elm`的`n`个副本初始化。 |
| `list<elementType> listCont(beg, end);` | 创建list容器`listCont`。`listCont`被初始化为范围`[beg, end)`中的元素；也就是说，范围`beg...end-1`中的所有元素。`beg`和`end`都是迭代器。 |

表21-5描述了所有容器共有的操作。表21-6描述了所有顺序容器共有的操作。除这些共有操作之外，表21-10描述了`list`容器特有的操作。在此表中，`listCont`是类型为`list`的容器。

## 表21-10 `list`容器特有的各种操作

| 表达式 | 描述 |
|---|---|
| `listCont.assign(n, elem);` | 赋值elem的n个副本。 |
| `listCont.assign(beg, end);` | 赋值范围`beg...end-1`中的所有元素。beg和end都是迭代器。 |
| `listCont.push_front(elem);` | 在`listCont`的开头插入elem。 |
| `listCont.pop_front();` | 从`listCont`中移除第一个元素。 |
| `listCont.front();` | 返回第一个元素。（不检查容器是否为空。） |
| `listCont.back();` | 返回最后一个元素。（不检查容器是否为空）。 |
| `listCont.remove(elem);` | 移除所有等于elem的元素。 |
| `listCont.remove_if(oper);` | 移除所有使oper为`true`的元素。 |
| `listCont.unique();` | 如果`listCont`中连续元素具有相同值，则移除重复项。 |
| `listCont.unique(oper);` | 如果`listCont`中连续元素具有相同值，则移除其中oper为`true`的重复项。 |
