

```cpp
// Fig. 15.14: fig15_14.cpp
// Standard library deque class template.
#include <iostream>
#include <deque> // deque class-template definition
#include <algorithm> // copy algorithm
#include <iterator> // ostream_iterator
using namespace std;

int main() {
    deque<double> values; // create deque of doubles
    ostream_iterator<double> output(cout, " ");

    // insert elements in values
    values.push_front(2.2);
    values.push_front(3.5);
    values.push_back(1.1);

    cout << "values contains: ";

    // use subscript operator to obtain elements of values
    for (size_t i{0}; i < values.size(); ++i) {
        cout << values[i] << ' ';
    }

    values.pop_front(); // remove first element
    cout << "\nAfter pop_front, values contains: ";
    copy(values.cbegin(), values.cend(), output);

    // use subscript operator to modify element at location 1
    values[1] = 5.4;
    cout << "\nAfter values[1] = 5.4, values contains: ";
    copy(values.cbegin(), values.cend(), output);
    cout << endl;
}
```

```
values contains: 3.5 2.2 1.1
After pop_front, values contains: 2.2 1.1
After values[1] = 5.4, values contains: 2.2 5.4
```

**图 15.14 标准库 `deque` 类模板。**

第 10 行实例化了一个可以存储 `double` 值的 `deque`。第 14–16 行使用函数 `push_front` 和 `push_back` 在 `deque` 的开头和末尾插入元素。第 21–23 行的 `for` 语句使用下标运算符获取 `deque` 中每个元素的值用于输出。循环条件使用函数 `size` 确保我们不会尝试访问 `deque` 边界*之外*的元素。

第 25 行使用函数 `pop_front` 演示移除 `deque` 的第一个元素。第 30 行使用下标运算符获取一个*左值*，这使得可以将值直接赋给 `deque` 的任意元素。

## 15.6 关联容器

*关联容器*提供通过**键**（通常称为**搜索键**）*直接*存取元素的机制。四种*有序关联容器*是 `multiset`、`set`、`multimap` 和 `map`。它们都以*排序顺序*维护键。此外还有四种对应的*无序关联容器*——`unordered multiset`、`unordered set`、`unordered multimap` 和 `unordered map`——它们提供了与有序版本相同的大部分功能。有序关联容器与无序关联容器的主要区别在于，无序关联容器*不*以*排序*顺序维护键。本节我们重点讨论*有序关联容器*。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1941_0.png)

### 性能提示 15.10

*在不需要按排序顺序维护键的情况下，无序关联容器可能会提供更好的性能。*

遍历*有序关联容器*时，会按照该容器的排序顺序进行遍历。`multiset` 和 `set` 类提供对值集合进行操作的函数，其中值本身即键。`multiset` 与 `set` 的主要区别在于，`multiset` *允许重复键*，而 `set` *不允许*。

`multimap` 和 `map` 类提供对与键关联的值进行操作的函数（这些值有时称为**映射值**）。`multimap` 与 `map` 的主要区别在于，`multimap` 允许存储*重复键*及其关联值，而 `map` 只允许存储*唯一键*及其关联值。除了常见的容器成员函数外，*有序关联容器*还支持一些特定于关联容器的成员函数。接下来的几个小节将分别介绍每种*有序关联容器*及其常见成员函数的示例。

### 15.6.1 `multiset` 关联容器

`multiset` *有序关联容器*（来自头文件 `<set>`）提供快速的键存储和检索，并允许重复键。元素的排序由所谓的**比较函数对象**决定。例如，在一个整数 `multiset` 中，可以通过使用**比较函数对象** `less<int>` 对键进行排序，使得元素按*升序*排列。我们将在[第 16.5 节](#)详细讨论函数对象。在本章中，我们仅展示如何在声明有序关联容器时使用 `less<int>`。所有*有序关联容器*中的键数据类型必须支持基于比较函数对象的比较——使用 `less<T>` 排序的键必须支持与 `operator<` 比较。如果*有序关联容器*中使用的键是用户自定义数据类型，则这些类型必须提供适当的比较运算符。`multiset` 支持*双向迭代器*（但不支持*随机访问迭代器*）。如果键的顺序不重要，可以使用 `unordered_multiset`（头文件 `<unordered_set>`）。

[图 15.15](#) 演示了 `multiset` *有序关联容器*，其中 `multiset` 存储 `int` 类型，键按*升序*排序。`multiset` 和 `set` 容器（**第 15.6.2 节**）提供相同的基本功能。

```cpp
// Fig. 15.15: fig15_15.cpp
// Standard Library multiset class template
#include <array>
#include <iostream>
#include <set> // multiset class-template definition
#include <algorithm> // copy algorithm
#include <iterator> // ostream_iterator
using namespace std;

int main() {
   multiset<int, less<int>> intMultiset; // multiset of ints

   cout << "There are currently " << intMultiset.count(15)
        << " values of 15 in the multiset\n";

   intMultiset.insert(15); // insert 15 in intMultiset
   intMultiset.insert(15); // insert 15 in intMultiset
   cout << "After inserts, there are " << intMultiset.count(15)
        << " values of 15 in the multiset\n";

   // find 15 in intMultiset; find returns iterator
   auto result{intMultiset.find(15)};

   if (result != intMultiset.end()) { // if iterator not at end
       cout << "Found value 15\n"; // found search value 15
   }

   // find 20 in intMultiset; find returns iterator
   result = intMultiset.find(20);

   if (result == intMultiset.end()) { // will be true here
       cout << "Did not find value 20\n"; // did not find 20
   }

   // insert elements of array a into intMultiset
   array<int, 10> a{7, 22, 9, 1, 18, 30, 100, 22, 85, 13};
   intMultiset.insert(a.cbegin(), a.cend());
   cout << "\nAfter insert, intMultiset contains:\n";
   ostream_iterator<int> output(cout, " ");
   copy(intMultiset.begin(), intMultiset.end(), output);

   // determine lower and upper bound of 22 in intMultiset
   cout << "\n\nLower bound of 22: "
        << *intMultiset.lower_bound(22);
   cout << "\nUpper bound of 22: " << *intMultiset.upper_bound(22);

   // use equal_range to determine lower and upper bound
   // of 22 in intMultiset
   auto p{intMultiset.equal_range(22)};

   cout << "\n\nequal_range of 22:\n  Lower bound: "
        << *(p.first) << "\n  Upper bound: " << *(p.second);
   cout << endl;
}
```

```
There are currently 0 values of 15 in the multiset
After inserts, there are 2 values of 15 in the multiset

Found value 15
Did not find value 20

After insert, intMultiset contains:
1 7 9 13 15 15 18 22 22 30 85 100

Lower bound of 22: 22
Upper bound of 22: 30

equal_range of 22:
  Lower bound: 22
  Upper bound: 30
```

**图 15.15 标准库 `multiset` 类模板。**

### 创建 `multiset`

第 11 行创建了一个 `int` 类型的 `multiset`，使用函数对象 `less<int>` 按*升序*排列。*升序*是 `multiset` 的默认顺序，因此可以省略 `less<int>`，第 11 行可以写成：

```cpp
multiset<int> intMultiset; // multiset of ints
```

C++11 修复了 `less<int>` 的右尖括号与 `multiset` 类型右尖括号之间空格导致的语法问题。在 C++11 之前，如果像第 11 行那样指定该 `multiset` 的类型，编译器会将 `multiset<int, less<int>>` 中的 `>>` 视为 `>>` 运算符并产生编译错误。因此，你必须在 `less<int>` 的右尖括号与 `multiset` 类型的右尖括号（或任何其他类似的模板类型，如 `vector<vector<int>>`）之间放入一个空格。从 C++11 开始，上述声明可以正确编译。

