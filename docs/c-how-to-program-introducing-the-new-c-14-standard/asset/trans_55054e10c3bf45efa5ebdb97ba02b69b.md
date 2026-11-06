
## 16.4.6 基本搜索和排序算法

**图 16.7** 演示了一些基本的搜索和排序标准库算法，包括 `find`、`find_if`、`sort`、`binary_search`、`all_of`、`any_of`、`none_of` 和 `find_if_not`。

```cpp
1    // Fig. 16.7: fig16_07.cpp
2    // Standard Library search and sort algorithms.
3    #include <iostream>
4    #include <algorithm> // algorithm definitions
5    #include <array> // array class-template definition
6    #include <iterator>
7    using namespace std;
8    int main() {
9       const size_t SIZE{10};
10      array<int, SIZE> a{10, 2, 17, 5, 16, 8, 13, 11, 20, 7};
11      ostream_iterator<int> output(cout, " ");
12
13      cout << "array a contains: ";
14
15      copy(a.cbegin(), a.cend(), output); // display output vector
16
17      // locate first occurrence of 16 in a
18      auto location = find(a.cbegin(), a.cend(), 16);
19
20      if (location != a.cend()) { // found 16
21         cout << "\n\n16 found at location " << (location - a.cbegin());
22      }
23      else { // 16 not found
24         cout << "\n\n16 not found";
25      }
26
27      // locate first occurrence of 100 in a
28      location = find(a.cbegin(), a.cend(), 100);
29
30      if (location != a.cend()) { // found 100
31          cout << "\nFound 100 at location " << (location - a.cbegin());
32      }
33      else { // 100 not found
34          cout << "\n100 not found";
35      }
36
37      // create variable to store lambda for reuse
38      auto isGreaterThan10{[](auto x){return x > 10;}};
39
40      // locate first occurrence of value greater than 10 in a
41      location = find_if(a.cbegin(), a.cend(), isGreaterThan10);
42
43      if (location != a.cend()) { // found value greater than 10
44          cout << "\n\nThe first value greater than 10 is " << *location
45               << "\nfound at location " << (location - a.cbegin());
46      }
47      else { // value greater than 10 not found
48          cout << "\n\nNo values greater than 10 were found";
49      }
50
51      // sort elements of a
52      sort(a.begin(), a.end());
53      cout << "\nArray after sort: ";
54      copy(a.cbegin(), a.cend(), output);
55
56      // use binary_search to check whether 13 exists in a
57      if (binary_search(a.cbegin(), a.cend(), 13)) {
58          cout << "\n\n13 was found in a";
59      }
60      else {
61          cout << "\n\n13 was not found in a";
62      }
63
64      // use binary_search to check whether 100 exists in a
65      if (binary_search(a.cbegin(), a.cend(), 100)) {
66          cout << "\n100 was found in a";
67      }
68      else {
69          cout << "\n100 was not found in a";
70      }
71
72      // determine whether all of the elements of a are greater than 10
73      if (all_of(a.cbegin(), a.cend(), isGreaterThan10)) {
74          cout << "\n\nAll the elements in a are greater than 10";
75      }
76      else {
77          cout << "\n\nSome elements in a are not greater than 10";
78      }
79
80      // determine whether any of the elements of a are greater than 10
81      if (any_of(a.cbegin(), a.cend(), isGreaterThan10)) {
82          cout << "\n\nSome of the elements in a are greater than 10";
83      }
84      else {
85          cout << "\n\nNone of the elements in a are greater than 10";
86      }
87
88      // determine whether none of the elements of a are greater than 10
89      if (none_of(a.cbegin(), a.cend(), isGreaterThan10)) {
90          cout << "\n\nNone of the elements in a are greater than 10";
91      }
92      else {
93          cout << "\n\nSome of the elements in a are greater than 10";
94      }
95
96      // locate first occurrence of value that's not greater than 10 in a
97      location = find_if_not(a.cbegin(), a.cend(), isGreaterThan10);
98
99      if (location != a.cend()) { // found a value less than or equal to 10
100         cout << "\nThe first value not greater than 10 is " << *location
101              << "\nfound at location " << (location - a.cbegin());
102     }
103     else { // no values less than or equal to 10 were found
104         cout << "\nOnly values greater than 10 were found";
105     }
106
107     cout << endl;
108 }
```

```text
array a contains: 10 2 17 5 16 8 13 11 20 7

16 found at location 4
100 not found

The first value greater than 10 is 17
found at location 2

Array after sort: 2 5 7 8 10 11 13 16 17 20

13 was found in a
100 was not found in a

Some elements in a are not greater than 10

Some of the elements in a are greater than 10

Some of the elements in a are greater than 10

The first value not greater than 10 is 2
found at location 0
```

图 16.7 标准库搜索和排序算法。

### `find` 算法

第 18 行使用 `find` 算法在从 `a.cbegin()` 到（但不包括）`a.cend()` 的范围内定位值 `16`。该算法要求其两个迭代器实参至少为*输入迭代器*，并返回一个*输入迭代器*，该迭代器要么定位到包含该值的第一个元素，要么指示序列末尾（如第 28 行的情况）。

### *将 Lambda 存储在变量中*

在本例中，我们多次测试 `array a` 中的元素是否大于 10。可以将 lambda 存储在变量中，如第 38 行所示：

```cpp
auto isGreaterThan10 = [](auto x){return x > 10;};
```

随后可以在以后使用该变量将 lambda 传递给其他函数，如第 41、73、81、89 和 97 行所示。还可以像函数名一样使用该变量来调用 lambda，如 `isGreaterThan10(9)`，它返回 `false`。

### `find_if` 算法

第 41 行使用 `find_if` 算法（线性搜索）在从 `a.cbegin()` 到（但*不*包括）`a.cend()` 的范围内定位第一个使*一元谓词函数*返回 `true` 的值——在本例中，该一元谓词函数是存储在变量 `isGreaterThan10` 中的 lambda `[](auto x){return x > 10;}`。编译器将参数 `x` 的类型推断为 `int`（因为该 `array` 存储 `int`），并将返回类型推断为 `bool`，因为该 lambda 返回条件值。算法 `find_if` 要求其两个迭代器实参至少为*输入迭代器*。该算法返回一个*输入迭代器*，它要么定位到包含使谓词函数返回 `true` 的值的第一个元素，要么指示序列末尾。

### `sort` 算法

第 52 行使用 `sort` 算法将范围从 `a.begin()` 到（但*不*包括）`a.end()` 中的元素按*升序*排列。该算法要求其两个迭代器实参为*随机访问迭代器*——因此该算法可用于内置数组以及标准库容器 `array`、`vector` 和 `deque`。该算法的一个重载版本具有第三个实参，它是一个*二元谓词函数*，接受两个实参并返回一个 `bool`，用于指示*排序顺序*。该谓词比较待排序序列中的两个值。如果返回值为 `true`，则这两个元素已处于*有序*顺序；否则，需要在序列中重新排列这两个元素。

### `binary_search` 算法

第 57 行使用 `binary_search` 算法确定值 13 是否在从 `a.cbegin()` 到（但*不*包括）`a.cend()` 的范围内。这些值必须按*升序*排序。算法 `binary_search` 要求其两个迭代器实参至少为*前向迭代器*。该算法返回一个 `bool`，指示该值是否在序列中找到。第 65 行演示了一次对 `binary_search` 的调用，其中该值*未*找到。该算法的一个重载版本接收一个*二元谓词函数*作为第四个实参，该函数有两个实参，它们是序列中的值，并返回一个 `bool`。如果被比较的两个元素处于*有序顺序*，则该谓词函数返回 `true`。如果需要知道搜索键在容器中的*位置*，请使用 `lower_bound` 或 `find` 算法，而不是 `binary_search`。

### `C++11: all_of` 算法

第 73 行使用 `all_of` 算法确定*一元谓词函数*（存储在 `isGreaterThan10` 中的 lambda）是否对从 `a.cbegin()` 到（但*不*包括）`a.cend()` 的范围内的所有元素都返回 `true`。算法 `all_of` 要求其两个迭代器实参至少为*输入迭代器*。

