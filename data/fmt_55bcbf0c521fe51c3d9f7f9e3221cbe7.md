
从 C++11 开始，STL 提供了 `unordered_set` 和 `unordered_multiset` 类模板。它们与 `set` 和 `multiset` 类相似，有两个不同：(1) `unordered_set` 或 `unordered_multiset` 中存储的值没有任何特定排序；(2) `unordered_set` 和 `unordered_multiset` 类的性能优于 `set` 和 `multiset`。如果你对大量元素进行频繁搜索，且不在意检索顺序，你应该使用 `unordered_set` 或 `unordered_multiset` 代替 `set` 或 `multiset`。

要使用 `unordered_set` 或 `unordered_multiset`，必须在程序中编写 `#include <unordered_set>` 指令。在大多数情况下，使用 `unordered_set` 或 `unordered_multiset` 与使用 `set` 或 `multiset` 相似。

# 检查点

- 17.28 `set` 和 `vector` 有哪些不同？
- 17.29 写一个语句定义名为 `aset` 的 `set` 对象，它可以包含字符串。
- 17.30 写一个语句定义名为 `aset` 的 `set` 对象，它可以包含整数。该集合应初始化为这些值：10, 20, 30, 40。
- 17.31 使用 `insert()` 成员函数向 `set` 插入一个值会发生什么？如果值已经存在？
- 17.32 `set` 类的 `count` 成员函数返回什么？
- 17.33 如果在 `set` 中存储编写的类对象，该类必须重载什么运算符？
- 17.34 `set` 和 `multiset` 之间的区别是什么？

# 算法

概念：许多常用的算法在 STL 中都是以函数模板的形式编写的。

STL 在 `<algorithm>` 头文件中提供了许多算法，这些算法是以函数模板的形式实现的。这些函数对元素范围执行各种操作。元素范围是由两个迭代器表示的元素序列。第一个迭代器指向范围内的第一个元素，第二个迭代器指向范围的末尾（第二个迭代器指向的元素不包含在范围内）。算法可以分为以下几类：

- 最小/最大值算法：确定元素范围内的最小值（`min`）和最大值（`max`）。
- 排序算法：对元素范围进行排序，或者确定一个范围是否已排序。
- 搜索算法：在已排序的范围上执行各种搜索操作。
- 只读序列算法：遍历元素范围，执行各种不修改元素的操作。
- 复制与移动算法：使用各种技术来复制或移动元素范围。
- 交换算法：交换值、元素范围或迭代器指向的值。
- 替换算法：替换指定值的元素。
- 移除算法：移除元素。
- 反转算法：反转范围内元素的顺序。
- 填充算法：用值填充范围内的元素。
- 旋转算法：用值旋转范围内的元素。
- 打乱算法：打乱范围内元素的顺序。
- 集合算法：在元素范围上执行常见的数学集合操作。
- 变换算法：遍历元素范围，对每个元素执行某种操作。
- 分区算法：将元素范围分为两组。
- 合并算法：合并元素范围。
- 排列算法：将元素范围排列为所有可能的不同排列组合。
- 堆算法：创建并操作堆数据结构。
- 字典序比较算法：在两个元素范围之间进行字典序比较。

在编写此内容时，`<algorithm>` 头文件中有 85 个函数模板。关于所有 STL 算法的摘要，请参阅计算机科学门户 www.pernsigheredighed.com/gaddi 上的附录 H。我们不会讨论所有的 STL 算法，但我们将使用其中一些有趣的算法示例。

# 排序与搜索算法

`<algorithm>` 头文件定义了七个用于排序和搜索的函数模板。我们将查看两个：`sort()` 和 `binary_search()`。`sort` 函数采用以下格式：

```
sort(iterator1, iterator2)
```

在通用格式中，`iterator1` 和 `iterator2` 标记元素范围的开始和结束。`sort` 函数按升序对元素范围进行排序。`binary_search()` 函数采用以下格式：

```
binary_search(iterator1, iterator2, value)
```

在通用格式中，参数 `iterator1` 和 `iterator2` 标记按升序排序的元素范围，以及要搜索的 `value`。如果在元素范围内找到了该值，函数返回 `true`，否则返回 `false`。程序 17-23 展示了 `sort()` 和 `binary_search()` 函数。

# 程序 17-23

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() 
{
    int searchValue; // 要搜索的值

    // 创建一个未排序的整数 vector。
    vector<int> numbers = {10, 1, 9, 2, 8, 3, 7, 4, 6, 5};

    // 对 vector 排序。
    sort(numbers.begin(), numbers.end());
```

（程序继续）

# 程序 17-23（继续）

```cpp
16 // 显示 vector。
17 cout << "Here are the sorted values:\n";
18 for (auto element : numbers)
19     cout << element << " ";
20 cout << endl;
21
22 // 获取要搜索的值。
23 cout << "Enter a value to search for: ";
24 cin >> searchValue;
25
26 // 搜索该值。
27 if (binary_search(numbers.begin(), numbers.end(), searchValue))
28     cout << "That value is in the vector.\n";
29 else
30     cout << "That value is not in the vector.\n";
31 return 0;
32 }
```

程序输出

```
Here are the sorted values:
1 2 3 4 5 6 7 8 9 10
Enter a value to search for: 8
That value is in the vector.
```

程序输出

```
Here are the sorted values:
1 2 3 4 5 6 7 8 9 10
Enter a value to search for: 99
That value is not in the vector.
```

`sort()` 和 `binary_search()` 函数使用 `<` 运算符来比较元素。如果你正在排序和搜索的元素包含你自定义的类，请务必重载 `<` 运算符。例如，回想本章早些时候显示的 `Customer` 类，在我们讨论 `map` 类时（`Customer.h` 文件的内容）提到的。`Customer` 持有关于客户的两个数据：客户编号和姓名。（由于我们使用一个元素范围通过指定的客户编号进行搜索，因此不需要为客户姓名提供有意义的值）。`binary_search` 函数将接受此对象作为参数，并将在指定的元素范围内进行搜索。如果在元素范围内找到了具有匹配客户编号的对象，该函数将返回 `true`；否则返回 `false`。

# 程序 17-24

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include "Customer.h"
using namespace std;

int main()
{
    int searchValue; // 要搜索的值

    // 创建一个未排序的 Customer vector。
    vector<Customer> customers = {
        Customer(10, "Scott"),
        Customer(1, "Hill"),
        Customer(9, "Megan"),
        Customer(2, "Sarah"),
        Customer(8, "Austin"),
        Customer(3, "John"),
        Customer(7, "Jane"),
        Customer(4, "Jane"),
        Customer(6, "Bob"),
        Customer(5, "Alice")
    };

    // 对 vector 排序。
    sort(customers.begin(), customers.end());

    // 显示 vector。
    cout << "Here are the sorted values:\n";
    for (auto element : customers)
        cout << element << " ";
    cout << endl;

    // 获取要搜索的值。
    cout << "Enter a value to search for: ";
    cin >> searchValue;

    // 搜索该值。
    if (binary_search(customers.begin(), customers.end(), Customer(searchValue)))
        cout << "That value is in the vector.\n";
    else
        cout << "That value is not in the vector.\n";

    return 0;
}
```

程序输出

```
Here are the sorted values:
1 Hill 2 Sarah 3 John 4 Jane 5 Alice 6 Bob 7 Jane 8 Austin 9 Megan 10 Scott
Enter a value to search for: 8
That value is in the vector.
```

程序输出

```
Here are the sorted values:
1 Hill 2 Sarah 3 John 4 Jane 5 Alice 6 Bob 7 Jane 8 Austin 9 Megan 10 Scott
Enter a value to search for: 99
That value is not in the vector.
```

# 检测排列

如果一个范围有 N 个元素，那么这些元素就有 N! 种可能的排列。每种排列被称为一个排列。例如，我们有一个包含以下元素的 vector：

```
1, 2, 3
1, 3, 2
2, 1, 3
2, 3, 1
3, 1, 2
3, 2, 1
```

vector 中有三个元素，因此有六种重新排列元素的方法。STL 的 `is_permutation()` 函数判断一个元素范围是否是另一个元素范围的排列。其通用格式如下：

```
is_permutation(iterator1, iterator2, iterator3)
```

在通用格式中，`iterator1` 和 `iterator2` 标记第一个元素范围的开始和结束。`iterator3` 标记第二个元素范围的开始，假设其数量与第一个范围相同。如果第二个范围是第一个范围的排列，函数返回 `true`，否则返回 `false`。

程序 17-25 展示了 `is_permutation()` 函数。它使用该函数来确定一组数字是否与中奖的彩票号码匹配。

# 程序 17-25

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
int main() {
    const int MAX = 5; // 每张彩票的数字
    vector<int> winning(MAX); // 中奖号码
    vector<int> player(MAX); // 彩票上的号码
    // 获取中奖号码。
    cout << "Enter the " << MAX << " winning numbers:\n";
    for (auto &element : winning) {
        cout << "> ";
        cin >> element;
    }
    // 获取在彩票上购买的号码。
    cout << "\nEnter your " << MAX << " lottery numbers:\n";
    for (auto &element : player) {
        cout << "> ";
        cin >> element;
    }
    // 检查是否有中奖者。
    if (is_permutation(winning.begin(), winning.end(), player.begin())) {
        cout << "You won the lottery!\n";
    } else {
        cout << "Sorry, you did not win.\n";
    }
    return 0;
}
```

# 程序输出

```
输入 5 个中奖号码：
> 10
> 25
> 67
> 88
> 93
输入你的 5 个彩票号码：
> 25
> 15
> 62
```

（程序输出继续）

# 程序 17-25（续）

```
> 93
> 88
很抱歉，你没有中奖。
```

# 程序输出

```
输入 5 个中奖号码：
> 10
> 25
> 67
> 88
> 93
输入你的 5 个彩票号码：
> 67
> 10
> 93
> 88
> 25
你中奖了！
```

# 将你自己的函数插入算法中

当 C++ 程序运行时，该程序中每个函数的代码都存储在内存中。你可以使用函数的名称来获取该函数在内存中的地址，就像使用数组名称来获取数组在内存中的地址一样。这种能力允许你获取函数指针，即指向函数可执行代码的指针。

STL 中的许多函数模板被设计为接受函数指针作为参数。这允许你将自己的一个函数“插入”算法中。例如，这里是 `for_each` 函数的通用格式：

```cpp
for_each(iterator1, iterator2, function)
```

在通用格式中，`iterator1` 和 `iterator2` 参数标记了元素范围的开始和结束。`function` 参数是函数的地址，该函数接受一个元素作为参数（函数返回的任何值都会被忽略）。`for_each()` 函数遍历元素范围，将每个元素作为参数传递给函数。

程序 17-26 展示了 `for_each()` 函数。该程序定义了一个名为 `doubleNumber()` 的函数。`doubleNumber()` 函数接受一个 `int` 引用作为参数，并将该参数的值翻倍。该程序使用 `for_each()` 函数将整数向量中每个元素的值翻倍。

# 程序 17-26

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// 函数原型
void doubleNumber(int &);

int main()
{
    vector<int> numbers = { 1, 2, 3, 4, 5 };

    // 显示翻倍前的数字。
    for (auto element : numbers) {
        cout << element << " ";
    }
    cout << endl;

    // 将向量中每个元素的值翻倍。
    for_each(numbers.begin(), numbers.end(), doubleNumber);

    // 显示翻倍后的数字。
    for (auto element : numbers) {
        cout << element << " ";
    }
    cout << endl;

    return 0;
}

/****************************************************
// doubleNumber 函数将 n 的值翻倍。
****************************************************/
void doubleNumber(int &n) {
    n = n * 2;
}
```

程序输出

```
1 2 3 4 5
2 4 6 8 10
```

另一个例子是 `count_if()` 函数。`count_if()` 函数的通用格式为：

```cpp
count_if(iterator1, iterator2, function)
```
