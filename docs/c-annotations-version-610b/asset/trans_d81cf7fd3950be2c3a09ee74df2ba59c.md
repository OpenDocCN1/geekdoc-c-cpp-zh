
分层标准。这个示例值得进一步关注：

- 首先，在`// 1`处，围绕`std::pair<std::string, std::string>`创建了一个包装结构体`Pss`。一旦C++11标准支持在派生类中直接使用基类构造函数（参见第13.3节），创建这个结构体就会变得更加简单。这里的意图是定义一个类型，它包装一个在`std`命名空间中定义的类，而该类没有定义插入操作。这种结构体设计与第14.7节概述的原则相冲突。不过，在这里使用继承是可以辩护的，因为目的并不是添加“缺失的功能”，而且`pair`本身本质上只是Plain Old Data（纯旧数据）。
- 接下来（`// 2`），为`Pss`对象重载了`operator<<`。尽管如果为`pair<string, string>`类型在`std`命名空间中定义这个运算符，编译器也不会抱怨，但这同样会是一种糟糕的风格，因为`std`命名空间对普通程序来说是*禁区*。通过围绕`pair<string, string>`定义包装类型，可以避免这种风格。
- 然后（`// 3`），定义了一个类`Sortby`，允许我们构造一个匿名对象，该对象接收一个指向用于排序的`Pss`数据成员之一的指针。在这种情况下，由于两个成员都是字符串对象，其构造函数可以很容易地定义。它期望一个指向`Pss`类的字符串成员的指针。
- `Sortby`的`operator()`成员（`// 4`）接收两个`Pss`对象的引用，并使用其成员指针来比较`Pss`对象的相应字段。
- 在`main`中，一些数据存储在一个vector中（`// 5`）。
- 然后（`// 6`）进行第一次排序。最不重要的标准必须首先排序，为此一个简单的`sort`就足够了。由于我们希望名字在城市内部排序，名字代表最不重要的标准，因此我们按名字排序：`Sortby(&Pss::first)`。
- 下一个重要标准是城市，接下来对城市排序（`// 7`）。由于`stable_sort`不再改变名字的相对顺序，在按城市排序时观察到的并列情况会以不破坏现有相对顺序的方式解决。因此，我们最终得到Eugene中的Goldberg排在Eugene中的Hampson之前，再排在Eugene中的Moran之前。为了按城市排序，我们使用另一个匿名`Sortby`对象：`Sortby(&Pss::second)`。

## 19.1.61 swap

- 头文件：`<algorithm>`
- 函数原型：
  - `void swap(Type &object1, Type &object2);`
- 描述：
  - 元素`object1`和`object2`交换它们的值。它们通过循环复制赋值或循环移动赋值（如果可用）来完成交换。
- 示例：

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <iterator>
using namespace std;

int main()
{
    string first[] = {"alpha", "bravo", "charley"};
    string second[] = {"echo", "foxtrot", "golf"};
    size_t const n = sizeof(first) / sizeof(string);

    swap_ranges(first, first + n, second);

    cout << "After:\n";
    copy(first, first + n, ostream_iterator<string>(cout, " "));
    cout << '\n';
    copy(second, second + n, ostream_iterator<string>(cout, " "));
    cout << '\n';
}
/*
    Displays:
        Before:
        alpha bravo charley
        echo foxtrot golf
        After:
        echo foxtrot golf
        alpha bravo charley
*/
```

## 19.1.63 transform

- 头文件：`<algorithm>`
- 函数原型：
  - `OutputIterator transform(InputIterator first, InputIterator last, OutputIterator result, UnaryOperator op);`
  - `OutputIterator transform(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, OutputIterator result, BinaryOperator op);`
- 描述：
  - 第一个原型：一元运算符op应用于范围`[first, last)`中的每个元素，结果值存储在从result开始的范围中。返回值指向最后生成元素之后的位置。
  - 第二个原型：二元运算符op应用于范围`[first1, last1)`中的每个元素以及从first2开始的第二个范围中的对应元素。结果值存储在从result开始的范围中。返回值指向最后生成元素之后的位置。
- 示例：

```cpp
#include <functional>
#include <vector>
#include <algorithm>
#include <iostream>
#include <string>
#include <cctype>
#include <iterator>
using namespace std;

string caps(string const &src)
{
    string tmp;
    tmp.resize(src.length());

    transform(src.begin(), src.end(), tmp.begin(), ::toupper);
    return tmp;
}

int main()
{
    string words[] = {"alpha", "bravo", "charley"};

    copy(words, transform(words, words + 3, caps),
         ostream_iterator<string>(cout, " "));
    cout << '\n';

    int        values[] = {1, 2, 3, 4, 5};
    vector<int> squares;

    transform(values, values + 5, values,
              back_inserter(squares), multiplies<int>());

    copy(squares.begin(), squares.end(),
         ostream_iterator<int>(cout, " "));
    cout << '\n';
}
/*
    Displays:
        ALPHA BRAVO CHARLEY
        1 4 9 16 25
*/
```

应当注意`for_each`（第19.1.17节）和`transform`泛型算法之间的以下差异：

- 使用`transform`时，使用的是函数对象`operator()`成员的*返回值*；传递给`operator()`成员本身的参数不会被改变。
- 使用`for_each`时，函数对象的`operator()`接收一个参数的引用，该参数本身可能会被函数对象的`operator()`改变。

## 19.1.64 unique

- 头文件：`<algorithm>`
- 函数原型：
  - `ForwardIterator unique(ForwardIterator first, ForwardIterator last);`
  - `ForwardIterator unique(ForwardIterator first, ForwardIterator last, BinaryPredicate pred);`
- 描述：
  - 第一个原型：使用迭代器所指向数据类型的`operator==`，在`[first, last)`指向的范围中，除第一个之外的所有连续相等元素都被重新安置到该范围的末尾。返回的前向迭代器标记*剩余部分*的开始。范围`[first, return-value)`中的所有元素都是唯一的，范围`[return-value, last)`中的所有元素都等于范围`[first, return-value)`中的元素。
  - 第二个原型：在`[first, last)`指向的范围中，对于二元谓词`pred`（期望两个迭代器所指向数据类型的参数）返回`true`的连续元素，除第一个之外的所有元素都被重新安置到该范围的末尾。返回的前向迭代器标记*剩余部分*的开始。对于范围`[first, return-value)`中的所有元素对，`pred`返回`false`（即它们是唯一的），而对于一个组合，其第一操作数是范围`[return-value, last)`中的元素，第二操作数是范围`[first, return-value)`中的元素，`pred`返回`true`。
- 示例：

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <cstring>
#include <iterator>
using namespace std;

bool casestring(string const &first, string const &second)
{
    return strcasecmp(first.c_str(), second.c_str()) == 0;
}
int main()
{
    string words[] = {"alpha", "alpha", "Alpha", "papa", "quebec"};
    size_t const size = sizeof(words) / sizeof(string);

    string *removed = unique(words, words + size);
    copy(words, removed, ostream_iterator<string>(cout, " "));
    cout << '\n';
    cout << "Trailing elements are:\n";
    copy(removed, words + size, ostream_iterator<string>(cout, " "));
    cout << '\n';

    removed = unique(words, words + size, casestring);
    copy(words, removed, ostream_iterator<string>(cout, " "));
    cout << '\n';
    cout << "Trailing elements are:\n";
    copy(removed, words + size, ostream_iterator<string>(cout, " "));
    cout << '\n';
}
/*
    Displays:
        alpha Alpha papa quebec
        Trailing elements are:
        quebec
        alpha papa quebec
        Trailing elements are:
        quebec quebec
*/
```

## 19.1.65 unique_copy

- 头文件：`<algorithm>`
- 函数原型：
  - `OutputIterator unique_copy(InputIterator first, InputIterator last, OutputIterator result);`
  - `OutputIterator unique_copy(InputIterator first, InputIterator last, OutputIterator result, BinaryPredicate pred);`
- 描述：
  - 第一个原型：范围`[first, last)`中的元素被复制到结果容器中，从`result`开始。连续相等的元素（使用迭代器所指向数据类型的`operator==`）只复制一次（保留一系列相等元素中的第一个）。返回的输出迭代器指向最后复制的元素之后的位置。
