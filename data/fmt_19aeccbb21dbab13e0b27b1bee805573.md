
第 13–15 行包含类 `Multiply`，如前面的代码段所示。在这个示例中，你使用算法 `std::transform()` 将两个范围的内容相乘并存储在第三个范围内。在这种情况下，涉及的范围存储在 `std::vector` 中，分别为 `multiplicands`、`multipliers` 和 `vecResult`。你在第 27–31 行中使用 `std::transform()` 将 `multiplicands` 中的每个元素与 `multipliers` 中对应的元素相乘，并将乘法结果存储在 `vecResult` 中。乘法本身是由二元函数 `Multiply::operator()` 完成的，该函数会在源范围和目标范围的每个元素上调用一次。`operator()` 的返回值存储在 `vecResult` 中。

此示例演示了二元函数在对 STL 容器元素执行算术运算的应用。下一个示例也使用 `std::transform()` 通过函数 `tolower()` 将字符串转换为小写。

## 二元谓词

接受两个参数并返回 `bool` 的函数是二元谓词。此类函数应用在 STL 函数中，例如 `std::sort()`。列表 21.6 展示了将两个字符串转换为小写后进行比较的二元谓词。这种谓词可以用于对字符串向量进行不区分大小写的排序。

### 列表 21.6 用于区分大小写排序的二元谓词

```cpp
0: #include <algorithm>
1: #include <string>
2: using namespace std;
3:
4: class StringNoCase
5: {
6: public:
7:   bool operator (const string& str1, const string& str2)
8:   {
9:     string str1;
```

![](img/cc6520e9d7dbb125f4a)

## 课程 21: 理解函数对象

```cpp
10:     // 分配空间
11:     str1LowerCase.resize(str1.size());
12:
13:     // 将每个字符转换为小写
14:     transform(str1.begin(), str1.end(), str1LowerCase.begin(),
15:                               ::tolower);
16:
17:     string str2LowerCase;
18:     str2LowerCase.resize(str2.size());
19:     transform(str2.begin(), str2.end(), str2LowerCase.begin(),
20:                               ::tolower);
21:
22:     return (str1LowerCase < str2LowerCase);
23: }
```

## 分析

二元谓词 `StringNoCase` 通过将两个字符串转换为小写来比较它们。这允许了进行不区分大小写的比较。

### 列表 21.7 使用函数对象执行区分大小写排序

```cpp
0: #include <algorithm>
1: #include <string>
2: #include <vector>
3: #include <iostream>
4: using namespace std;
5:
6: template <typename T>
7: void DisplayContents(const vector<T>& container)
8: {
9:     for (size_t index = 0; index < container.size(); ++index)
10:        cout << container[index] << " ";
11:    cout << endl;
12: }
13:
14: int main ()
15: {
16:     vector<string> names{"apple", "Banana", "cherry", "date"};
17:
18:     cout << "插入顺序的是: " << endl;
19:     DisplayContents(names);
20:
21:     sort(names.begin(), names.end());
22:     cout << "使用 less< 排序后的名称: " << endl;
23:     DisplayContents(names);
24:
25:     sort(names.begin(), names.end(), StringNoCase());
26:     cout << "使用忽略大小写谓词的排序结果: " << endl;
27:     DisplayContents(names);
28:
29:     return 0;
30: }
```

## 分析

列表 21.7 展示了如何将二元谓词 `StringNoCase` 与 `std::sort` 算法结合。第一次调用 `sort` 使用默认的 `less<>()` 运算符，它是区分大小写的。第二次调用 `sort` 使用 `StringNoCase` 对象来执行不区分大小写的排序。

## 测验

- 1. 返回 bool 结果的一元函数的术语是什么？
- 2. 一个既不修改数据也不返回 bool 的函数对象有什么用？你能用例子来解释一下吗？
- 3. 函数对象（function objects）这一术语的定义是什么？

## 练习

- 1. 编写一个一元函数，可以配合 `std::for_each()` 用于显示输入参数的倍数。
- 2. 扩展此谓词，以记录它被使用的次数。
- 3. 写一个有助于按升序排序的二元谓词。

# 第 22 节

## Lambda 表达式

Lambda 表达式是定义和构造无名函数对象的一种紧凑方式。这些表达式是在 C++11 中引入的。在本节中，你将了解到：

- 如何编写 lambda 表达式
- 如何将 lambda 表达式作为谓词使用
- 什么是 C++14 通用 lambda 表达式
- 如何编写可以持有并操作状态的 lambda 表达式

### 什么是 Lambda 表达式？

Lambda 表达式可以可视化为无名结构体（或类）的紧凑版本，并带有公共的 `operator()`……从这个意义上说，lambda 表达式类似于第 21 节“理解函数对象”中的函数对象。在开始分析 lambda 函数的编程之前，以列表 21.1（来自第 21 节）中的函数对象为例：

```cpp
// 行为类似于一元函数的结构体
template <typename elementType>
struct DisplayElement
{
    void operator () (const elementType& element) const
    {
        cout << element << ' ';
    }
}
```

该函数对象使用 `cout` 在屏幕上显示元素对象，通常在算法中作为 `std::for_each()` 使用：

```cpp
// 打印 vector 中包含的每个整数
for_each (numsInVec.begin(), // 范围开始
    numsInVec.end(), // 范围结束
    DisplayElement<int> (})); // 一元函数对象
```

Lambda 表达式将包括函数对象定义在内的整个代码压缩成了三行：

```cpp
// 使用 lambda 表达式打印 vector 中包含的每个整数
for_each (numsInVec.begin(), // 范围开始
    numsInVec.end(), // 范围结束
    [] (const int& element) { cout << element << ' ' }; });
```

当编译器看到 lambda 表达式时，在此情况下：

```cpp
[] (const int& element) { cout << element << ' ' }
```

它会自动将此表达式扩展为类似于 `struct DisplayElement<int>` 的表示：

```cpp
struct NoName
{
    void operator () (const int& element) const
```

```cpp
cout << element << ' '
);
```

> Lambda 表达式也称为 Lambda 函数。

提示 22

## 如何定义 Lambda 表达式

Lambda 表达式的定义必须以方括号 `[]` 开始。这些括号本质上告诉编译器 lambda 表达式已经开始。紧随其后的是参数列表，这与在你不使用 lambda 表达式时为 `operator()` 提供实现时提供的参数列表相同。

### 用于一元函数的 Lambda 表达式

接收一个参数的一元运算符 `(Type)` 的 lambda 版本如下：

```cpp
[](Type paramName) { // 此处编写 lambda 表达式代码; }
```

注意，如果你愿意，可以通过引用传递参数：

```cpp
[(Type& paramName) { // 此处编写 lambda 表达式代码; }
```

使用列表 22.1 研究如何使用 lambda 函数通过算法 `for_each()` 来显示标准模板库 (STL) 容器的内容。

### 列表 22.1 通过算法 `for_each()` 显示容器中的元素 —— 使用 Lambda 表达式而非函数对象调用

```cpp
0: #include <algorithm>
1: #include <iostream>
2: #include <vector>
3: #include <list>
4:
5: using namespace std;
6:
7: int main()
8: {
9:     vector<int> numsInVec = {1, 2, 3, 4, 5};
10:    list<char> charsList = {'a', 'b', 'c', 'd', 'e'};
11:
12:    // 打印 vector 中的每个整数
13:    for_each(numsInVec.begin(), // 范围开始
14:             numsInVec.end(), // 范围结束
15:             [](const int& element) { cout << element << ' '; }); // lambda 表达式
16:
17:    // 打印 list 中的每个字符
18:    for_each(charsList.begin(), // 范围开始
19:             charsList.end(), // 范围结束
20:             [](const char& element) { cout << element << ' '; }); // lambda 表达式
21:
22:    return 0;
23: }
```
