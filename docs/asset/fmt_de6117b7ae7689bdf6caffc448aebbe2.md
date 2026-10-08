
有几个容器不支持迭代器，它们是：容器适配器（container adapters）、`bitset` 和 `valarray`。注意：C++11 为 `valarray` 定义了迭代器 `begin()` 和 `end()`。

## STL 迭代器

迭代器、容器和算法是是由 Alexander Stepanov 等人在 20 世纪 90 年代初在惠普编写的标准模板库组件，随后在标准库中合并并改进。

迭代器是特殊指针的抽象，用于对给定容器（如 `vector`, `map` 和用户自定义容器类）的元素进行解引用。

每个容器类都包含用于生成迭代器的成员函数，例如成员 `begin()` 和 `end()` 分别返回指向第一个元素和最后一个元素之后元素的迭代器。

下图描述了迭代器 (`*it`) 与其容器 (`vector<int>data {1111, 1134, 1134, 1124, 1124, 1134, 1111, 1176, 1124, 1134, 1176}`) 之间的关系。

然后，迭代器可以在算法操作（如 `sort`, `accumulate` 和自定义算法函数）中包含容器的元素。

换句话说，迭代器将容器与算法关联起来。最常用的迭代器来自 `begin()` 和 `end()` 如下所示：

如图所示，`data[0]` 和 `data.begin()` 都代表同一个元素，即 elem 1，但 `data[N]` 和 `data.end()` 代表一个“无人区”，访问这会导致运行时错误。然而，成员函数 `end()` 在迭代语句中构造条件时非常有用。

以下代码代码阐明了迭代器的这一基本属性：

```cpp
// iterators.cpp
#include "..\.\my_essentials.hpp"
void illustrate_iterators()
int arr[] = {1111, 1134, 1134, 1124, 1124, 1134, 1111, 1176, 1124, 1134, 1176};

vector<int>data(arr, arr+sizeof(arr)/sizeof(arr[0])); //
vector<int>data2{1111, 1134, 1134, 1124, 1124, 1134, 1111, 1176, 1124, 1134, 1176}; // 在 gcc-4.7.0 下正常

cout << "\nIteration of iterators: \n"
cout << "\n Given iteration: data =\n";
for(auto element: data) // 范围 for 在 VC10 中不支持
cout << element << " ";
cout << "\n\n Let us define an iterator, say *it for this vector.\n";
```

```cpp
vector<int>::iterator it = data.begin();
```

注意：

STL 容器每个容器模板类定义了自己的迭代器成员类，因此 `vector<int>::iterator` 不同于 `list<int>::iterator`。

```cpp
/*
out << "Thus,\t*it = \t << *it << "\" is that data[0] Iterators can be incremented, i.e, ++it;\n"
++it;
```

```cpp
cout << " After +*it = \t << *it << \" is that data[1] Therefore, iterator *it dereferences through vector.\nSo, let us express the entire using the vector using:\n\t(";
```

```cpp
cout << "In the function unique() 返回了指向标识符 "my_unique" 的迭代器，从该处开始，重复元素被推到末尾之前。
```

任务：由于这个 vector 有重复数字，

我们可以只保留每个数字的一个副本并删除重复项吗？

是的，可以！

为了实现，我们将迭代器通过三种 STL 算法如下所示：

步骤.1 升序排序：

迭代器通过 `sort()` 之后：

( 1111; 1111; 1124; 1124; 1124; 1134; 1134; 1134; 1176; 1176; )

步骤.2 将相邻元素移动到左侧：

迭代器通过 `unique()` 之后：

( 1111; 1124; 1134; 1134; 1134; 1176; 1176; )

步骤.3 删除那些重复的元素：

迭代器通过 `erase()` 之后，即：

最终：( 1111; 1124; 1134; 1176 )

```cpp
// 用于打印的容器无关代码
// 带有一个类型名的容器
template<typename container>
void cout_container(const std::string& message, const container& data) {
    std::cout << message << "{";";
    if(data.empty()){
        std::cout << "NULL"<<std::endl;
        return;
    }
    auto start = data.begin();
    auto end = data.end();
}
```

```cpp
while(true)
{
    std::cout << *start;
    ++start;
    if(start != end)
        std::cout << ", ";
    else
        std::cout << "{}" << std::endl;
    break;
}
```
// 让我们将此模板添加到 `"my_essentials.hpp"` 中并使用以下代码测试该模板。
然后，让我们使用这个模板：

```cpp
// cout_containers.\cpp
#include "../my_essentials.hpp"
#include <array>
#include <vector>
#include <unordered_set>
#include <forward_list>
#include <set>
int main()
{
    // 让我们定义， // 一个固定大小数组
    array<int,6> arr = {1,3,5,1,2,4};
    cout_container("my array\t = ", arr);
    // 一个 vector
    vector<int> vec(arr.begin(), arr.end());
    cout_container("my vector\t = ", vec);
    // 一个单向链表
    forward_list<int>
    f_lis(arr.begin(), arr.end());
    cout_container("my forward_list\t = ",f_lis);
    // 一个无序集合
    unordered_set<int>
    u_set(arr.begin(), arr.end());
    cout_container("my unordered_set = ", u_set); // 一个集合容器
    set<int>se(arr.begin(), arr.end());
    cout_container("my set\t = ", se);
    just_pause();
}
```

输出结果：
my array = {1, 3, 5, 1, 2, 4}
my vector = {1, 3, 5, 1, 2, 4}
my forward_list = {1, 3, 5, 1, 2, 4}
my unordered_set = {1, 3, 5, 1, 2, 4}
my set = {1, 2, 3, 4, 5}

在我们实验了迭代器的某些应用后，现在我们在下面的表中总结了它们的操作。

迭代器并没有单一的定义，因此并不是所有的迭代器都能支持上述的所有操作。迭代器分为五类，即：
因此，通过这一主要讨论，我们发现指针及其对不同对象的解引用属性对迭代器和 STL 操作起着至关重要的作用。

# 第7章：STL 算法

STL 算法位于 `<algorithms>` 头文件中，因此我们需要在程序中包含它。算法可以分类为：

- 非修改性算法：例如 `for each`, `count`, `search` 等。
- 修改性算法：例如 `copy`, `transform` 等。
- 移除算法：`remove`, `remove if` 等。
- 变动算法：`reverse`, `rotate` 等。
- 排序算法：`sort`, `partial sort` 等。
- 有序范围算法：`binary search`, `partial sum`, `merge` 等。
- 数值算法：`accumulate`, `partial sum`, `inner product`。

等等等。
接下来的示例展示了 `sort()` 函数是如何在数组上工作的。

## 程序 13.11：使用 sort 算法对数组进行排序

```cpp
#include <iostream>
#include <algorithm>
using namespace std; 
int main()
{
int a[] = {3,5,7,2,9};
sort(a, a + 5);
cout << "Sorted Array:" << endl;
for (int i = 0; i < 5; i++)
    cout << a[i] << " ";
return 0;
}
```

输出：
Sorted Array:
2 3 5 7 9

在上面的示例中，当我们把数组名作为参数传递时，我们是在告诉函数从数组的开头开始排序。如果我们想让它从数组的第三个元素开始排序，可以使用 `sort(a+3, a+5);`。

我们使用了 `a+5` 作为第二个参数，指定了我们想要排序到数组的最后一个元素。
现在，类似的 `sort()` 函数可以与 `vector` 容器工作，如下程序所示。这表明 STL 算法是通用的。

## 程序 13.12：使用 sort 算法对 vector 进行排序

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
int main()
{
int a[] = {5,3,7,6,2,9};
vector<int> v(a, a+6);
sort(v.begin(), v.end());
for (int i = 0; i != v.size(); i++)
    cout << v[i] << " ";
cout << endl;
return 0;
}
```
输出：
2 3 5 6 7 9

你可以看到，排序函数的工作方式与数组几乎相同。`sort()` 的第一个参数接受一个指向第一个元素的迭代器，因此它将从第一个元素开始排序。`end()` 返回一个指向最后一个元素之后的迭代器，注意 `sort` 排序到这里。

## find() 和 count() 算法

`find()` 算法有助于从容器中查找特定值。`count()` 算法用于统计特定值在容器中出现的次数。

## 程序 13.13：使用 find 算法从 vector 中查找值

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
int main()
{
vector<int> v;
for(int i = 0; i < 10; i++)
    v.push_back(i);
int a = 5;
vector<int>::iterator it;
it = find(v.begin(), v.end(), a);
if(it != v.end()) {
    cout << "found " << a << endl;
} else {
    cout << "could not find " << a << endl;
}
int c = count(v.begin(), v.end(), a);
cout<<"Number of in vector:" << c; 
return 0;
}
```
输出：
found 5
Number of in vector:1

## For each()

该算法将指定的函数对象应用于容器中的每个元素。容器中的原始值不会改变，但它用于显示修改后的元素。它前两个参数作为开始和结束范围。第三个参数是函数对象的地址。例如 `for_each()` 算法对数组的所有元素平方并显示它们。

## 程序 13.14：使用 each 算法对数组的所有元素平方

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
void square(int a)
{ cout<<a<<a<<endl; }
int main()
{
  int s[]={1,2,3,4};
  for_each(s, s+4, square);
  return 0;
}
```
