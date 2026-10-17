
```cpp
20:     vector<int> vecResult;

21:

22:     // 为乘法结果分配空间

23:     vecResult.resize(10);

24:

25:     transform (vecMultiplicand.begin(), // 乘数范围
26:               vecMultiplicand.end(), // 乘数范围
27:               vecResult.begin(), // 存储结果的范围
28:               [int a, int b] { return a * b; }); // lambda

29:

30:     cout << "The contents of the first vector are: " << endl;
31:     for (size_t nIndex = 0; nIndex < vecMultiplicand.size(); ++nIndex)
32:         cout << vecMultiplicand[nIndex] << " ";
33:     cout << endl;

34:

35:     cout << "The contents of the second vector are: " << endl;
36:     for (size_t nIndex2 = 0; nIndex2 < vecMultiplier.size(); ++nIndex2)
37:         cout << vecMultiplier[nIndex2] << " ";
38:     cout << endl;

39:

40:     cout << "The result of the multiplication is: " << endl;
41:     for (size_t nIndex = 0; nIndex < vecResult.size(); ++nIndex)
42:         cout << vecResult[nIndex] << " ";
43:     cout << endl;

44:

45:     return 0;
46: }
```

### 二元谓词的 Lambda 表达式

返回 true 或 false 以帮助做决策的二函数被称为二元谓词。这些谓词被用于算法中，例如 `std::sort()` 会对容器中的任意两个值调用二元谓词，以决定哪一个应该放在另一个后面。二元谓词的通用语法是
`[...] (Type1&paramName, Type2&paramName) { // return bool expression; }`

列表22.5 演示了一个用于排序的 lambda 表达式。

# 列表 22.5 作为二元谓词在 std::sort() 中的 lambda 表达式以实现忽略大小写的排序

```cpp
0: #include <algorithm>
1: #include <string>
2: #include <vector>
```

# 列表 22.5 继续

```cpp
3: #include <iostream>
4: using namespace std;

6: template <typename T>
7: void DisplayContents(const T& Input)
8: {
9:     for(auto iElement = Input.begin() // auto, cbegin and cend: c++11
10:        iElement != Input.end();
11:             ++iElement)
12:        cout << *iElement << endl;
13: }

15: int main ()
16: {
17:     // 定义一个字符串 vector 来存储名称
18:     vector<string> vecNames;

19:     // 在 vector 中插入示例名称
20:     vecNames.push_back("Jim");
21:     vecNames.push_back("Jack");
22:     vecNames.push_back("Sam");
23:     vecNames.push_back("Anna");

26:     cout << "vector 中按插入顺序的名称: " << endl;
27:     DisplayContents(vecNames);

29:     cout << "默认 std::vector 排序后的名称: " << endl;
30:     sort(vecNames.begin(), vecNames.end());
31:     DisplayContents(vecNames);

33:     cout << "使用忽略大小写的谓词排序后的名称: " << endl;
34:     sort(vecNames.begin(), vecNames.end(),
35:         [](const string& str1, const string& str2) -> bool // lambda 
36:         {
37:             string str1LowerCase;
38:             // 分配空间
39:             str1LowerCase.resize(str1.size());

41:             // 将每个字符转换为小写
42:             transform(str1.begin(), str1.end(),
43:                 str1LowerCase.begin(), tolower);

45:             string str2LowerCase;
46:             str2LowerCase.resize(str2.size());
47:             transform(str2LowerCase.begin(), str2LowerCase.end(), str2LowerCase.begin(),
```

### 二元谓词的 Lambda 表达式

```cpp
48:     tolower);

49:

50:     return (str1LowerCase < str2LowerCase);
51:     } // lambda 结束
52:     ); // sort 结束
53:     DisplayContents(vecNames);

55:     return 0;
56: }
```

### 输出

vector 中按插入顺序的名称:
Jim
Jack
Sam
Anna
默认 std::vector 排序后的名称:
Anna
Jack
Sam
Jim
使用忽略大小写的谓词排序后的名称:
Anna
Jack
Jim
Sam

### 分析

这展示了一个跨越第 35-51 行的巨大 lambda 函数——`std::sort()` 的第三个参数从第 34 行开始，到第 52 行结束！该函数说明了 lambda 可以跨越多个语句，前提是如第 35 行所示显式指定了返回值（bool）。输出展示了按插入顺序的 vector 内容，其中 Jim 在 Jack 之前。如第 30 行所示，在使用提供的 lambda 或谓词进行默认排序后，vector 内容将 Jim 排在 Sam 之后，因为通过 `string::operator<` 它是区分大小写的。最后，在第 34-52 行中可以看到使用忽略大小写 lambda 表达式的版本，它如用户预期那样将 Jim 置于 Jack 之后。这种排序也使用了跨越多行的 lambda 表达式。

# 课程 22：C++11 Lambda 表达式

### 注意

列表 22.5 中这个异常巨大的 lambda 列表展示了...

## STL 算法分类

| 表格 23.1 续 |
| 算法 | 描述 |
| --- | --- |
| find | 在范围内搜索第一个与指定匹配的元素 |
| find_if | 在范围内搜索第一个满足指定条件的元素 |
| find_end | 在提供的范围内搜索特定子范围的最后一次出现 |
| find_first_of | 在目标范围内搜索一个范围内提供的任何元素的首次出现；或者，在重载版本中，搜索满足一个所提供的 find 准则的元素的首次出现 |
| adjacent_find | 在集合中搜索两个相等或满足指定条件的相邻元素 |

## 比较算法

`equal`: 比较两个元素是否相等，或使用指定的二元谓词来判断是否相同。

`mismatch`: 使用指定的二元谓词在两个元素范围内定位第一个差异值位置。

`lexicographical_compare`: 比较两个序列之间的元素，以确定哪一个较小。

## 变异算法

变异算法是指改变其所操作序列的内容或顺序的算法。STL 提供的某些常用的变异算法如表 23.2 所示。

| 表格 23.2 变异算法快速参考 |
| 算法 | 描述 |
| --- | --- |
| **初始化算法** | |
| fill | 将指定值赋值给指定范围内的每个元素。 |
| fill_n | 将指定值赋值给指定范围内前 n 个元素。 |
| generate | 将指定函数对象的返回值赋值给提供范围内的每个元素。 |
| generate_n | 将函数生成的值赋值给指定范围内指定数量的值。 |

| 表格 23.2 续 |
| 算法 | 描述 |
| --- | --- |
| **修改算法** | |
| for_each | 在范围内的每个元素上执行操作。当指定参数修改范围时，`for_each` 变成一个变异算法。 |
| transform | 在指定范围内的每个元素上应用指定的一元函数。 |
| **复制算法** | |
| copy | 将一个拷贝到另一个。 |
| copy_backward | 将一个拷贝到另一个，并按反序排列目标中的元素。 |
| **移除算法** | |
| remove | 从指定范围内移除指定值的元素。 |
| remove_if | 从指定范围内移除满足指定一元谓词的元素。 |
| remove_copy | 将所有元素从源拷贝到目标范围，指定值除外。 |
| remove_copy_if | 将所有元素从源拷贝到目标范围，满足指定一元谓词的元素除外。 |
| unique | 比较范围内的相邻元素并移除重复。重载版本使用二元谓词工作。 |
| unique_copy | 将指定源的所有相邻重复元素拷贝到指定范围。 |
| **替换算法** | |
| replace | 将范围内每个匹配指定值的元素替换为替换值。 |
| replace_if | 将指定范围内每个匹配指定值的元素替换为替换值。 |
| **排序算法** | |
| sort | 使用指定的排序准则对范围内的元素进行排序，该准则是提供严格弱排序的二元谓词。`sort` 可能会改变等元素的相对位置。 |
| stable_sort | 排序与 `sort` 类似，但也会保留顺序。 |
| partial_sort | 对范围内指定数量的元素进行排序。 |
| partial_sort_copy | 将元素从指定的源范围拷贝到目标范围，并在目标中以排序顺序存储 |

| 表格 23.2 续 |
| 算法 | 描述 |
| --- | --- |
| partition | 给定指定范围，将元素分为范围内的两组：满足一元谓词的在前，其余在后。可能不会维护集合中的相对顺序。 |
| stable_partition | 将输入范围划分为部分，类似于 `partition`，但保持了相对顺序。 |

## 分区算法

适用于有序容器的算法

- `binary_search`: 用于确定元素是否存在于排序集合中。
- `lower_bound`: 返回根据值或提供的二元谓词在排序集合中可能插入要素的第一个位置的迭代器。
- `upper_bound`: 返回根据值或提供的二元谓词在排序集合中可能插入要素的最后一个位置的迭代器。

## STL 算法的使用

表 23.1 和 23.2 中提到的 STL 算法的使用通过直接代码实践来学习效果最好。为此，请从代码示例中学习算法的细节，并开始将其应用于应用程序中。

### 给值或条件查找元素

给定如 `vector` 等容器，STL 算法 `find()` 和 `find_if()` 分别帮助你查找匹配值或满足条件的元素。`find()` 的用法模式如下：

```cpp
auto elementFound = find(vecIntegers.begin(), // 范围开始
                            vecIntegers.end(),    // 范围结束
                            numToFind);
```

```cpp
// 检查 find 是否成功
if (elementFound != vecIntegers.end())
    cout << "Result: Value found!" << endl;
```

`find_if()` 类似，并且要求你提供一个一元谓词。

# 给定值或条件计数元素

`std::count()` 和 `count_if()` 是用于在给定范围内计数元素的算法。`std::find()` 帮助你计算匹配某个值（通过等值运算符 `==` 进行测试）的元素个数；

```cpp
size_t nNumZeros = count(vecIntegers.begin(), vecIntegers.end());
cout << "Number of instances of '0': " << nNumZeros << endl;
```

`std::count_if()` 帮助你计算满足参数提供的一元谓元的元素个数（该参数可以是函数对象或 lambda 表达式）：

```cpp
// 一元谓元：
template <typename elementType>
bool IsEven(const elementType& number)
{
    return ((number % 2) == 0); // 如果是偶数则为 true
}
```

```cpp
// 使用一元谓元 IsEven 使用 count_if 算法：
size_t nNumEvenElements = count_if(vecIntegers.begin(),
vecIntegers.end(), IsEven<int>);
cout << "Number of even elements:" << nNumEvenElements << endl;
```

列表 23.2 中的代码演示了这些函数用法。

- **列表 23.2** 展示了如何使用 `std::count()` 确定特定值的数量，以及使用 `count_if()` 确定满足条件的元素数量

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>

4: // 用于 *_if 函数的一元谓元
5: template <typename elementType>
6: bool IsEven(const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }

11: int main (
12: {
13:     using namespace std;
14:     vector<int> vecIntegers;

16:     cout << "Populating a vector<int> with values from -9 to 9" << endl;
17:     for (int nNum = -9; nNum < 10; ++nNum)
18:     vecIntegers.push_back (nNum);

20:     // 使用 count 确定 vector 中 '0' 的个数
21:     size_t nNumZeroes = count (vecIntegers.begin(),vecIntegers.end(), '0');
22:     cout << "Number of instances of '0': " << nNumZeroes << endl;

24:     // 使用一元谓元 IsEven 使用 count_if:
25:     size_t nNumEvenElements = count_if (vecIntegers.begin(),
                                      vecIntegers.end (), IsEven<int> );

27:     cout << "Number of even elements: " << nNumEvenElements << endl;
28:     cout << "Number of odd elements:  ";
29:     cout << vecIntegers.size () - nNumEvenElements << endl;

31:     return 0;
32: }
```
