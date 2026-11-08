
```cpp
cout << "Line 6: vecList1: ";                    //Line 6
copy(vecList1.begin(), vecList1.end(),
     screenOut);                                  //Line 7
cout << endl;                                     //Line 8

copy(vecList1.begin(), vecList1.end(),
     inserter(vecList2, vecList2.begin()));       //Line 9

cout << "Line 10: vecList2: ";                  //Line 10
copy(vecList2.begin(), vecList2.end(),
     screenOut);                                  //Line 11
cout << endl;                                     //Line 12

list<int> tempList;                               //Line 13

copy(vecList2.begin(), vecList2.end(),
     front_inserter(tempList));                   //Line 14

cout << "Line 15: tempList: ";                   //Line 15
copy(tempList.begin(), tempList.end(),
     screenOut);                                  //Line 16
cout << endl;                                     //Line 17

return 0;
}
```

**示例运行：**

```
Line 6: vecList1: 1 2 3 4 5 6 7 8
Line 10: vecList2: 1 2 3 4 5 6 7 8
Line 15: tempList: 8 7 6 5 4 3 2 1
```

## STL 算法

接下来的章节将介绍大多数 STL 算法。对于每种算法，我们都会给出函数原型、算法功能的简要描述，以及展示如何使用它的程序。在函数原型中，参数类型指明了该算法适用的容器类型。例如，如果参数类型是 randomAccessIterator，则该算法仅适用于随机访问类型的容器，如 vector。在整个过程中，我们使用诸如 outputItr 这样的形容词来表示输出迭代器，inputItr 表示输入迭代器，forwardItr 表示前向迭代器，等等。

### 函数 `fill` 和 `fill_n`

函数 `fill` 用于向容器中填充元素；函数 `fill_n` 用于填充接下来的 n 个元素。用作填充元素的元素将作为参数传递给这些函数。这两个函数都定义在头文件 algorithm 中。这些函数的原型如下：

第1行和第2行的语句声明 vecList 为一个大小为8的序列容器，screen 为一个初始化为 cout 且以空格作为分隔符的 ostream 迭代器。第3行的语句使用函数 `fill` 将 vecList 填充为 2；也就是说，vecList 的所有八个元素都被设置为 2。回顾一下，vecList.begin() 返回指向 vecList 第一个元素的迭代器，vecList.end() 返回指向 vecList 最后一个元素之后一个位置的迭代器。第5行的语句使用 `copy` 函数输出 vecList 的元素。第7行的语句使用函数 `fill_n` 将 5 存储到 vecList 的元素中。`fill_n` 的第一个参数是 vecList.begin()，它指定开始复制的起始位置。`fill_n` 的第二个参数是 3，它指定要填充的元素个数。第三个参数 5 指定填充字符。因此，5 被复制到 vecList 的前三个元素中。第9行的语句输出 vecList 的元素。

### 函数 `generate` 和 `generate_n`

函数 `generate` 和 `generate_n` 用于生成元素并填充序列。这两个函数定义在头文件 algorithm 中。这些函数的原型如下：

```cpp
template <class forwardItr, class function>
void generate(forwardItr first, forwardItr last, function gen);

template <class forwardItr, class size, class function>
void generate_n(forwardItr first, size n, function gen);
```

函数 `generate` 通过连续调用函数 gen() 来填充范围 first...last-1 内的序列。函数 `generate_n` 通过连续调用函数 gen() 来填充范围 first...first+n-1 内的序列，即从位置 first 开始。注意，gen 也可以是一个指向函数的指针。此外，如果 gen 是一个函数，它必须是一个不带参数并返回值的函数。示例 21-15 中的程序说明了如何使用这些函数。

**示例 21-15**

```cpp
//STL Functions generate and generate_n

#include <iostream>
#include <algorithm>
#include <iterator>
#include <vector>

using namespace std;

int nextNum();

int main()
{
    vector<int> vecList(8);

    ostream_iterator<int> screen(cout, " ");

    generate(vecList.begin(), vecList.end(), nextNum); //Line 1

    cout << "Line 4: vecList after filling with "
         << " numbers: "; //Line 4

    copy(vecList.begin(), vecList.end(), screen); //Line 5
    cout << endl; //Line 6

    generate_n(vecList.begin(), 3, nextNum); //Line 7

    cout << "Line 8: vecList after filling the "
         << "first three elements " << endl
         << " with the next number: "; //Line 8

    copy(vecList.begin(), vecList.end(), screen); //Line 9
    cout << endl; //Line 10

    return 0;
}

int nextNum()
{
    static int n = 1;

    return n++;
}
```

**示例运行：**

```
Line 4: vecList after filling with numbers: 1 2 3 4 5 6 7 8
Line 8: vecList after filling the first three elements
        with the next number: 9 10 11 4 5 6 7 8
```

该程序包含一个返回值函数 nextNum，其中包含一个初始化为 1 的静态变量 n。对该函数的调用返回 n 的当前值，然后将 n 的值加 1。因此，第一次调用 nextNum 返回 1，第二次调用返回 2，依此类推。

第1行和第2行的语句声明 vecList 为一个大小为8的序列容器，screen 为一个初始化为 cout 且以空格作为分隔符的 ostream 迭代器。第3行的语句使用函数 `generate` 通过连续调用函数 nextNum 来填充 vecList。注意，在第3行的语句执行后，nextNum 的静态变量 n 的值为 9。第5行的语句输出 vecList 的元素。第7行的语句调用函数 `generate_n`，通过三次调用函数 nextNum 来填充 vecList 的前三个元素。起始位置是 vecList.begin()，即 vecList 的第一个元素，要填充的元素个数为 3，由 `generate_n` 的第二个参数给出（见第7行）。第9行的语句输出 vecList 的元素。

### 函数 `find`、`find_if`、`find_end` 和 `find_first_of`

函数 `find`、`find_if`、`find_end` 和 `find_first_of` 用于在给定范围内查找元素。这些函数定义在头文件 algorithm 中。函数 `find` 和 `find_if` 的原型如下：

```cpp
template <class inputItr, class size, class Type>
inputItr find(inputItr first, inputItr last,
              const Type& searchValue);

template <class inputItr, class unaryPredicate>
inputItr find_if(inputItr first, inputItr last, unaryPredicate op);
```

函数 `find` 在元素范围 first...last-1 中搜索元素 searchValue。如果在范围内找到 searchValue，函数返回范围内找到 searchValue 的位置；否则返回 last。函数 `find_if` 在元素范围 first...last-1 中搜索使 op(rangeElement) 为 true 的元素。如果找到满足 op(rangeElement) 为 true 的元素，则返回给定范围内该元素的位置；否则返回 last。

示例 21-16 中的程序说明了如何使用函数 `find` 和 `find_if`。

**示例 21-16**

```cpp
//STL Functions find and find_if

#include <iostream>
#include <cctype>
#include <algorithm>
#include <iterator>
#include <vector>

using namespace std;

int main()
{
    char cList[10] = {'a', 'i', 'C', 'd', 'e',
                      'f', 'o', 'H', 'u', 'j'};

    vector<char> charList(cList, cList + 10);        //Line 2

    ostream_iterator<char> screen(cout, " ");          //Line 3

    cout << "Line 4: Character list: ";                  //Line 4
    copy(charList.begin(), charList.end(), screen);      //Line 5
    cout << endl;                                        //Line 6

    vector<char>::iterator position;                     //Line 7

            //find it
    position = find(charList.begin(),
                   charList.end(), 'd');                 //Line 8

    if (position != charList.end())                      //Line 9
        cout << "Line 10: The element is found at "
             << "position "
             << (position - charList.begin())            //Line 10
             << endl;                                    //Line 11
    else
        cout << "Line 12: The element is not in "
             << "the list." << endl;                    //Line 12

            //find_if
    position = find_if(charList.begin(),
                       charList.end(), isupper);         //Line 13

    if (position != charList.end())                      //Line 14
        cout << "Line 15: The first uppercase "
             << "letter is found at position "
             << (position - charList.begin())            //Line 15
             << endl;                                    //Line 16
    else
        cout << "Line 17: The element is not in "
             << "the list." << endl;                    //Line 17

    return 0;
}
```

**示例运行：**

```
Line 4: Character list: a i C d e f o H u j
Line 10: The element is found at position 3
Line 15: The first uppercase letter is found at position 2
```

第1行的语句创建并初始化一个包含10个元素的字符数组 cList。第2行的语句创建 vector 容器 charList，并使用字符数组 cList 对其进行初始化。第3行的语句创建一个 ostream 迭代器。第5行的语句输出 charList。（在输出中，标记为第4行的行包含程序第4到6行的输出。）第7行的语句声明一个类型为 vector<char> 的迭代器 position。第8行的语句在 charList 中搜索 'd' 的首次出现，并返回一个迭代器，存储到 position 中。第9到12行的语句输出搜索的结果。因为 'd' 是 charList 中的第四个字符，所以它的位置是 3。

