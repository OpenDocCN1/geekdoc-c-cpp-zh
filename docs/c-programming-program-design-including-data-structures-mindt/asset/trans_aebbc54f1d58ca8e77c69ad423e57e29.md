

```cpp
generate(vecList.begin(), vecList.end(), nextNum);  //Line 11

cout << "Line 12: vecList after filling with "
     << "numbers: ";                              //Line 12

copy(vecList.begin(), vecList.end(), screen);       //Line 13
cout << endl;                                        //Line 14

generate_n(vecList.begin(), 3, nextNum);            //Line 15

cout << "Line 16: vecList after filling the "
     << "first three elements" << endl
     << "    with the next number: ";               //Line 16

copy(vecList.begin(), vecList.end(), screen);       //Line 17
cout << endl;                                        //Line 18

return 0;                                           //Line 19
}                                                    //Line 20

int nextNum()                                        //Line 21
{                                                    //Line 22
    static int n = 1;                                //Line 23

    return n++;                                      //Line 24
}                                                    //Line 25
```

### 示例运行

```text
Line 12: vecList after filling with numbers: 1 2 3 4 5 6 7 8
Line 16: vecList after filling the first three elements
    with the next number: 9 10 11 4 5 6 7 8
```

该程序包含一个带返回值的函数 nextNum，其中有一个初始化为 1 的静态变量 n。调用该函数会返回 n 的当前值，然后将 n 的值递增。因此，第一次调用 nextNum 返回 1，第二次调用返回 2，依此类推。

第 9 行和第 10 行的语句将 vecList 声明为大小为 8 的序列容器，并将 screen 声明为以 cout 初始化、以空格字符作为分隔符的 ostream 迭代器。第 11 行的语句使用函数 generate，通过连续调用函数 nextNum 来填充 vecList。注意，第 11 行的语句执行后，nextNum 的静态变量 n 的值为 9。第 13 行的语句输出 vecList 的元素。第 15 行的语句调用函数 generate_n，通过调用函数 nextNum 三次来填充 vecList 的前三个元素。起始位置是 vecList.begin()，即 vecList 的第一个元素，而要填充的元素个数为 3，由 generate_n 的第二个参数给出（见第 15 行）。第 17 行的语句输出 vecList 的元素。

## 函数 find、find_if、find_end 和 find_first_of

函数 find、find_if、find_end 和 find_first_of 用于在给定范围内查找元素。这些函数定义在头文件 algorithm 中。函数 find 和 find_if 的原型如下：

```cpp
template <class inputItr, class size, class Type>
inputItr find(inputItr first, inputItr last,
              const Type& searchValue);

template <class inputItr, class unaryPredicate>
inputItr find_if(inputItr first, inputItr last, unaryPredicate op);
```

函数 find 在元素范围 first...last-1 中查找元素 searchValue。如果在范围内找到 searchValue，该函数返回 searchValue 在范围内被找到的位置；否则，它返回 last。函数 find_if 在元素范围 first...last-1 中查找使 op(rangeElement) 为真的元素。如果找到满足 op(rangeElement) 为真的元素，它返回给定范围中该元素被找到的位置；否则，它返回 last。

示例 21-17 中的程序说明了如何使用函数 find 和 find_if。

### 示例 21-17

```cpp
//STL Functions find and find_if

#include <iostream>                     //Line 1
#include <cctype>                       //Line 2
#include <algorithm>                    //Line 3
#include <iterator>                     //Line 4
#include <vector>                       //Line 5

using namespace std;                    //Line 6

int main()                              //Line 7
{                                       //Line 8
    vector<char> charList = {'a', 'i', 'C', 'd',
                             'e', 'f', 'o', 'H',
                             'u', 'j'};                  //Line 9

    ostream_iterator<char> screen(cout, " ");            //Line 10

    cout << "Line 11: Character list: ";                 //Line 11
    copy(charList.begin(), charList.end(), screen);      //Line 12
    cout << endl;                                        //Line 13

    vector<char>::iterator position;                     //Line 14

    //find
    position = find(charList.begin(),
                    charList.end(), 'd');                 //Line 15

    if (position != charList.end())                       //Line 16
        cout << "Line 17: The element is found "
             << "at position "
             << (position - charList.begin())
             << endl;                                     //Line 17
    else                                                   //Line 18
        cout << "Line 19: The element is not "
             << "in the list." << endl;                  //Line 19

    //find_if
    position = find_if(charList.begin(),
                       charList.end(), isupper);          //Line 20

    if (position != charList.end())                       //Line 21
        cout << "Line 22: The first uppercase "
             << "letter is found at position "
             << (position - charList.begin())
             << endl;                                     //Line 22
    else                                                   //Line 23
        cout << "Line 24: The element is not "
             << "in the list." << endl;                  //Line 24

    return 0;                                              //Line 25
}                                                      //Line 26
```

### 示例运行

```text
Line 11: Character list: a i C d e f o H u j
Line 17: The element is found at position 3
Line 22: The first uppercase letter is found at position 2
```

第 9 行的语句创建并初始化 vector 容器 charList。第 10 行的语句创建一个 ostream 迭代器。第 12 行的语句输出 charList。（在输出中，标记为 Line 11 的行包含程序第 11 行到第 13 行的输出。）第 14 行的语句声明类型为 vector<char> 的迭代器 position。第 15 行的语句在 charList 中查找第一次出现的 'd'，并返回一个迭代器，将其存储在 position 中。第 16 行到第 19 行的语句输出查找结果。因为 'd' 是 charList 中的第四个字符，所以其位置为 3。（在输出中，见标记为 Line 17 的行。）第 20 行的语句使用函数 find_if 查找 charList 中的第一个大写字符。注意，来自头文件 cctype 的函数 isupper 作为第三个参数传递给函数 find_if（见第 20 行）。第 21 行到第 24 行的语句输出查找结果。`charList` 中的第一个大写字符是 'C'，它是 `charList` 的第三个元素；其位置为 2。（在输出中，见标记为 Line 22 的行。）

接下来，我们描述函数 `find_end` 和 `find_first_of`。这两个函数都有两种形式。函数 `find_end` 的原型如下：

```cpp
template <class forwardItr1, class forwardItr2>
forwardItr1 find_end(forwardItr1 first1, forwardItr1 last1,
                     forwardItr2 first2, forwardItr2 last2);

template <class forwardItr1, class forwardItr2,
          class binaryPredicate>
forwardItr1 find_end(forwardItr1 first1, forwardItr1 last1,
                    forwardItr2 first2, forwardItr2 last2,
                    binaryPredicate op);
```

函数 `find_end` 的两种形式都在范围 `first1...last1-1` 中查找范围 `first2...last2-1` 作为子范围的最后一次出现。如果查找成功，该函数返回匹配发生在 `first1...last1-1` 中的位置；否则，它返回 `last1`。也就是说，函数 `find_end` 返回范围 `first1...last1-1` 中最后一个元素的位置，在该位置处范围 `first2...last2-1` 是 `first1...last1-1` 的子范围。在第一种形式中，元素按相等性进行比较；在第二种形式中，比较 op(`elementFirstRange`, `elementSecondRange`) 必须为真。

函数 `find_first_of` 的原型如下：

```cpp
template <class forwardItr1, class forwardItr2>
forwardItr1 find_first_of(forwardItr1 first1, forwardItr1 last1,
                          forwardItr2 first2, forwardItr2 last2);

template <class forwardItr1, class forwardItr2,
          class binaryPredicate>
forwardItr1 find_first_of(forwardItr1 first1, forwardItr1 last1,
                         forwardItr2 first2, forwardItr2 last2,
                         binaryPredicate op);
```

第一种形式返回 `first2...last2-1` 中第一个也位于范围 `first1...last1-1` 中的元素在 `first1...last1-1` 内的位置。第二种形式返回 `first2...last2-1` 中第一个使 `op(elemRange1, elemRange2)` 为真的元素在 `first1...last1-1` 内的位置。如果未找到匹配项，两种形式都返回 `last1`。

示例 21-18 中的程序说明了如何使用函数 `find_end` 和 `find_first_of`。

