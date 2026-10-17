
```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <list>
3: #include <iostream>
4: using namespace std;
5:
6: template <typename T>
7: void DisplayContents(const T& container)
8: {
9:   for (auto element = container.begin();
10:  element != container.end();
11:   ++ element)
12:  cout << *element << ' ' << ' ';
13:
14:  cout << endl;
15: }
16:
17: int main()
18: {
19:  vector<int> numsInVec(2017, 0, -42, 10101, 25, 9, 9, 9);
20:  list<int> numsInList({-1, 42, 10101});
21:
22:  cout << "The contents of the sample vector: " << endl;
23:  DisplayContents(numsInVec);
24:
25:  cout << "The contents of the sample list are: " << endl;
26:  DisplayContents(numsInList);
27:
28:  cout << "search() for the contents of list in vector: " << endl;
29:  auto range = search(numsInVec.begin(), // 搜索的起始范围
30:  numsInVec.end(), // 要查找的结束范围
31:  numsInList.begin(), // 要查找的起始范围
32:  numsInList.end()); // 要查找的结束范围
33:
34:  // 检查 search 是否找到了匹配项
35: if (range != numsInVec.end())
36: {
37:  cout << "Sequence list found in vector at position: ";
38:  cout << distance(numsInVec.cbegin(), range) << endl;
39: }
40: cout << "Searching {9, 9, 9} in vector using search_n(): " << endl;
41: auto partialRange = search_n(numsInVec.cbegin(), // 起始范围
42:                            numsInVec.end(), // 结束范围
43:                            3, // 要查找的项数
44:                            9); // 要查找的项
45: if (partialRange != numsInVec.end())
46:  cout << "Sequence {9, 9, 9} found in vector at position: ";
47:  cout << distance(numsInVec.cbegin(), partialRange) << endl;
48: }
49: return 0;
```

## 输出

示例 `vector` 的内容：

2017 0 -42 10101 25 9 9 9

示例 `list` 的内容：

-1 42 10101

在 `vector` 中搜索 `list` 的内容：

在 `vector` 中找到序列列表，位置为：2

在 `vector` 中使用 `search_n()` 搜索 `{9, 9, 9}`:

在 `vector` 中找到序列 `{9, 9, 9}`,位置为：6

## 分析

示例从两个容器开始，一个 `vector` 和一个 `list`，最初填充了整数值。如第 29 行所示，使用 `search()` 来查找 `vector` 中是否存在该 `list`。由于我们想在由两个类的 `cbegin()` 和 `end()` 方法返回的范围内进行搜索，因此它实际上演示了迭代器如何将算法与容器连接。容器的物理特性对搜索算法没有意义，因为它们只与迭代器一起工作。第 42 行使用 `search_n()` 来查找 `vector` 中 `{9, 9, 9}` 的首次出现。

# 将容器中的元素初始化为特定值

`fill()` 和 `fill_n()` 是帮助设置给定内容的 STL 算法。`fill()` 用于填充给定范围的内容：

```cpp
vector<int> numsInVec(3);
```

正如其名，`fill_n()` 需要起始位置、数量和值：

```cpp
fill_n(numsInVec.begin(), 3, 9);
```

列表 23.4 演示了这些算法如何初始化一个 `vector`。

# 列表 23.4 使用 `fill()` 和 `fill_n()` 将容器元素为特定值

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <list>
3: #include <iostream>
4: using namespace std;
5:
6: template <typename T>
7: void DisplayContents(const T& container)
8: {
9:   for (auto element = container.begin();
10:  element != container.end();
11:   ++ element)
12:  cout << *element << ' ' << ' ';
13:
14:  cout << endl;
15: }
16:
17: int main()
18: {
19:  vector<int> numsInVec(2017, 0, -42, 10101, 25, 9, 9, 9);
20:  list<int> numsInList({-1, 42, 10101});
21:
22:  cout << "The contents of the sample vector: " << endl;
23:  DisplayContents(numsInVec);
24:
25:  cout << "The contents of the sample list are: " << endl;
26:  DisplayContents(numsInList);
27:
28:  cout << "search() for the contents of list in vector: " << endl;
29:  auto range = search(numsInVec.begin(), // 搜索的起始范围
30:  numsInVec.end(), // 要查找的结束范围
31:  numsInList.begin(), // 要查找的起始范围
32:  numsInList.end()); // 要查找的结束范围
33:
34:  // 检查 search 是否找到了匹配项
35: if (range != numsInVec.end())
36: {
37:  cout << "Sequence list found in vector at position: ";
38:  cout << distance(numsInVec.cbegin(), range) << endl;
39: }
40: cout << "Searching {9, 9, 9} in vector using search_n(): " << endl;
41: auto partialRange = search_n(numsInVec.cbegin(), // 起始范围
42:                            numsInVec.end(), // 结束范围
43:                            3, // 要查找的项数
44:                            9); // 要查找的项
45: if (partialRange != numsInVec.end())
46:  cout << "Sequence {9, 9, 9} found in vector at position: ";
47:  cout << distance(numsInVec.cbegin(), partialRange) << endl;
48: }
49: return 0;
```

## 输出

示例 `vector` 的内容：

2017 0 -42 10101 25 9 9 9

示例 `list` 的内容：

-1 42 10101

在 `vector` 中搜索 `list` 的内容：

在 `vector` 中找到序列列表，位置为：2

在 `vector` 中使用 `search_n()` 搜索 `{9, 9, 9}`:

在 `vector` 中找到序列 `{9, 9, 9}`,位置为：6

## 分析

示例从两个容器开始，一个 `vector` 和一个 `list`，最初填充了整数值。如第 29 行所示，使用 `search()` 来查找 `vector` 中是否存在该 `list`。由于我们想在由两个类的 `cbegin()` 和 `end()` 方法返回的范围内进行搜索，因此它实际上演示了迭代器如何将算法与容器连接。容器的物理特性对搜索算法没有意义，因为它们只与迭代器一起工作。第 42 行使用 `search_n()` 来查找 `vector` 中 `{9, 9, 9}` 的首次出现。

# 使用运行时生成的值初始化元素

正如 `fill()` 和 `fill_n()` 函数使用特定值填充集合，STL 算法 `generate()` 和 `generate_n()` 则使用一元函数的返回值初始化集合。

你可以使用 `generate()` 使用一元函数的返回值填充范围：

```cpp
generate(numsInVec.begin(), numsInVec.end());
```

`generate_n()` 与 `generate()` 类似，只是你提供了要赋值的元素数量而不是范围的结束边界：

```cpp
generate_n(numsInList.begin(), 5);
```

因此，你可以使用这两个算法将集合的内容初始化为文件的内容，例如或随机值，如列表 23.5 所示。

# 列表 23.5 使用 `generate()` 和 `generate_n()` 初始化随机值集合

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <list>
3: #include <iostream>
4: #include <ctime>
5:
6: int main ()
7: {
8:   using namespace std; // 使用时间种子随机生成器
9:   srand(NULL);
10:
11:  vector <int> numsInVec(5);
12:  generate(numsInVec.begin(), numsInVec.end(), // 范围
13:  rand()); // 生成函数
14:
15:  cout << "Elements in the vector are: ";
16:  for (size_t index = 0; index < numsInVec.size(); ++ index)
17:  cout << numsInVec[index] << " ";
18:  cout << endl;
19:
20:  list <int> numsInList(5);
21:  generate_n(numsInList.begin(), 3, rand);
22:
23:  cout << "Elements in the list are: ";
24:  for (auto element = numsInList.begin();
```

# STL 算法的使用

```cpp
25:   element != numsInList.end();
26:   ++ element
27:   cout << element << ' ';
28:
29:   return 0;
30: }
```

# 输出

`vector` 中的元素为: 41 18467 6334 26500 19169

`list` 中的元素为: 15724 11478 29358 0 0

![](img/ccb6520e9d7dbb1b25f5e4ac7152a7c5_602_0.png)

# 分析

使用当前时间作为种子的随机数生成器的用法与第 9 行所示的方法不同，这意味着每次运行应用程序时的输出都是不同的。列表 23.5 使用第 12 行的 `generate()` 函数填充 `vector` 中的所有元素，并使用第 21 行的 `generate_n()` 使用生成器 `rand()` 提供的随机值填充 `list` 的前三个元素。注意，`generate()` 函数接受一个范围作为输入，并对范围内的每个元素调用指定的函数对象 `rand()`。相比之下，`generate_n()` 仅接受起始位置。然后根据 `count` 参数指定的次数调用指定的函数对象 `rand()`，以覆盖多个元素的内容。超出指定偏移量的容器中的元素将保持不变。

# 使用 `for_each()` 处理范围内的元素

`for_each()` 算法对所提供范围内的每个元素应用一元函数对象。`for_each()` 的用法如下：
