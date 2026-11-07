
### 示例 21-3

考虑以下语句：

```cpp
int intArray[7] = {1, 3, 5, 7, 9, 11, 13};             //Line 1
vector<int> vecList(intArray, intArray + 7);             //Line 2
vector<int>::iterator intVecIter;                       //Line 3
```

第 2 行的语句声明并初始化了 vector 容器 vecList。现在考虑以下语句：

```cpp
intVecIter = vecList.begin();                          //Line 4
++intVecIter;                                           //Line 5
vecList.insert(intVecIter, 22);                        //Line 6
```

第 4 行的语句将迭代器 intVecIter 初始化为 vecList 的第一个元素；第 5 行的语句将 intVecIter 推进到 vecList 的第二个元素。第 6 行的语句在 intVecIter 指定的位置插入 22。第 6 行的语句执行后，vecList = {1, 22, 3, 5, 7, 9, 11, 13}。注意，容器的大小也增加了。

以下示例说明了如何在程序中使用 vector 容器以及如何处理 vector 容器中的元素。

### 示例 21-4

```cpp
#include <iostream>                                      //Line 1
#include <vector>                                        //Line 2

using namespace std;                                     //Line 3

int main()                                               //Line 4
{                                                        //Line 5
    vector<int> intList;                                 //Line 6
    intList.push_back(13);                               //Line 7
    intList.push_back(75);                               //Line 8
    intList.push_back(28);                               //Line 9
    intList.push_back(35);                               //Line 10

    cout << "Line 11: List elements: ";                 //Line 11
    for (int i = 0; i < 4; i++)                          //Line 12
        cout << intList[i] << " ";                      //Line 13
    cout << endl;                                        //Line 14

    for (int i = 0; i < 4; i++)                          //Line 15
        intList[i] *= 2;                                 //Line 16

    cout << "Line 17: List elements: ";                 //Line 17
    for (int i = 0; i < 4; i++)                          //Line 18
        cout << intList[i] << " ";                      //Line 19
    cout << endl;                                        //Line 20

    vector<int>::iterator listIt;                         //Line 21

    cout << "Line 22: List elements: ";                 //Line 22
    for (listIt = intList.begin();
         listIt != intList.end(); ++listIt)              //Line 23
        cout << *listIt << " ";                         //Line 24
    cout << endl;                                        //Line 25

    listIt = intList.begin();                            //Line 26
    ++listIt;                                            //Line 27
    ++listIt;                                            //Line 28

    //Insert 88 at the position specified by listIt
    intList.insert(listIt, 88);                          //Line 29

    cout << "Line 30: List elements: ";                 //Line 30
    for (listIt = intList.begin();
         listIt != intList.end(); ++listIt)              //Line 31
        cout << *listIt << " ";                         //Line 32
    cout << endl;                                        //Line 33

    return 0;                                            //Line 34
}                                                        //Line 35
```

### 运行示例：

```text
Line 11: List elements: 13 75 28 35
Line 17: List elements: 26 150 56 70
Line 22: List elements: 26 150 56 70
Line 30: List elements: 26 150 88 56 70
```

第 6 行的语句声明了一个 int 类型的 vector 容器（简称 vector）intList。第 7 行到第 10 行的语句使用 push_back 操作将四个数字——13、75、28 和 35——插入 intList。第 12 行和第 13 行的语句使用 for 循环和数组下标运算符 [] 输出 intList 的元素。在输出中，请查看标记为 Line 11 的那一行，它包含第 11 行到第 14 行的输出。第 15 行和第 16 行的语句使用 for 循环将 intList 中每个元素的值加倍；第 18 行和第 19 行的语句输出 intList 的元素。在输出中，请查看标记为 Line 17 的那一行，它包含第 17 行到第 20 行的输出。

第 21 行的语句将 listIt 声明为 vector 迭代器，用于处理元素类型为 int 的任何 vector 容器。使用迭代器 listIt，第 23 行和第 24 行的语句输出 intList 的元素。第 26 行的语句执行后，listIt 指向 intList 的第一个元素。第 27 行和第 28 行的语句将 listIt 推进两次；这些语句执行后，listIt 指向 intList 的第三个元素。第 29 行的语句将 88 插入 `intList` 中由迭代器 `listIt` 指定的位置。因为 `listIt` 指向位置 2 的组件（`intList` 的第三个元素），所以 88 被插入到 `intList` 中的位置 2；也就是说，88 成为 `intList` 的第三个元素。第 31 行和第 32 行的语句输出修改后的 `intList`。

## 所有容器共有的成员函数

上一节讨论了 vector 容器。本节讨论所有容器共有的操作。例如，每个容器类都有默认构造函数、若干带参数的构造函数、析构函数、向容器中插入元素的函数，等等。

回想一下，类将数据以及对数据的操作封装为一个单元。因为每个容器都是一个类，所以若干操作直接为容器定义，并作为类定义的一部分提供。另外，回想一下，用于操作数据的操作是在函数的帮助下实现的，这些函数称为类的成员函数。表 21-5 描述了所有容器共有的成员函数；也就是说，这些函数作为实现该容器的类模板的成员包含在内。

假设 `ct`、`ct1` 和 `ct2` 是同一类型的容器。表 21-5 展示了如何调用函数。

**表 21-5** 所有容器共有的操作

| 成员函数 | 描述 |
|---|---|
| 默认构造函数 | 将对象初始化为空状态。 |
| 带参数的构造函数 | 除了默认构造函数外，每个容器还有带参数的构造函数。我们将在讨论具体容器时描述这些构造函数。 |
| 复制构造函数 | 当对象按值作为参数传递时，以及当使用同一类型的另一个对象声明并初始化对象时执行。 |
| 析构函数 | 当对象超出作用域时执行。 |
| `ct.empty()` | 如果容器 `ct` 为空，则返回 `true`，否则返回 `false`。 |
| `ct.size()` | 返回容器 `ct` 中当前元素的数量。 |
| `ct.max_size()` | 返回可以插入容器 `ct` 中的最大元素数量。 |
| `ct1.swap(ct2);` | 交换容器 `ct1` 和 `ct2` 的元素。 |
| `ct.begin()` | 返回指向容器 `ct` 中第一个元素的迭代器。 |
| `ct.end()` | 返回指向容器 `ct` 中最后一个元素之后位置的迭代器。 |
| `ct.rbegin()` | 反向开始。返回指向容器 `ct` 中最后一个元素的指针。此函数用于反向处理 `ct` 的元素。 |
| `ct.rend()` | 反向结束。返回指向容器 `ct` 中第一个元素之前位置的指针。 |
| `ct.insert(position,elem);` | 将元素插入容器 `ct` 中由 `position` 指定的位置。注意，这里的 `position` 是一个迭代器。 |
| `ct.erase(beg, end);` | 从容器 `ct` 中删除 `beg` ... `end - 1` 之间的所有元素。`beg` 和 `end` 都是迭代器。 |
| `ct.clear();` | 删除容器中的所有元素。调用此函数后，容器 `ct` 为空。 |
| **运算符函数** |  |
| `ct1 = ct2;` | 将 `ct2` 的元素复制到 `ct1`。此操作后，两个容器中的元素相同。 |
| `ct1 == ct2` | 如果容器 `ct1` 和 `ct2` 相等，则返回 `true`，否则返回 `false`。 |
| `ct1 != ct2` | 如果容器 `ct1` 和 `ct2` 不相等，则返回 `true`，否则返回 `false`。 |

由于这些操作是所有容器共有的，因此在讨论具体容器时，为节省篇幅，将不再列出这些操作。

![](img/b217c421655b51e7494cf3b89bb5432d_1516_0.png)
