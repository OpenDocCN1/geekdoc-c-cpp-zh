
如果我在字符串映射中插入两次字符串 `"Jack"`，会发生什么？

`map` 设计初衷不是用于插入非唯一值。因此，该映射仍然只会包含一个键名为 `"Jack"` 的键值对。

在前面的示例中，如果我想拥有两个 `"Jack"` 实例，我应该修改什么？

根据设计，`map` 只持有唯一值。你需要将所选的容器更改为 `multimap`。

`multimap` 的哪个成员函数可以返回容器中某个特定值的元素计数？

`count(value)` 是感兴趣的函数。

我使用 `find()` 函数在映射中找到了一个元素，并获得了一个指向它的迭代器。我应该使用这个迭代器来更改所指向的值吗？

不。某些 STL 实现允许用户通过 `find()` 返回的迭代器更改 `map` 内部元素的值。然而，这并不是正确的做法。指向 `map` 中元素的迭代器应该被当作常量迭代器（const iterator）使用——即使你的 STL 实现没有强制要求这样做。

我正在使用一个不支持 `auto` 关键字的旧编译器。我该如何声明一个持有 `map::find()` 返回值的变量？

迭代器始终使用以下语法定义：

```
container<Type>::iterator variableName;
```

因此，整数映射的迭代器声明如下：

```cpp
std::map<int>::iterator pairFound = mapIntegers.find(1000);
if (pairFound != mapIntegers.end()) {
  // 执行某些操作
}
```

## 工作坊

工作坊包含了测验题，帮助你巩固对所涵盖内容的理解，并提供了练习题以提供使用所学知识的经验。在检查附录 E 中的答案之前，尝试回答测验和练习题，并确保在进入下一节之前理解了答案。

### 测验

- 1. 你声明了一个整数映射 `map<int>`。哪个函数提供了排序标准？
- 2. 你会在 `multimap` 的哪里找到重复元素？
- 3. 哪个 `map` 或 `multimap` 函数提供了容器中元素的数量？
- 4. 你会在 `map` 的哪里找到重复元素？

### 练习题

- 1. 你需要编写一个可以像电话簿那样的应用程序，其中每个人的名字不需要是唯一的。你会选择哪种容器？写出该容器的定义。
- 2. 以下是你的字典应用程序中的一个映射模板定义：

```cpp
map<WordProperty, string, fPredicate> mapWordDefinition;
```

其中 `WordProperty` 是一个结构：

```cpp
struct WordProperty {
  string word;
  bool isLatinBase;
};
```

定义二元谓词 `fPredicate`，帮助映射根据其包含的字符串属性对类型为 `WordProperty` 的键进行排序。
- 3. 通过一个简单的程序证明 `map` 不能接受重复条目，而 `multimap` 可以。

# 第 21 节

## 理解函数对象

函数对象或*仿函数*（functors）听起来可能很奇异或令人生畏，但它们是 C++ 中的实体，你可能已经见过甚至在使用它们，只是并没有意识到。在本节中，你将学习：

- 函数对象的概念
- 函数对象作为谓词的使用
- 如何使用函数对象实现一元和二元谓词

## 函数对象与谓词的概念

在概念层，函数对象是像函数一样工作的对象。在实现层上，函数对象是实现了 `operator()` 的类对象。

### 函数对象的典型应用

541

#### 提示

C++11 引入了 lambda 表达式，它是一种无名的函数对象。

列表 21.1 中 `struct DisplayElement<T>` 的 lambda 表达式版本将整个代码（包括结构体的定义及其用法）压缩在 `main()` 函数中的三行内，替换了第 21–24 行：

```cpp
// 使用 lambda 表达式显示元素
for_each (numsInVec.begin(), // 范围开始
    numsInVec.end(), // 范围结束
    [](int& element) { cout << element << ' '; });
// Lambda 表达式
```

因此，lambdas 是 C++ 的一项极佳改进，“Lambda 表达式”。列表 22.1 展示了如何在 `for_each()` 中使用 lambda 函数来显示容器的内容，而不是像列表 21.1 那样使用函数对象。

当你能够使用 `struct` 的对象来存储信息时，使用 `struct` 实现的函数对象的真正优势就显现出来了。这是 `DisplayElement` 无法做到的，因为 `struct` 除了 `operator()` 之外还可以拥有成员属性。下面是一个利用成员属性的稍微修改的版本：

```cpp
template <typename elementType>
struct DisplayElementKeepCount
{
    int count;

    DisplayElementKeepCount() // 构造函数
    {
        count = 0;
    }

    void operator () (const elementType& element)
    {
        ++ count;
        cout << element << ' ';
    }
};
```

前面的代码段 `DisplayElementKeepCount` 是对之前版本的微调。`operator()` 不是一个 `const` 成员函数，因为它会递增（因此改变）成员变量 `count`，以记录显示数据的次数。该计数可以通过公共成员属性 `count` 获取。使用这种可以同时存储状态的函数对象的优势在列表 21.2 中所示。

### 列表 21.2 持有状态的函数对象

```cpp
0: #include<algorithm>
1: #include<iostream>
2: #include<vector>
3: using namespace std;
4:
5: template<typename elementType>
6: struct DisplayElementKeepCount
7: {
8:     int count;
9:
10:    DisplayElementKeepCount() : count(0) {} // 构造函数
11:
12:    void operator()(const elementType& element)
13:    {
14:        ++ count;
15:
16:        cout << element<< ' ';
17:    }
18:
19: int main() {
20:    vector<int> numsInVec{22, 2017, -1, 999, 43, 901 };
21:    cout << "Displaying the vector of integers: " << endl;
22:
23:
24:    DisplayElementKeepCount<int> result;
25:    result = for_each(numsInVec.begin(),
26:                       numsInVec.end(),
27:                       DisplayElementKeepCount<int>());
28:
29:    cout << endl << "Functor invoked " << result.count << " times";
30:
31:    return 0;
32: }
```

#### 输出

```
Displaying the vector of integers:

22 2017 -1 999 43 901

Functor invoked 6 times
```

#### 分析

此示例与列表 21.1 中示例最大的区别在于将 `DisplayElementKeepCount()` 作为 `for_each()` 的返回值。在 `struct DisplayElementKeepCount` 中实现的 `operator()` 由算法 `for_each` 为容器中的每个元素各调用一次。它显示元素并递增存储在成员属性 `count` 中的计数器。在 `for_each()` 完成后，你使用第 29 行的对象来显示元素被显示的次数。请注意，在这种情况下，使用普通函数而不是在 `struct` 中实现的函数，将无法直接提供这一功能。

### 一元谓词

返回 `bool` 的一元函数称为谓词。此类函数有助于 STL 算法做出决策。列表 21.3 是一个示例谓词，用于判断输入元素是否为初始值的倍数。

#### 列表 21.3 判断一个数是否为另一个数倍数的一元谓词

```cpp
0: // 作为一元谓词的结构
1: template <typename getType>
2: struct IsMultiple
3: {
4:     numberType Divisor;
5:
6:     IsMultiple (const numberType& divisor)
7:     {
8:         Divisor = divisor;
9:     }
10:    bool operator () (const numberType& element) const
11:    {
12:        // 检查元素是否是除数的倍数
13:        return ((element % Divisor) == 0);
14:    }
15: };
```

#### 分析

`operator()` 返回 `bool` 并可以作为一元谓词工作。该结构体有一个构造函数，并在第 8 行被初始化为除数的值。存储在对象中的该值随后被用于判断用于比较的元素是否能被其整除，正如你在 `operator()` 的实现中所看到的，在第 14 行使用了数学取模运算符 `%`，该运算符返回除法运算的余数。谓词比较的就是该余数。

### 课程 21：理解函数对象

在第 21 节中，我们使用谓词 `IsMultiple` 来判断一个元素是否为除数的倍数。

#### 列表 21.4 在 find_if 使用一元谓词在向量中查找

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3: using namespace std;
4: // 作为一元谓词的结构
5: template <typename getType>
6: struct IsMultiple
7: {
8:     numberType Divisor;
9:
10:    IsMultiple (const numberType& divisor)
11:    {
12:        Divisor = divisor;
13:    }
14:    bool operator () (const numberType& element) const
15:    {
16:        // 检查元素是否是除数的倍数
17:        return ((element % Divisor) == 0);
18:    }
19: };
20:
21: int main() {
22:    vector<int> numsInVec{22, 2017, -1, 999, 43, 901};
23:    cout << "The vector contains ";
24:
25:    cout << "Enter divisor (> 0): ";
26:    int divisor;
27:    cin >> divisor;
28:
29:    auto element = find_if(numsInVec.begin(),
30:                            numsInVec.end(),
31:                            IsMultiple<int>(divisor));
32:
33:    if (element != numsInVec.end())
34:    {
35:        cout << "First element in vector divisible by " << divisor;
36:        cout << ": " << *element << endl;
37:    }
38:
39:    return 0;
40: }
```

#### 输出

```
The vector contains 22 2017 -1 999 43 901

Enter divisor (> 0): 4

First element in vector divisible by 4: 22
```

#### 分析

示例从一个整数向量开始。一元谓词的使用是在第 29 行的 `find_if()` 中。在这里，函数对象 `IsMultiple` 被初始化为用户提供的除数。`find_if()` 通过为范围内的每个元素调用一元谓词来工作。当 `operator()` 对元素返回 `true` 时（当元素被除后不产生余数时），`find_if()` 返回该元素的迭代器。`find_if()` 操作的结果与容器的 `end()` 进行比较以验证是否找到了元素，如第 33 行所示，随后使用迭代器显示值，如第 36 行所示。

### 二元函数

类型为 `f(x, y)` 的函数在根据输入返回值时特别有用。此类二元函数可以用于涉及操作数的各种算运算，如加法、乘法、减法等。一个返回参数乘积的示例二元函数可以写为：

```cpp
template <typename elementType>
class Multiply
{
public:
    elementType operator () (const elementType& elem1, const elementType& elem2)
    {
        return elem1 * elem2;
    }
};
```

感兴趣的实现再次是 `operator()`，它接受两个参数并返回它们的乘积。此类二元函数用于 `std::transform()` 等算法，其中你可以用它来乘以两个容器的内容。列表 21.5 展示了在 `std::transform()` 中使用二元函数的方法。

#### 列表 21.5 使用二元函数相乘两个范围

```cpp
0: #include <vector>
1: #include <iostream>
2: #include <algorithm>
3:
4: template <typename elementType>
5: class Multiply
6: {
7: public:
8:     elementType operator (const elementType& elem1,
9:                          const elementType& elem2)
10:    {
11:        return (elem1 * elem2);
12:    }
13: };
14:
15: int main ()
16: {
17:     using namespace std;
18:
19:     vector<int> multiplicands{0, 1, 2, 3, 4};
20:     vector<int> multipliers{100, 101, 102, 103, 104};
21:
22:     // 存储乘法结果的第三个容器
23:     vector<int> vecResult;
24:
25:     // 为乘法结果分配空间
26:     vecResult.resize(multipliers.size());
27:     transform(multiplicands.begin(), multiplicands.end(), // 乘数的范围
28:               multipliers.begin(), multipliers.end(), // 乘数值
29:               vecResult.begin(), // 存储结果
30:               Multiply<int> ()); // 相乘
31:
32:     cout << "第一个 vector 的内容是: " << endl;
33:     for (size_t index = 0; index < multiplicands.size(); ++ index)
34:         cout << multiplicands[index] << ' ';
35:     cout << endl;
36:
37:     cout << "第二个 vector 的内容是: " << endl;
38:     for (size_t index = 0; index < multipliers.size(); ++index)
39:         cout << multipliers[index] << ' ';
40:     cout << endl;
41:
42:     cout << "乘法结果是: " << endl;
43:     for (size_t index = 0; index < vecResult.size(); ++ index)
44:         cout << vecResult[index] << ' ';
45:
46:     return 0;
47: }
```

#### 函数对象的典型应用

#### 输出

```
第一个 vector 的内容是:

0 1 2 3 4

第二个 vector 的内容是:

100 101 102 103 104

乘法结果是:

0 101 204 309 416
```

#### 分析
