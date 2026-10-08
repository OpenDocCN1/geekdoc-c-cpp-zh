
### 分析

观察输出以及初始桶数为 8 的 `unordered_map` 如何在填充 8 个键值对（pairs）后，在插入第 9 个对时进行调整大小。此时，桶的数量增加到 64。注意在第 9-11 行中使用的方法 `max_bucket_count()`、`load_factor()` 和 `max_load_factor()`。除了这些，代码的其他部分与 `std::map` 并没有太大区别。这包括第 42 行中 `find()` 的用法，它返回一个类似于 `std::map` 的迭代器，需要与操作的 `end()` 进行比较。

# 注意事项

无论键的顺序如何，都不要依赖 `unordered_map` 中元素的顺序（这也是其命名的由来）。在 map 中，一个元素相对于其他元素的顺序取决于许多因素，包括其键、插入顺序以及桶的数量等。
这些容器针对搜索性能进行了优化，在遍历它们时，你不应该依赖其元素的顺序。

# 第 20 节：STL Map 类

## 备注

`std::unordered_map` 提供的插入和搜索（在无冲突的情况下）几乎是常数时间复杂度，且与包含的元素数量无关。然而，这并不意味着 `std::unordered_map` 优于在所有情况下都提供对数复杂度的 `std::map`。常数项可能大得多，导致在包含元素数量不高的情况下，后者的速度反而更慢。

在执行了模拟真实场景使用的基准测试后，根据容器类型做出决策是非常重要的。

| 应该 (DO) | 避免 (DON'T) |
|---|---|
| 在需要键是唯一的键值对的情况下，使用 `map`。 | 不要忘记 `multimap::count(Key)` 可以告诉你容器中使用该键索引的键值对数量。 |
| 在需要键可以重复的键值对的情况下（例如电话簿），使用 `multimap`。 | 不要忘记通过与容器的 `end()` 比较来检查 `find()` 操作的结果。 |
| 记住 `map` 和 `multimap` 与其他 STL 容器一样，都具有成员函数 `size()`，可以告诉你它们包含的键值对数量。 | |
| 当常数时间插入和搜索至关重要时（通常当元素数量非常多时），使用 `unordered_map` 或 `unordered_multimap`。 | |

## 总结

在本节中，你学习了如何使用 STL map 和 multimap、它们的重要函数以及它们的特性。你还学习了这些容器具有对数复杂度，且 STL 以 `unordered_map` 和 `unordered_multimap` 的形式提供哈希表。这些在 `insert()` 和 `find()` 操作中的性能与容器大小无关。你学习了使用谓词自定义排序标准的重要性，正如列表 20.5 中的目录应用程序所示。

# 问答 (Q&A)

问：我该如何声明一个整数 map，使其按幅值降序顺序排序或存储？

答：`map<int>` 定义了一个整数 map。它使用默认的排序谓词 `std::less` 按幅值升序排序项目，也可以表示为 `map<int, less<int>>`。要按幅值降序排序，将 map 定义为 `map<int, greater<int>>`。

问：如果我在字符串 map 中插入两次字符串 "Jack"，会发生什么？

答：map 的设计目的不是为了插入非唯一值。因此，`std::map` 类的实现不允许插入第二个值。

问：在前面的示例中，如果我想拥有两个 "Jack" 实例，我应该修改什么？

答：从设计上讲，map 只持有唯一值。你需要将选择的容器改为 `multimap`。

问：哪个 multimap 成员函数返回容器中特定值的计数？

答：`count(value)` 是感兴趣的函数。

问：我使用 `find()` 函数在 map 中找到了一个元素，并获得了一个指向它的迭代器。我可以使用这个迭代器来更改所指向的值吗？

答：不行的。某些 STL 实现可能允许用户通过 `find()` 返回的迭代器更改 map 内部元素的值。然而，这不是正确的做法。指向 map 的迭代器应该是常量迭代器（const iterator），即使你的 STL 实现没有强制要求。

问：我正在使用不支持 `auto` 关键字的旧编译器。我该如何声明一个持有 `map::find` 返回值的变量？

答：迭代器始终由此语法定义：
`container<Type>::iterator variableName;`

因此，整数 map 的迭代器声明如下：

```cpp
std::map<int>::iterator iPairFound = mapIntegers.find(1000);

if (iPairFound != mapIntegers.end())
{
    // ...
}
```

# 工作坊 (Workshop)

工作坊包含了巩固知识的问答题以及针对所学内容的练习。

# 测验 (Quiz)

1. 你声明了一个整数 map，什么提供了排序标准？
2. 在 multimap 中哪里找到（查找）元素？
3. 哪个 map 或 multimap 提供了它们包含的键值对数量？
4. 在 map 中哪里找到重复元素？

# 练习 (Exercises)

1. 编写一个键不需要唯一的字典应用程序。你会选择什么？
2. 下面是一个模板定义：
```cpp
struct wordProperty
{
    string strWord;
    bool bisLatin;
};
```
定义二元谓词 `fPredicate`，帮助根据字符串排序。
3. 通过一个简单的程序演示 map 不接受重复项，而 multimap 可以。

# 第 21 节：理解函数对象

函数对象或*仿函数*（functors）听起来很奇异或令人生畏，但它们是你可能已经见过、甚至用过的 C++ 实体。在本节中，你将学习

- 函数对象的概念
- 函数对象作为谓词的使用
- 使用函数对象实现一元和二元谓词

## 函数对象与谓词的概念

在概念上，函数对象是作为函数工作的对象。但在实现上，函数对象是实现 `operator()` 的类对象。虽然函数和函数指针也可以归类为函数对象，但实现 `operator()` 的类能够携带状态（即成员属性中的值），这使得它们在标准模板算法中非常有用。

C++ 程序员通常使用的函数对象分为以下类型：

- 一元函数——带一个参数调用的函数，例如 `f(x)`。一个一元函数返回 bool，被称为谓词。
- 二元函数——带两个参数调用的函数，例如 `f(x, y)`。一个返回 bool 的二元函数被称为二元谓词。

返回布尔值的函数对象自然用于需要决策的算法。组合两个函数对象的函数对象被称为自适应对象。

## 一元函数

对单个参数操作的函数是一元函数。一元函数可以执行非常简单的操作，例如在屏幕上显示元素。这可以编写为如下：

```cpp
// 一元函数
template <typename elementType>
void FuncDisplayElement(const elementType& element)
{
    cout << element << ' ';
};
```

## 函数对象的典型应用

函数 `FuncDisplayElement` 接受一个模板类型 `elementType` 的参数，并使用标准输出输出语句 `std::cout` 显示该参数。该函数也可以有另一种表示形式，即函数的实现实际上包含在类或结构体（struct）的 `operator()` 中：

```cpp
// 一个可以作为一元函数的结构体
template <typename elementType>
struct DisplayElement
{
    void operator () (const elementType& element) const
    {
        cout << element << ' ';
    }
}
```

> 注意 `DisplayElement` 是一个 `struct`。如果它是一个 `class`，则 `operator()` 需要赋予 `public` 访问修饰符。`struct` 类似于 `class`，其成员默认是公开的。

这两种实现都可以用于 STL 算法 `for_each`，将集合的内容逐个打印到屏幕上，如列表 21.1 所示。

# 列表 21.1 使用函数在屏幕上显示集合的内容

```cpp
0: #include <algorithm>
1: #include <iostream>
2: #include <vector>
3: #include <list>

5: using namespace std;
// 行为类似于一元函数的结构体
template <typename elementType>
struct DisplayElement
{
   void operator () (const elementType& element) const
   {
       cout << element << ' ';
   }
};

int main ()
{
   vector <int> vecIntegers;
  for (int nCount = 0; nCount < 10; ++ nCount)
    vecIntegers.push_back (nCount);

  list<char> listChars;

  for (char nChar = 'a'; nChar < 'k'; ++nChar)
    listChars.push_back (nChar);

  cout << "Displaying the vector of integers: " << endl;

  // 显示整数数组
  for_each ( vecIntegers.begin ( // 范围开始
            vecIntegers.end ( ) // 范围结束
            DisplayElement<int> ( ); // 一元函数对象

  cout << endl << endl;
  cout << "Displaying the list of characters: " << endl;

  // 显示字符列表
  for_each ( listChars.begin ( // 范围开始
            listChars.end ( ) // 范围结束
            DisplayElement<char> ( ); // 一元函数对象

  return 0;
}
```

# 输出

Displaying the vector of integers:
0 1 2 3 4 5 6 7 8 9

Displaying the list of characters:
a b c d e f g h i j

# 分析

第 8–15 行包含了函数对象 `DisplayElement`，它实现了 `operator()`。在第 32–34 行中可以看到 STL 算法 `std::for_each` 使用了该函数对象，它接受三个参数：第一个是范围的起始点，第二个是范围的结束点，第三个参数是针对范围内每个元素调用的函数。换句话说，代码为 `vecIntegers` 向量每个元素调用了 `DisplayElement::operator()`。注意，与其使用结构体 `struct DisplayElement`，你也可以使用 `FuncDisplayElement` 达到相同效果。第 40–42 行演示了字符列表的功能。

# 第 21 节：理解函数对象

### 提示

C++11 引入了 lambda 表达式，它是一种无名的函数对象。

列表 21.1 中 `struct DisplayElement<T>` 的 lambda 表达式版本将整个代码（包括结构体的定义及其用法）压缩在 `main()` 函数中的三行内，替换了第 32-34 行：
```cpp
// 使用 lambda 表达式显示整数数组
for_each ( vecIntegers.begin () // 范围开始
vecIntegers.end () // 范围结束
[](int& element) { cout << ' '; } ); // Lambda 表达式
```

因此，lambda 是 C++ 的一个极大改进，你不应该错过第 22 节“C++11 Lambda 表达式”中的它们。列表 22.1 演示了在 `for_each` 中使用 lambda 函数显示容器的内容，而不是像列表 21.1 那样使用函数对象。

在 `struct` 中实现的函数的真正优势在于当你可以使用该对象来存储信息时。`DisplayElement` 不能像 `struct` 那样这样做，因为它除了 `operator()` 之外没有成员属性。以下是一个利用成员属性的稍微修改的版本：

```cpp
template <typename elementType>
struct DisplayElementCount
{
    int Count;
    DisplayElementCount () // 构造函数
    {
        Count = 0;
    }
    void operator () (const elementType& element)
    {
        Count++;
        cout << element << ' ';
    }
};
```

在前面的代码中，`DisplayElementCount` 是前一个版本的微调。`operator()` 不是一个 `const` 函数，因为它增加了（因此改变了）成员 `Count`，以记录显示数据的次数。该计数可以通过公开属性 `Count` 可用。

使用此类还可以存储状态的函数对象的优势在列表 21.2 所示。

# 列表 21.2 使用函数对象持有状态

```cpp
0: #include <algorithm>
1: #include <iostream>
2: #include <vector>
using namespace std;

template<typename elementType>
struct DisplayElementCount
{
    int Count;

   // 构造函数
   DisplayElementCount() : Count(0) {}

   // 显示元素，持有计数！
   void operator()(const elementType& element)
   {
       Count++;
       cout << element << ' ';
   }
};

int main()
{
    vector<int> vecIntegers;
    for(int nCount = 0; nCount < 10; ++ nCount)
       vecIntegers.push_back(nCount);

    cout << "Displaying the vector of integers: " << endl;

    // 显示整数数组
    DisplayElementCount<int> Result;
    for_each(vecIntegers.begin(), // 范围开始
                   vecIntegers.end(), // 范围结束
                   Result()); // 一元函数对象

    cout << endl << endl;
    cout << "Total elements displayed: " << Result.Count << endl;

    return 0;
}
```
