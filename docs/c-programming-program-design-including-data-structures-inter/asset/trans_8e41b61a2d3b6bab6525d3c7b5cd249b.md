
```cpp
template <class bidirectionalItr>
void inplace_merge(bidirectionalItr first,
                   bidirectionalItr middle,
                   bidirectionalItr last);

template <class bidirectionalItr, class binaryPredicate>
void inplace_merge(bidirectionalItr first,
                   bidirectionalItr middle,
                   bidirectionalItr last,
                   binaryPredicate op);
```

这两种形式都会合并已排序的连续序列 first...middle-1 和 middle...last-1。合并后的元素会覆盖从 first 开始的两个区间。第一种形式使用小于准则来合并这两个连续序列。第二种形式使用二元谓词 op 来合并序列；也就是说，对于两个序列中的元素，op(elemSeq1, elemSeq2) 必须为 true。例如，假设：

`vecList = {1, 3, 5, 7, 9, 2, 4, 6, 8}`

其中 vecList 是一个 vector 容器。再假设 vecItr 是一个指向元素 2 的 vector 迭代器。那么，在执行语句：

```cpp
inplace_merge(vecList.begin(), vecItr, vecList.end());
```

之后，vecList 中的元素将按以下顺序排列：

`vecList = {1, 2, 3, 4, 5, 6, 7, 8, 9}`

示例 21-22 中的程序演示了这些算法的工作原理。

## 示例 21-22

```cpp
//STL Functions adjacent_find, merge, and inplace_merge

#include <iostream>
#include <functional>
#include <algorithm>
#include <iterator>
#include <vector>
#include <list>

using namespace std;

int main()
{
    int list1[10] = {1, 3, 5, 7, 9, 0, 2, 4, 6, 8};    //Line 1
    int list2[10] = {0, 1, 1, 2, 3, 4, 4, 5, 6, 6};    //Line 2

    int list3[5] = {0, 2, 4, 6, 8};                     //Line 3
    int list4[5] = {1, 3, 5, 7, 9};                     //Line 4

    list<int> intList(list2, list2 + 10);                    //Line 5
    list<int>::iterator listItr;                              //Line 6

    vector<int> vecList(list1, list1 + 10);                   //Line 7
    vector<int>::iterator       intItr;                       //Line 8

    ostream_iterator<int> screen(cout, " ");                 //Line 9

    cout << "Line 10: intList : ";                            //Line 10
    copy(intList.begin(), intList.end(), screen);              //Line 11
    cout << endl;                                              //Line 12

           //adjacent_find
    listItr = adjacent_find(intList.begin(),
                            intList.end());                   //Line 13

    if (listItr != intList.end())                              //Line 14
        cout << "Line 15: Adjacent equal "
             << "elements are found " << endl
             << "         The first set of "
             << "adjacent equal elements: "
             << listItr << endl;                              //Line 15
    else                                                         //Line 16
        cout << "Line 17: No adjacent equal "
             << "element found" << endl;                      //Line 17

    intList.clear();                                           //Line 18

           //merge
    merge(list3, list3 + 5, list4, list4 + 5,
          back_inserter(intList));                             //Line 19

    cout << "Line 20: intList after merging list3 "
         << "and " << list4 << "\n"
         << " ";                                                //Line 20
    copy(intList.begin(), intList.end(), screen);              //Line 21
    cout << endl;                                              //Line 22

           //adjacent_find; second form
    intItr = adjacent_find(vecList.begin(),
                           vecList.end(),
                           greater<int>());                    //Line 23

    cout << "Line 24: Last element of first "
         << "sorted sublist: " << *intItr << endl;             //Line 24
    intItr++;
    cout << "Line 26: First element of second "
         << "sorted sublist: " << *intItr << endl;             //Line 26

    cout << "Line 27: vecList before "
         << "inplace_merge: ";
    copy(vecList.begin(), vecList.end(), screen);              //Line 28
    cout << endl;                                              //Line 29
```

inplace_merge 和迭代器 intItr 用于合并 vecList 的已排序子序列。请注意，vecList 包含合并后的序列。在输出中，标记为 Line 27 的行包含第 27 至 29 行语句的输出；标记为 Line 31 的行包含第 31 至 33 行语句的输出。

## reverse、reverse_copy、rotate 和 rotate_copy 函数

算法 reverse 用于反转给定范围内元素的顺序。实现算法 reverse 的函数原型如下：

```cpp
template <class bidirectionalItr>
void reverse(bidirectionalItr first, bidirectionalItr last);
```

范围 first...last-1 中的元素会被反转。例如，如果 vecList = {1, 2, 5, 3, 4}，则反转后的元素顺序为 vecList = {4, 3, 5, 2, 1}。

算法 reverse_copy 通过将给定范围内的元素复制到目标范围来反转这些元素。源范围不会被修改。实现算法 reverse_copy 的函数原型如下：

```cpp
template <class bidirectionalItr, class outputItr>
outputItr reverse_copy(bidirectionalItr first,
                       bidirectionalItr last,
                       outputItr destFirst);
```

范围 first...last-1 中的元素会以相反顺序复制到目标位置，从 destFirst 开始。该函数还会返回目标中最后一个被复制元素之后的位置。

算法 rotate 用于旋转给定范围内的元素。其原型如下：

```cpp
template <class forwardItr>
void rotate(forwardItr first, forwardItr newFirst,
            forwardItr last);
```

范围 first...newFirst-1 中的元素会被移动到范围的末尾。由 newFirst 指定的元素将成为该范围的第一个元素。例如，假设：

```text
vecList = {3, 5, 4, 0, 7, 8, 2, 5}
```

且迭代器 vecItr 指向 0。然后，在执行语句：

```cpp
rotate(vecList.begin(), vecItr, vecList.end());
```

之后，vecList 如下所示：

```text
vecList = {0, 7, 8, 2, 5, 3, 5, 4}
```

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1526_0.png)

算法 `rotate_copy` 是 rotate 和 copy 的组合。也就是说，源范围中的元素会以旋转后的顺序复制到目标位置。源范围不会被修改。实现该算法的函数原型如下：

```cpp
template <class forwardItr, class outputItr>
outputItr rotate_copy(forwardItr first, forwardItr middle,
                      forwardItr last,
                      outputItr destFirst);
```

范围 `first...last-1` 中的元素会以旋转后的顺序复制到从 `destFirst` 开始的目标范围中，使得范围 `first...last-1` 中由 `middle` 指定的元素成为目标范围的第一个元素。该函数还会返回目标中最后一个被复制元素之后的位置。

算法 reverse、reverse_copy、rotate 和 rotate_copy 包含在头文件 algorithm 中。示例 21–23 中的程序演示了如何使用这些算法。

## 示例 21-23

```cpp
//STL Functions: reverse, reverse_copy, rotate, and rotate_copy

#include <iostream>
#include <algorithm>
#include <iterator>
#include <list>

using namespace std;

int main()
{
    int temp[10] = {1, 3, 5, 7, 9, 0, 2, 4, 6, 8};       //Line 1

    list<int> intList(temp, temp + 10);                    //Line 2
    list<int> result;                                      //Line 3
    list<int>::iterator listItr;                           //Line 4

    ostream_iterator<int> screen(cout, " ");              //Line 5

    cout << "Line 6: intList: ";                          //Line 6
    copy(intList.begin(), intList.end(), screen);          //Line 7
    cout << endl;                                          //Line 8

        //reverse
    reverse(intList.begin(), intList.end());                //Line 9

    cout << "Line 10: intList after reversal: ";           //Line 10
    copy(intList.begin(), intList.end(), screen);           //Line 11
    cout << endl;                                           //Line 12
```
