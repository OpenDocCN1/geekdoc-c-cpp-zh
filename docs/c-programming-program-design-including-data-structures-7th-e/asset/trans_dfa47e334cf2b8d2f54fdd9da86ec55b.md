
（在输出中，标记为 Line 18 的那一行包含程序第 18 行至第 20 行的输出。）

第 22 行的语句创建向量 intList，并使用第 21 行声明的数组对其进行初始化。第 25 行的语句输出 intList 各元素的值。第 27 行的语句使用函数 swap_ranges 将 intList 的前四个元素与 intList 中从第六个元素开始的四个元素交换。第 29 行的语句输出 intList 的元素。（在输出中，标记为 Line 28 的那一行包含程序第 28 行至第 30 行的输出。）

第 31 行的语句将数组 list 的元素与向量 intList 的元素交换。第 34 行的语句输出数组 list 的元素，第 37 行的语句输出 intList。

## 函数 `search`、`search_n`、`sort` 和 `binary_search`

函数 search、search_n、sort 和 binary_search 用于搜索和排序元素。这些函数定义在头文件 algorithm 中。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1570_0.png)

函数 search 的原型为：

```cpp
template <class forwardItr1, class forwardItr2>
forwardItr1 search(forwardItr1 first1, forwardItr1 last1,
                   forwardItr2 first2, forwardItr2 last2);
```

```cpp
template <class forwardItr1, class forwardItr2,
          class binaryPredicate>
forwardItr1 search(forwardItr1 first1, forwardItr1 last1,
                  forwardItr2 first2, forwardItr2 last2,
                  binaryPredicate op);
```

给定两个元素范围 first1...last1−1 和 first2...last2−1，函数 search 在范围 first1...last1−1 中搜索范围 first2...last2−1 作为其子范围首次出现的位置。第一种形式对两个范围的元素进行相等比较。对于第二种形式，比较 op(elemFirstRange, elemSecondRange) 必须为 true。如果找到匹配项，函数返回范围 first1...last1−1 中发生匹配的位置；否则，函数返回 last1。

函数 search_n 的原型为：

```cpp
template <class forwardItr, class size, class Type>
forwardItr search_n(forwardItr first, forwardItr last,
                     size count, const Type& value);
```

```cpp
using namespace std;

int main()
{
    int intList[15] = {12, 34, 56, 34, 34,
                       78, 38, 43, 12, 25,
                       34, 56, 62, 5, 49};

    vector<int> vecList(intList, intList + 15);
    int list[2] = {34, 56};

    vector<int>::iterator location;

    ostream_iterator<int> screenOut(cout, " ");

    cout << "Line 6: vecList: ";
    copy(vecList.begin(), vecList.end(), screenOut);
    cout << endl;

    cout << "Line 9: list: ";
    copy(list, list + 2, screenOut);
    cout << endl;

    //search
    location = search(vecList.begin(), vecList.end(),
                      list, list + 2);

    if (location != vecList.end())
        cout << "Line 14: list found in vecList. "
             << "The first occurrence of " << endl
             << "the list in vecList is at "
             << "the position "
             << (location - vecList.begin()) << endl;
    else
        cout << "Line 16: list is not in vecList."
             << endl;

    //search_n
    location = search_n(vecList.begin(),
                        vecList.end(), 2, 34);

    if (location != vecList.end())
        cout << "Line 19: two consecutive "
             << "occurrences of 34 found in " << endl
             << "vecList at the position "
             << (location - vecList.begin()) << endl;
    else
        cout << "Line 21: vecList does not contain "
             << "two consecutive occurrences of 34."
             << endl;

    //sort
    sort(vecList.begin(), vecList.end());

    cout << "Line 23: vecList after sorting:"
         << endl << "        ";                  //Line 23
    copy(vecList.begin(), vecList.end(), screenOut); //Line 24
    cout << endl;                                  //Line 25

                 //binary_search
    bool found;                                    //Line 26

    found = binary_search(vecList.begin(),
                          vecList.end(), 78);      //Line 27

    if (found)                                     //Line 28
        cout << "Line 29: 78 found in vecList."
             << endl;                              //Line 29
    else                                           //Line 30
        cout << "Line 31: 78 not in vecList."
             << endl;                              //Line 31

    return 0;
}
```

### 示例运行：

```text
Line 6: vecList: 12 34 56 34 34 78 38 43 12 25 34 56 62 5 49
Line 9: list: 34 56
Line 14: list found in vecList. The first occurrence of
         list in vecList is at the position 1
Line 19: two consecutive occurrences of 34 found in
         vecList at the position 3
Line 23: vecList after sorting:
         5 12 12 25 34 34 34 34 38 43 49 56 56 62 78
Line 29: 78 found in vecList.
```

第 2 行的语句创建一个向量 vecList，并使用第 1 行创建的数组 intList 对其进行初始化。第 3 行的语句创建一个包含两个分量的数组 list，并初始化 list。第 7 行的语句输出 vecList。第 12 行的语句使用函数 search 搜索 vecList，以查找 list 作为子序列在 vecList 中首次出现的位置。第 13 行至第 16 行的语句输出搜索结果；参见输出中标记为 Line 14 的那一行。

第 17 行的语句使用函数 search_n 查找 vecList 中连续两个 34 出现的位置。第 18 行至第 21 行的语句输出搜索结果。

第 22 行的语句使用函数 sort 对 vecList 进行排序。第 24 行的语句输出 vecList。在输出中，标记为 Line 23 的那一行包含第 23 行至第 25 行语句的输出。

第 27 行的语句使用函数 binary_search 搜索 vecList。第 28 行至第 31 行的语句输出搜索结果。

## 函数 `adjacent_find`、`merge` 和 `inplace_merge`

算法 `adjacent_find` 用于查找满足特定条件的连续元素首次出现的位置。实现该算法的函数原型为：

```cpp
template <class forwardItr>
forwardItr adjacent_find(forwardItr first, forwardItr last);

template <class forwardItr, class binaryPredicate>
forwardItr adjacent_find(forwardItr first, forwardItr last,
                          binaryPredicate op);
```

`adjacent_find` 的第一种形式使用相等条件；也就是说，它查找同一元素首次连续出现的位置。在第二种形式中，算法返回范围 `first...last−1` 中某个元素的迭代器，使得 `op(elem, nextElem)` 为 true，其中 elem 是范围 `first...last−1` 中的一个元素，nextElem 是该范围中紧邻 elem 的下一个元素。如果未找到匹配元素，则两种算法都返回 `last`。

算法 `merge` 合并已排序的列表。结果是已排序的列表。两个列表必须按相同条件排序。例如，两个列表都应按升序或降序排列。实现 merge 算法的函数原型为：

```cpp
template <class inputItr1, class inputItr2, class outputItr>
outputItr merge(inputItr1 first1, inputItr1 last1,
                inputItr2 first2, inputItr2 last2,
                outputItr destFirst);
```

```cpp
template <class inputItr1, class inputItr2,
          class outputItr, class binaryPredicate>
outputItr merge(inputItr1 first1, inputItr1 last1,
                inputItr2 first2, inputItr2 last2,
                outputItr destFirst, binaryPredicate op);
```

算法 `merge` 的两种形式都合并已排序范围 `first1...last1−1` 和 `first2...last2−1` 的元素。以迭代器 `destFirst` 开始的目标范围包含合并后的元素。第一种形式使用小于运算符 < 对元素排序。第二种形式使用二元谓词 op 对元素排序；也就是说，`op(elemRange1, elemRange2)` 必须为 true。两种形式都返回目标范围中最后一个被复制元素的位置。此外，源范围不会被修改，并且目标范围不应与源范围重叠。

算法 `inplace_merge` 用于合并已排序的连续序列。实现该算法的函数原型为：
