

```cpp
int list4[5] = {1, 3, 5, 7, 9};                    //Line 13
list<int> intList(list2, list2 + 10);                //Line 14
list<int> intList;                                    //Line 15

vector<int> vecList(list1, list1 + 10);               //Line 16
vector<int>::iterator intItr;                         //Line 17

ostream_iterator<int> screen(cout, " ");             //Line 18

cout << "Line 19: intList :";
copy(intList.begin(), intList.end(), screen);          //Line 20
cout << endl;                                          //Line 21

    //adjacent_find
listItr = adjacent_find(intList.begin(),
                        intList.end());               //Line 22

if (listItr != intList.end())                          //Line 23
    cout << "Line 24: Adjacent equal "
         << " elements are found " << endl
         << "        The first set of "
         << " adjacent equal elements: "
         << *listItr << endl;                          //Line 24
else                                                    //Line 25
    cout << "Line 26: No adjacent equal "
         << " element found " << endl;                //Line 26

intList.clear();                                        //Line 27

    //merge
merge(list3, list3 + 5, list4, list4 + 5,
      back_inserter(intList));                         //Line 28

cout << "Line 29: intList after merging list3 "
     << " and " << "list4:\n"
     << "       ";                                     //Line 29
copy(intList.begin(), intList.end(), screen);          //Line 30
cout << endl;                                          //Line 31

    //adjacent_find, second form
intItr = adjacent_find(vecList.begin(),
                       vecList.end(),
                       greater<int>());                //Line 32

cout << "Line 33: Last element of first "
     << "sorted sublist: " << *intItr << endl;         //Line 33
intItr++;                                               //Line 34
cout << "Line 35: First element of second "
     << " sorted sublist: " << *intItr << endl;        //Line 35

cout << "Line 36: vecList before "
     << " inplace_merge: ";                            //Line 36
copy(vecList.begin(), vecList.end(), screen);
cout << endl;                                      //Line 38

    //inplace_merge
    inplace_merge(vecList.begin(), intItr,
                  vecList.end());                  //Line 39

    cout << "Line 40: vecList after inplace_merge: " //Line 40
    copy(vecList.begin(), vecList.end(), screen);    //Line 41
    cout << endl;                                    //Line 42

    return 0;                                        //Line 43
}                                                    //Line 44
```

# 示例运行：

```text
Line 19: intList : 0 1 1 2 3 4 4 5 6 6
Line 24: Adjacent equal elements are found
          The first set of adjacent equal elements: 1
Line 29: intList after merging list3 and list4:
          0 1 2 3 4 5 6 7 8 9
Line 33: Last element of first sorted sublist: 9
Line 35: First element of second sorted sublist: 0
Line 36: vecList before inplace_merge: 1 3 5 7 9 0 2 4 6 8
Line 40: vecList after inplace_merge: 0 1 2 3 4 5 6 7 8 9
```

第14行的语句创建一个类型为 `list<int>` 的 `intList`，并使用 `list2` 初始化 `intList`。因此，`intList` 是一个链表。第16行的语句创建类型为 `int` 的向量 `vecList`，并使用 `list1` 初始化它。第20行的语句输出 `intList`。第22行的语句使用函数 `adjacent_find` 查找（第一组）连续相同元素的位置。该函数返回指向第一组连续元素的指针，并将其存储在 `listItr` 中。第23行至第26行的语句输出这些连续相同元素（如果找到的话）。注意，第24行的语句输出 *listItr——即 `listItr` 所指向内存空间的内容。

第27行的语句通过删除 `intList` 的所有元素来清空 `intList`。第28行的语句使用函数 `merge` 合并 `list3` 和 `list4`。第28行中函数 `merge` 的第三个参数是对 `back_inserter` 的调用，它将合并后的列表放入 `intList`。第28行的语句执行后，`intList` 包含合并后的列表。第30行的语句输出 `intList`。在输出中，请参见标有 Line 29 的那一行，它包含第29行至第31行语句的输出。

注意，`vecList` 为 {1, 3, 5, 7, 9, 0, 2, 4, 6, 8}，其中包含两个已排序的子序列。第32行的语句使用函数 `adjacent_find` 的第二种形式来查找第二个子序列的起始位置。注意，函数 `adjacent_find` 的第三个参数是二元谓词 `greater`，它返回 `vecList` 中第一个元素大于第二个元素的位置。返回的位置存储在迭代器 `intItr` 中，此时它指向元素 9。第34行的语句将 `intItr` 推进到指向元素 0，即第二个子序列的第一个元素。第39行的语句使用函数 `inplace_merge` 和迭代器 `intItr` 合并 `vecList` 的已排序子序列。注意，`vecList` 包含结果序列。在输出中，标有 Line 36 的那一行包含第36行至第38行语句的输出；标有 Line 40 的那一行包含第40行至第42行语句的输出。

## 函数 reverse、reverse_copy、rotate 和 rotate_copy

算法 `reverse` 反转给定范围内元素的顺序。实现算法 `reverse` 的函数的原型如下：

```cpp
template <class biDirectionalItr>
void reverse(biDirectionalItr first, biDirectionalItr last);
```

范围 `first...last-1` 中的元素被反转。例如，如果 `vecList = {1, 2, 5, 3, 4}`，那么反转顺序后的元素为 `vecList = {4, 3, 5, 2, 1}`。

算法 `reverse_copy` 在将给定范围的元素复制到目标范围的同时反转这些元素。源不会被修改。实现算法 `reverse_copy` 的函数的原型如下：

```cpp
template <class biDirectionalItr, class outputItr>
outputItr reverse_copy(biDirectionalItr first,
                       biDirectionalItr last,
                       outputItr destFirst);
```

范围 `first...last-1` 中的元素按相反顺序复制到目标位置，从 `destFirst` 开始。该函数还返回目标位置中最后一个被复制元素之后的位置。

算法 `rotate` 旋转给定范围内的元素。其原型如下：

```cpp
template <class forwardItr>
void rotate(forwardItr first, forwardItr newFirst,
            forwardItr last);
```

范围 `first...newFirst-1` 中的元素被移动到该范围的末尾。由 `newFirst` 指定的元素成为该范围的第一个元素。例如，假设

```cpp
vecList = {3, 5, 4, 0, 7, 8, 2, 5}
```

并且迭代器 `vecItr` 指向 0。那么，在语句

```cpp
rotate(vecList.begin(), vecItr, vecList.end());
```

执行后，`vecList` 如下：

```cpp
vecList = {0, 7, 8, 2, 5, 3, 5, 4}
```

算法 `rotate_copy` 是 `rotate` 和 `copy` 的组合。也就是说，源中的元素按旋转后的顺序复制到目标。源不会被修改。实现该算法的函数的原型如下：

```cpp
template <class forwardItr, class outputItr>
outputItr rotate_copy(forwardItr first, forwardItr middle,
                      forwardItr last,
                      outputItr destFirst);
```

范围 `first...last-1` 中的元素按旋转后的顺序复制到目标范围，从 `destFirst` 开始，使得范围 `first...last-1` 中由 `middle` 指定的元素成为目标的第一个元素。该函数还返回目标位置中最后一个被复制元素之后的位置。

算法 `reverse`、`reverse_copy`、`rotate` 和 `rotate_copy` 包含在头文件 `algorithm` 中。示例 21-24 中的程序说明了如何使用这些算法。

# 示例 21-24

```cpp
//STL functions reverse, reverse_copy, rotate, and rotate_copy

#include <iostream>                                      //Line 1
#include <algorithm>                                     //Line 2
#include <iterator>                                      //Line 3
#include <list>                                          //Line 4

using namespace std;                                     //Line 5

int main()                                               //Line 6
{
    list<int> intList = { 1, 3, 5, 7, 9, 0, 2,         //Line 7
                          4, 6, 8 };                   //Line 8
    list<int> resultList;                                //Line 9
    list<int>::iterator listItr;                         //Line 10

    ostream_iterator<int> screen(cout, " ");            //Line 11

    cout << "Line 12: intList: ";                       //Line 12
    copy(intList.begin(), intList.end(), screen);        //Line 13
    cout << endl;                                        //Line 14

             //reverse
    reverse(intList.begin(), intList.end());             //Line 15

    cout << "Line 16: intList after reversal: ";        //Line 16
    copy(intList.begin(), intList.end(), screen);        //Line 17
    cout << endl;                                        //Line 18
```

