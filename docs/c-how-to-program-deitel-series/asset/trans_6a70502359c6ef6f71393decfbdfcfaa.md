
函数参数不显示指针声明。这些参数实际上可以接收函数指针、函数对象（第 16.4 节）或 lambda 表达式（第 16.5 节）作为实参。因此，标准库使用更通用的名称来声明这类参数。

例如，C++ 标准文档中列出了 generate 算法的原型：

```cpp
template<class ForwardIterator, class Generator>
void generate(ForwardIterator first, ForwardIterator last,
              Generator gen);
```

这表明 generate 期望的实参是 ForwardIterator，用于表示要处理的元素范围，以及一个 Generator 函数。标准解释说，该算法会调用 Generator 函数，为 ForwardIterator 指定的范围内的每个元素获取一个值。标准还规定，Generator 必须不接收任何参数，并返回元素类型的值。

对于每个可以接收函数指针、函数对象或 lambda 表达式的算法，标准库都提供了类似的文档。在本章大多数示例中，每介绍一个算法时，我们都会说明这类参数的要求。我们通常以函数为背景这样做，并将函数指针传入算法。在第 16.4～16.5 节中，我们将讨论如何创建和使用可以传入算法的函数对象和 lambda 表达式。

## 16.3.2 equal、mismatch 和 lexicographical_compare

图 16.2 演示了使用算法 equal、mismatch 和 lexicographical_compare 比较值序列是否相等。

```cpp
// Fig. 16.2: fig16_02.cpp
// Algorithms equal, mismatch and lexicographical_compare.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <array> // array class-template definition
#include <iterator> // ostream_iterator
using namespace std;

int main()
{
    const size_t SIZE = 10;
    array<int, SIZE> a1 = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    array<int, SIZE> a2(a1); // initializes a2 with copy of a1
    array<int, SIZE> a3 = { 1, 2, 3, 4, 1000, 6, 7, 8, 9, 10 };
    ostream_iterator<int> output(cout, " ");

    cout << "a1 contains: ";
    copy(a1.cbegin(), a1.cend(), output);
    cout << "\na2 contains: ";
    copy(a2.cbegin(), a2.cend(), output);
    cout << "\na3 contains: ";
    copy(a3.cbegin(), a3.cend(), output);

    // compare a1 and a2 for equality
    bool result = equal(a1.cbegin(), a1.cend(), a2.cbegin());
    cout << "\na1 is " << (result ? "equal to" : "not equal to")
         << " a2.\n";

    // compare a1 and a3 for equality
    result = equal(a1.cbegin(), a1.cend(), a3.cbegin());
    cout << "\na1 is " << (result ? "equal to" : "not equal to")
         << " a3.\n";

    // check for mismatch between a1 and a3
    auto location = mismatch(a1.cbegin(), a1.cend(), a3.cbegin());
    cout << "\nThere is a mismatch between a1 and a3 at location "
         << (location.first - a1.begin())
         << "\nwhere a1 contains " << *location.first
         << " and a3 contains " << *location.second
         << "\n\n";

    char c1[SIZE] = "HELLO";
    char c2[SIZE] = "BYE BYE";

    // perform lexicographical comparison of c1 and c2
    result = lexicographical_compare(
        begin(c1), end(c1), begin(c2), end(c2));
    cout << (result ? "c1 is less than c2"
                    : "c1 is greater than or equal to ")
         << c2 << endl;
} // end main
```

```text
a1 contains: 1 2 3 4 5 6 7 8 9 10
a2 contains: 1 2 3 4 5 6 7 8 9 10
a3 contains: 1 2 3 4 1000 6 7 8 9 10

a1 is equal to a2.
a1 is not equal to a3.

There is a mismatch between a1 and a3 at location 4
where a1 contains 5 and a3 contains 1000

HELLO is greater than or equal to BYE BYE
```

图 16.2 | 算法 equal、mismatch 和 lexicographical_compare。

### equal 算法

第 25 行使用 equal 算法比较两个值序列是否相等。第二个序列必须至少包含与第一个序列一样多的元素——如果序列长度不同，equal 返回 false。== 运算符（无论是内建还是重载的）执行元素比较。在此示例中，将 a1 中从 a1.cbegin() 到（但不包含）a1.cend() 的元素与从 a2.cbegin() 开始的 a2 元素进行比较。在此示例中，a1 和 a2 相等。三个迭代器实参至少必须是输入迭代器（即，它们可以用于从正向方向读取序列）。第 30 行使用 equal 比较 a1 和 a3，它们不相等。

### 带二元谓词函数的 equal 算法

equal 的另一个版本将二元谓词函数作为第四个参数。该二元谓词函数接收被比较的两个元素，并返回一个 bool 值，指示这两个元素是否相等。这在存储对象或指向值的指针而不是实际值的序列中非常有用，因为你可以定义一个或多个比较。例如，你可以比较 Employee 对象的年龄、社会保险号或位置，而不是比较整个对象。你可以比较指针所引用的内容，而不是比较指针值（即指针中存储的地址）。

### mismatch 算法

第 34 行调用 **mismatch** 算法来比较两个值序列。该算法返回一对迭代器，指示每个序列中*不匹配*元素的位置。如果所有元素都匹配，则这对迭代器中的两个迭代器分别等于每个序列的结束迭代器。三个迭代器实参至少必须是*输入迭代器*。我们使用 C++11 的 `auto` 关键字*推断* pair 对象 location 的类型（第 34 行）。第 36 行使用表达式 `location.first - a.begin()` 确定数组中不匹配的实际位置，该表达式计算迭代器之间的元素个数（这类似于指针算术；参见第 8 章）。在此示例中，这对应于元素编号，因为比较是从每个数组的开头进行的。与 equal 一样，mismatch 也有另一个版本，它将*二元谓词函数*作为第四个参数。

### lexicographical_compare 算法

第 44～45 行使用 **lexicographical_compare** 算法比较两个 char 内建数组的内容。该算法的四个迭代器实参至少必须是*输入迭代器*。如你所知，指向内建数组的指针是*随机访问迭代器*。前两个迭代器实参指定第一个序列中的位置范围。最后两个指定第二个序列中的位置范围。我们再次使用 C++11 的 `begin` 和 `end` 函数来确定每个内建数组的元素范围。在遍历序列时，lexicographical_compare 会检查第一个序列中的元素是否小于第二个序列中的对应元素。如果是，该算法返回 true。如果第一个序列中的元素大于或等于第二个序列中的元素，该算法返回 false。该算法可用于*按字典序*排列序列。通常，这类序列包含字符串。

## 16.6.3 remove、remove_if、remove_copy 和 remove_copy_if

图 16.3 演示了使用算法 remove、remove_if、remove_copy 和 remove_copy_if 从序列中移除值。

```cpp
// Fig. 16.3: fig16_03.cpp
// Algorithms that remove, remove_if, remove_copy and remove_copy_if.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <array> // array class-template definition
#include <iterator> // ostream_iterator
using namespace std;

bool greater9(int); // prototype

int main()
{
    const size_t SIZE = 10;
    array<int, SIZE> init = { 10, 2, 10, 4, 16, 6, 14, 8, 12, 10 };
    ostream_iterator<int> output(cout, " ");

    array<int, SIZE> a1(init); // initialize with copy of init
    cout << "a1 before removing all 10s:\n ";
    copy(a1.cbegin(), a1.cend(), output);

    // remove all 10s from a1
    auto newLastElement = remove(a1.begin(), a1.end(), 10);
    cout << "\na1 after removing all 10s:\n ";
    copy(a1.begin(), newLastElement, output);

    array<int, SIZE> a2(init); // initialize with copy of init
    array<int, SIZE> c2 = { 0 }; // initialize to 0s
    cout << "\na2 before removing all 10s and copying:\n ";
    copy(a2.cbegin(), a2.cend(), output);

    // copy from a2 to c2, removing 10s in the process
    remove_copy(a2.cbegin(), a2.cend(), c2.begin(), 10);
    cout << "\nc2 after removing all 10s from a2:\n ";
    copy(c2.cbegin(), c2.cend(), output);

    array<int, SIZE> a3(init); // initialize with copy of init
    cout << "\na3 before removing all elements greater than 9:\n ";
    copy(a3.cbegin(), a3.cend(), output);

    // remove elements greater than 9 from a3
    newLastElement = remove_if(a3.begin(), a3.end(), greater9);
    cout << "\na3 after removing all elements greater than 9:\n ";
    copy(a3.begin(), newLastElement, output);

    array<int, SIZE> a4(init); // initialize with copy of init
    array<int, SIZE> c4 = { 0 }; // initialize to 0s
    cout << "\na4 before removing all elements"
         << "\n greater than 9 and copying:\n ";
    copy(a4.cbegin(), a4.cend(), output);

    // copy elements from a4 to c4, removing elements
    // greater than 9 in the process
    remove_copy_if(a4.cbegin(), a4.cend(), c4.begin(), greater9);
    cout << "\nc4 after removing all elements"
         << "\n greater than 9 from a4:\n ";
    copy(c4.cbegin(), c4.cend(), output);
    cout << endl;
} // end main

// determine whether argument is greater than 9
bool greater9(int x)
{
```

图 16.3 | 算法 remove、remove_if、remove_copy 和 remove_copy_if。

