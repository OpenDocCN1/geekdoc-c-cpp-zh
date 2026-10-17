
# STL 算法的使用

### 输出

向 `vector<int>` 填充从 -9 到 9 的值
`'0'` 的个数: 1

偶数元素个数: 9
奇数元素个数: 10

### 分析

第 21 行使用 `count()` 来确定 `vector<int>` 中 0 的出现次数。
同样，第 25 行使用 `count_if()` 确定 `vector` 中偶数元素的个数。注意第三个参数，它是在第 6-9 行定义的的一元谓元 `IsEven()`。`vector` 中奇数元素的个数是通过从总元素数减去 `count_if()` 的返回值计算出的。
列表 23.2 在 `count_if()` 中使用了谓元函数 `IsEven()`，而列表 23.1 在 `find_if()` 中使用了 lambda 版本虽然减少了代码量，但应该记住，如果合并这两个示例，`IsEven()` 可以同时用于 `find_if()` 和 `count_if()`，从而增加重用性。

注意

在集合中搜索元素或范围

列表 23.1 演示了如何在容器中查找元素。有时，你需要查找一个值范围。在这种情况下，如果一个范围包含了另一个范围，可以使用 `search()` 或 `search_n()`：

```cpp
auto iRange = search (vecIntegers.begin(), // 范围起始
                      vecIntegers.end(), // 范围结束
                      listIntegers.begin(), // 要搜索范围的起始
                      listIntegers.end() ); // 要搜索范围的结束
```

容器中连续发现了 n 个值，可以使用 `search_n()`：

```cpp
auto iPartialRange = search_n (vecIntegers.begin(), // 范围起始
                                vecIntegers.end(), // 范围结束
                               3, // 要查找的项目个数
                               9); // 要搜索的项目
```

这两个函数都返回指向模式第一个实例的迭代器，在使用之前需要检查是否为 `end()`。列表 23.3 演示了 `search()` 和 `search_n()` 的用法。

列表 23.3 使用 `search()` 和 `search_n()` 在集合中搜索范围

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <list>
3: #include <iostream>
4: using namespace std;
5:
6: template <typename T>
7: void DisplayContents(const T &vec)
8: {
9:     for(auto element = vec.begin(); // auto begin 和 end:
10:          element != vec.end();
11:             ++element)
12:            cout << *element << ' ';
13:        cout << endl;
14: }
15:
16: int ()
17: {
18:     // 示例容器 包含 -9 到 9 的整数 vector
19:     vector<int> vecIntegers;
20:     for (int nNum = -9; nNum < 10; ++nNum)
21:     vecIntegers.push_back (nNum);
22:
23:     // 向 vector 插入更多值
24:     vecIntegers.push_back (9);
25:     vecIntegers.push_back (9);
26:
27:     // 另一个示例容器 - 从 -4 到 4 的整数 list
28:     list<int> listIntegers;
29:     for (int nNum = -4; nNum < 5; ++nNum)
30:     listIntegers.push_back (nNum);
31:
32:     cout << "The contents of the sample vector: " << endl;
33:     DisplayContents(vecIntegers);
34:
35:     cout << "The contents of the sample list: " << endl;
36:     DisplayContents(listIntegers);
37:
38:     cout << "search() for the contents of list in vector:" << endl;
39:     auto iRange = search (vecIntegers.begin(), // 范围起始
40:                           vecIntegers.end(), // 搜索范围结束
41:                           listIntegers.begin(), // 要搜索范围的起始
42:                           listIntegers.end() ); // 要搜索范围的结束
43:
44:     // 检查 search 是否找到匹配
45:     if (iRange != vecIntegers.end())
46:     {
47:         cout << "Sequence in list found in vector at position: "
48:         cout << distance (vecIntegers.begin(), iRange) << endl;
49:     }
50:
51:     cout << "Searching (9, 9, 9) in vector using search_n():";
52:     auto iPartialRange = search_n (vecIntegers.begin(), // 范围起始
53:                               vecIntegers.end(), // 范围结束
54:                               3, // 要查找的项目个数
55:                               9); // 要搜索的项目
56:
57:     if (iPartialRange != vecIntegers.end())
58:     {
59:         cout << "Sequence (9, 9, 9) found in vector at position: ";
60:         cout << distance (vecIntegers.begin(), iPartialRange) << endl;
61:     }
62:
63:     return 0;
64: }
```

### 输出

示例 `vector` 的内容：
- 9 -8 -7 -6 -5 -4 -3 -2 -1 0 1 2 3 4 5 6 7 8 9 9
示例 `list` 的内容为：
- 4 -3 -2 -1 0 1 2 3 4
在 `vector` 中搜索 `list` 的内容：
在 `vector` 中找到 `list` 序列的位置： 5
使用 `search_n()` 在 `vector` 中搜索 (9, 9, 9):

## 列表 23.4 使用 `fill()` 和 `fill_n()` 设置容器的初始值

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: int main ()
5: {
6:   using namespace std;
7:
8:   // 初始化一个包含 3 个元素的示例 vector
9:   vector<int> vecIntegers(3);
10:
11:  // 将容器中的所有元素填充为 9
12:  fill(vecIntegers.begin(), vecIntegers.end(), 9);
13:
14:  // 增加 vector 的大小以容纳 6 个元素
15:  vecIntegers.resize(6);
16:
17:  // 从偏移 3 开始将三个元素填充为 -9
18:  fill_n(vecIntegers.begin() + 3, 3, -9);
19:
20:  cout << "Contents of the vector are: " << endl;
21:  for (size_t nIndex = 0; nIndex < vecIntegers.size(); ++nIndex)
22:  {
23:    cout << "[" << nIndex << "] = ";
24:    cout << vecIntegers[nIndex] << endl;
25:  }
26:
27:  return 0;
28: }
```

### 输出

Contents of the vector are:
Element [0] = 9
Element [1] = 9
Element [2] = 9
Element [3] = -9
Element [4] = -9
Element [5] = -9

### 分析

23.4 使用 `fill()` 和 `fill_n()` 函数将容器的内容初始化为一组组值，如第 12 行和第 18 行所示。注意在向范围内填充值之前使用了 `resize()` 函数，这在本质上创建了元素，随后这些被填充了值。`fill()` 算法作用于部分范围，而 `fill_n()` 则有潜力作用于部分范围。

## 使用 `std::generate()` 将元素初始化为运行时生成的值

正如 `fill()` 和 `fill_n()` 函数向集合填充特定值一样，STL 算法（如 `generate()` 和 `generate_n()`）被用于使用一元函数的返回值来初始化集合。

你可以使用 `generate()` 使用生成器函数的返回值来填充范围：

```cpp
generate (vecIntegers.begin(), vecIntegers.end() //范围
               rand); // 要调用的生成器函数
```

`generate_n()` 与 `generate()` 类似，但你需要提供要赋值的元素数量作为范围的结束边界：

```cpp
generate_n (listIntegers.begin(), 5, rand);
```

因此，你可以使用两种算法将容器的内容初始化为文件内容（例如），或者简单地初始化为随机值，如列表 23.5 所示。

## 列表 23.5 使用 `generate()` 和 `generate_n()` 将集合初始化为随机值

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <list>
3: #include <iostream>
4:
5: int main ()
6: {
7:   using namespace std;
8:
9:   vector <int> vecIntegers(10);
10:  generate (vecIntegers.begin(), vecIntegers.end()
11:            rand); // 要调用的生成器函数
12:
13:  cout << "Elements in the vector of size " << vecIntegers.size();
14:  cout << " assigned by 'generate': " << endl << "{";
15:  for (size_t ncount=0; ncount<vecIntegers.size(); ++ ncount)
16:    cout << vecIntegers[ncount] << " ";
17:
18:
19:  cout << "}" << endl;
20:
21:  list<int> listIntegers(10);
22:  generate_n(listIntegers.begin(), 5, rand);
23:
24:  cout << "Elements in the list of size: " << listIntegers.size();
25:  cout << " assigned by 'generate_n': " << endl << "{";
26:  list<int>::const_iterator iElementLocator;
27:  for ( iElementLocator = listIntegers.begin();
28:      iElementLocator != listIntegers.end();
29:      ++ iElementLocator )
30:    cout << *iElementLocator << ' ';
31:
32:  cout << '}' << endl;
33:
34:  return 0;
35: }
```

大小为 10 的 `vector` 中由 'generate' 分配的元素为：
{ ...

大小为 10 的 `list` 中由 'generate_n' 分配的元素为：
{ ...

### 分析

23.5 使用 `generate` 函数将容器的内容填充为随机值。`generate` 函数接受一个范围作为输入，并随之调用范围内的每个元素。`generate_n` 接受起始位置和次数，以填充范围内的元素。

## 使用 `for_each()` 处理范围内的元素

`for_each()` 算法将指定的函数对象应用于范围内的每个元素。`for_each()` 的用法是：

```cpp
unaryFunction = for_each(start_of_range, end_of_range, unaryObject );
```

该函数对象也可以是一个 lambda 表达式。`for_each()` 返回该函数对象，这种指定意味着使用结构体或类作为函数对象有助于在 `for_each()` 完成后查询信息。这在列表 23.6 中得到了演示。

## 列表 23.6 使用 `for_each()` 显示序列的内容

```cpp
0: #include <algorithm>
1: #include <iostream>
2: #include <vector>
3: #include <string>
4: using namespace std;
5:
6: // for_each 调用的一元函数对象
7: template <typename elementType>
8: struct DisplayElementCount
9: {
10:    int Count;
11:
12:    // 构造函数
13:    DisplayElementCount() : Count(0) {}
14:
15:    void operator () (const elementType& element)
16:    {
17:        ++Count;
18:        cout << element << ' ';
19:    }
20: };
21:
22: int main (
23: {
24:    vector <int> vecIntegers;
25:    for (int nCount = 0; nCount < 10; ++ nCount)
26:        vecIntegers.push_back(nCount);
27:
28:    cout << 'Displaying the vector of integers: ' << endl;
29:
30:    // 显示整数数组
31:    DisplayElementCount<int> Functor =
32:    for_each (vecIntegers.begin() // 范围起始
33:        vecIntegers.end() // 范围结束
34:        DisplayElementCount<int>()()); // Functor
35:
36:    cout << endl;
37:
38:    // 使用 for_each 返回值中存储的状态
39:    cout << "" << Functor.Count << " elements were displayed " << endl;
40:   string Sample("for_each and strings!");
41:   cout << "String: " << Sample << ", length: " << Sample.length() << endl;
42:
43:   cout << "String displayed using lambda:" << endl;
44:   int NumChars = 0;
45:
46:   for_each( Sample.begin(),
```
