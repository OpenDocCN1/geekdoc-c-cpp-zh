
## 示例21-25

```cpp
//STL Functions for_each and transform

#include <iostream>
#include <cctype>
#include <algorithm>
#include <iterator>
#include <vector>

using namespace std;

void doubleNum(int& num);

int main()
{
    char cList[5] = {'a', 'b', 'c', 'd', 'e'};        //Line 1

    vector<char> charList(cList, cList + 5);          //Line 2

    ostream_iterator<char> screen(cout, " ");        //Line 3

    cout << "Line 4: cList: ";                       //Line 4
    copy(charList.begin(), charList.end(), screen);   //Line 5
    cout << endl;                                     //Line 6

    //transform
    transform(charList.begin(), charList.end(),
              charList.begin(), toupper);             //Line 7

    cout << "Line 8: cList after changing all "       //Line 8
         << "lowercase letters to \n"
         << "        uppercase letters: ";           //Line 9
    copy(charList.begin(), charList.end(), screen);   //Line 10
    cout << endl;                                     //Line 11

    int list[7] = {2, 8, 5, 1, 7, 11, 3};             //Line 12

    ostream_iterator<int> screenOut(cout, " ");      //Line 13

    cout << "Line 13: list: ";                       //Line 14
    copy(list, list + 7, screenOut);                  //Line 15
    cout << endl;

    cout << "Line 16: The effect of for_each "       //Line 16
         << "function:\n        ";

    //for_each                                      //Line 17
    for_each(list, list + 7, doubleNum);             //Line 18
    cout << endl;

    cout << "Line 19: list after a call to "
         << "for_each function:\n        ";                 //Line 19
    copy(list, list + 7, screenOut);                         //Line 20
    cout << endl;                                             //Line 21

    return 0;
}

void doubleNum(int& num)
{
    num = 2 * num;

    cout << num << " ";
}
```

### 示例运行：

```text
Line 4: cList: a b c d e
Line 8: cList after changing all lowercase letters to
         uppercase: A B C D E
Line 13: list: 2 8 5 1 7 11 3
Line 16: The effect of for_each function:
         4 16 10 2 14 22 6
Line 19: list after a call to for_each function:
         4 16 10 2 14 22 6
```

第7行中的语句使用函数 transform 将 charList 中的每个小写字母变成其对应的大写字母。第9行中的语句输出 charList 的元素。在输出中，标记为第8行的行包含程序中第8到10行语句的输出。注意，函数 transform（第7行）的第四个参数是来自头文件 cctype 的函数 toupper。

第17行中的语句调用函数 for_each，使用函数 doubleNum 处理 list 中的每个元素。函数 doubleNum 有一个引用参数 num，类型为 int。此外，该函数将 num 的值加倍，然后输出 num 的值。因为 num 是引用参数，所以实际参数的值会被改变。在输出中，标记为第16行的行包含函数 doubleNum 中 cout 语句产生的输出，该函数作为函数 for_each 的第三个参数传递（见第17行）。第20行中的语句输出 list 元素的值。在输出中，第19行包含第19到20行语句的输出。

## 函数 `includes`、`set_intersection`、`set_union`、`set_difference` 和 `set_symmetric_difference`

本节描述集合运算：includes（子集）、set_intersection、set_union、set_difference 和 set_symmetric_difference。所有这些算法都假设每个给定范围内的元素已经排序。

算法 includes 确定一个范围内的元素是否出现在另一个范围内。该函数有两种形式，如下面的原型所示：

```cpp
template <class inputItr1, class inputItr2>
bool includes(inputItr1 first1, inputItr1 last1,
              inputItr2 first2, inputItr2 last2);

template <class inputItr1, class inputItr2,
          class binaryPredicate>
bool includes(inputItr1 first1, inputItr1 last1,
              inputItr2 first2, inputItr2 last2,
              binaryPredicate op);
```

函数 includes 的两种形式都假设范围 first1...last1-1 和 first2...last2-1 中的元素按照相同的排序标准排序。如果范围 first2...last2-1 中的所有元素也都在 first1...last1-1 中，则函数返回 true。换句话说，如果 first1...last1-1 包含范围 first2...last2-1 中的所有元素，则函数返回 true。第一种形式假设两个范围内的元素都按升序排列。第二种形式使用操作 op 来确定元素的顺序。

示例21-26说明了函数 includes 的工作原理。

## 示例21-26

```cpp
//STL function includes
//This function assumes that the elements in the given ranges
//are ordered according to some sorting criteria

#include <iostream>
#include <algorithm>
#include <iterator>

using namespace std;

int main()
{
    char setA[5] = {'A', 'B', 'C', 'D', 'E'};       //Line 1
    char setB[10] = {'A', 'B', 'C', 'D', 'E',       //Line 2
                     'F', 'I', 'J', 'K', 'L'};      //Line 3
    char setC[5] = {'A', 'E', 'I', 'O', 'U'};        //Line 4
    ostream_iterator<char> screen(cout, " ");      //Line 5
    cout << "Line 5: setA: ";
    copy(setA, setA + 5, screen);                        //Line 6
    cout << endl;                                         //Line 7

    cout << "Line 8: setB: ";
    copy(setB, setB + 10, screen);                        //Line 8
    cout << endl;                                         //Line 9
                                                          //Line 10

    cout << "Line 11: setC: ";
    copy(setC, setC + 5, screen);                         //Line 11
    cout << endl;                                         //Line 12
                                                          //Line 13

    if (includes(setB, setB + 10, setA, setA + 5))        //Line 14
        cout << "Line 15: setA is a subset of "           //Line 15
             << "setB." << endl;                          //Line 16
    else
        cout << "Line 17: setA is not a subset "          //Line 17
             << "of setB." << endl;

    if (includes(setB, setB + 10, setC, setC + 5))        //Line 18
        cout << "Line 19: setC is a subset of "           //Line 19
             << "setB." << endl;                          //Line 20
    else
        cout << "Line 21: setC is not a subset "          //Line 21
             << "of setB." << endl;

    return 0;
}
```

### 示例运行：

```text
Line 5: setA: A B C D E
Line 8: setB: A B C D E F I J K L
Line 11: setC: A E I O U
Line 15: setA is a subset of setB
Line 21: setC is not a subset of setB
```

上述输出不言自明。具体细节留给读者作为练习。

算法 set_intersection 用于查找两个元素范围内共有的元素。该算法有两种形式，如下面的原型所示：

```cpp
template <class InputItr1, class InputItr2,
          class OutputItr>
OutputItr set_intersection(InputItr1 first1, InputItr1 last1,
                           InputItr2 first2, InputItr2 last2,
                           OutputItr destFirst);

template <class inputItr1, class inputItr2,
          class outputItr, class binaryPredicate>
outputItr set_intersection(inputItr1 first1, inputItr1 last1,
                           inputItr2 first2, inputItr2 last2,
                           outputItr destFirst,
                           binaryPredicate op);
```

两种形式都会创建一个有序序列，其中的元素是两个有序范围 first1...last1-1 和 first2...last2-1 所共有的元素。创建的序列被放置在从 destFirst 开始的容器中。两种形式都返回一个迭代器，该迭代器指向目标范围中最后一个被复制元素之后的位置。第一种形式假设元素按升序排列；第二种形式假设两个范围都使用 op 指定的操作进行排序。源范围中的元素不会被修改。

假设：

```cpp
setA[5] = {2, 4, 5, 7, 8};
setB[7] = {1, 2, 3, 4, 5, 6, 7};
setC[5] = {2, 5, 8, 8, 15};
setD[6] = {1, 4, 4, 6, 7, 12};
setE[7] = {2, 3, 4, 4, 5, 6, 10};
```

那么：

```cpp
AintersectB = {2, 4, 5, 7}
AintersectC = {2, 5, 8}
DintersectE = {4, 4, 6}
```

注意，因为 8 只在 setA 中出现一次，所以 8 在 AintersectC 中只出现一次，尽管 8 在 setC 中出现了两次。然而，因为 4 在 setD 和 setE 中都出现了两次，所以 4 在 DintersectE 中也出现了两次。

算法 set_union 用于查找两个元素范围内包含的元素。该算法有两种形式，如下面的原型所示：

```cpp
template <class inputItr1, class inputItr2,
          class outputItr>
outputItr set_union(inputItr1 first1, inputItr1 last1,
                    inputItr2 first2, inputItr2 last2,
                    outputItr destFirst);

template <class inputItr1, class inputItr2,
          class outputItr, class binaryPredicate>
outputItr set_union(inputItr1 first1, inputItr1 last1,
                    inputItr2 first2, inputItr2 last2,
                    outputItr destFirst,
                    binaryPredicate op);
```

两种形式都会创建一个有序序列，其中的元素出现在两个有序范围 first1...last1-1 或 first2...last2-1 中的任意一个中。创建的序列被放置在从 destFirst 开始的容器中。两种形式都返回一个迭代器，该迭代器指向目标范围中最后一个被复制元素之后的位置。第一种形式假设元素

