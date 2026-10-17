
```
1 ******************************************************************
2 * 一个寻找两个集合并集的程序 *
3*****************************************************************/
#include <set>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

10 // 打印函数
11 void print(int value)
12 {
13 cout << value << " ";
14 }

16 int main()
17 {
18 // 创建第一个集合
19 set<int> first;
20 first.insert(10);
21 first.insert(19);
22 first.insert(14);
23 first.insert(17);
24 first.insert(13);
25 cout << "Elements of first set" << endl;
26 for_each(first.begin(), first.end(), print());
27 cout << endl;

29 // 创建第二个集合
30 set<int> second;
31 second.insert(16);
32 second.insert(14);
```

# 程序 19.29 求两个集合的并集（续）

```
32 second.insert(13);
33 second.insert(11);
34 second.insert(20);
35 cout << "Elements of set" << endl;
36 for_each(second.begin(), second.end(), print());
37 cout << endl;
38 // 求两个集合的并集并存储在 vector 中
39 vector<int> temp(10);
40 vector<int>::iterator iter;
41 vector<int>::iterator iterEnd;
42 iterEnd = set_union(first.begin(), first.end(),
43 second.begin(), second.end(), temp.begin());
44 将元素从 vector 拷贝到结果集
45 set<int> result;
46 for (iter = temp.begin(); iter != iterEnd; ++iter)
47 {
48 result.insert(*iter);
49 }
50 cout << "Elements of result set" << endl;
51 for_each(result.begin(), result.end(), print());
52 cout << endl;
53 return 0;
54 }
```

运行：

Elements of first set

10 13 14 17 19

Elements of second set

11 13 14 16 20

Elements of result set

10 11 13 14 16 17 19 20

在 19.29 中，目标序列的大小必须足够大以容纳结果。对于 `set` 来说是不可能的，因为任何创建的 `set` 都是空的。为了解决这个问题，我们创建了一个 `vector` 来临时存放操作的结果，然后将 `vector` 中存储结果的部分拷贝到结果集里。图 19.17 显示了我们使用的过程。

## 19.7.4 数值算法

在 `<numeric>` 头文件中定义了几个数值算法，它们可以对容器或多个容器的元素执行简单的算术运算。请注意，这些算法并不非应用于算术类型（如 `int` 或 `double`）；只要为该类型定义了相应的操作，这些算法就可以应用于它们。表 19.9 显示了一个常用的数值算法。

![](img/ce9c99d45f71111839bc062830bd19fd_927_0.png)

图 19.17 使用 `set_intersection` 操作

| 表 19.9 accumulate 算法 |

| `accumulate(Iter first, Iter last, T init);` |

*accumulate* 算法找到范围 `[first, last]` 内值的和，并将结果加到 *init* 上。

程序 19.30 使用了 *accumulate* 算法。

# 程序 19.30 测试 accumulate 算法

```
****************************************************
/* 一个测试数值算法 accumulate 的程序 *
****************************************************/
#include <vector>
#include <numeric>
#include <iostream>
using namespace std;
// 打印函数
void print(int value)
{
    cout << value << " ";
}
int main() {
// 实例化 vector
vector<int> vec;
vec.push_back(17);
vec.push_back(10);
vec.push_back(13);
vec.push_back(18);

# 程序 19.30 accumulate 算法（续）

```

24 vec.push_back(15);

25 vec.push_back(17);

26 for_each(vec.begin(), vec.end(), print());

27 cout << endl;

28 // 计算和

29 int sum = accumulate(vec.begin(), vec.end(), 0);

30 cout << "Sum of elements: " << sum;

31 return 0;

}

| 单位 |

|---|


| 17 10 13 18 15 17 |

| Sum of elements: |

## 术语

标准模板库 (STL) 由迭代器、容器和算法组成。迭代器是访问容器元素的工具。容器是存储数据的结构，如 `vector`、`list`、`set` 等。算法是对数据执行的操作，如排序、搜索、求和。容器适配器为现有容器提供特定的功能，如栈（`stack`）和队列（`queue`）。迭代器允许对容器元素进行访问。容器可以按顺序存储元素，也可以按关联关系存储元素。算法可以分为非变算法和非变算法两类。

## 习题

- PR-1. 为一个任意类型的 `vector` 编写一个打印所有元素的泛函数。
- PR-2. 为一个任意类型的 `list` 编写一个打印其所有元素的泛函数。
- PR-3. 对于任意类型的 `vector`，编写代码创建一个包含 0, 1, 2, 3, 4 元素的 `vector`，并打印这些元素。
- PR-4. 对于任意类型的 `set`，编写代码创建一个包含 1, 2, 3, 4, 5 元素的 `set`，并打印这些元素。
- PR-5. 编写一个泛函数，用于计算一个包含 1, 2, 3, 4, 5 元素的 `vector` 中所有元素的和并打印。
- PR-6. 编写一个泛函数，用于计算一个包含 1, 2, 3, 4, 5 元素的 `list` 中所有元素的和并打印。
- PR-7. 使用 `for_each` 算法将一个包含 5, 4, 3, 2, 1 元素的 `vector` 中的元素翻倍并按升序打印。
- PR-8. 使用 `for_each` 算法将一个包含 5, 4, 3, 2, 1 元素的 `vector` 中的元素翻倍并按降序打印。
- PR-9. 使用 `sort` 算法对一个包含 5, 4, 3, 2, 1 元素的 `vector` 进行排序。
- PR-10. 使用 `reverse` 算法对一个包含 5, 4, 3, 2, 1 元素的 `vector` 进行反转。
- PR-11. 使用 `find` 算法在一个包含 5, 4, 3, 2, 1 元素的 `vector` 中查找元素 3。
- PR-12. 使用 `find` 算法在一个包含 5, 4, 3, 2, 1 元素的 `list` 中查找元素 3。
- PR-13. 使用 `count` 算法统计一个包含 5, 4, 3, 2, 1 元素的 `vector` 中元素 3 出现的次数。
- PR-14. 使用 `count` 算法统计一个包含 5, 4, 3, 2, 1 元素的 `list` 中元素 3 出现的次数。
- PR-15. 使用 `accumulate` 算法计算一个包含 5, 4, 3, 2, 1 元素的 `vector` 中所有元素的和。
- PR-16. 使用 `accumulate` 算法计算一个包含 5, 4, 3, 2, 1 元素的 `list` 中所有元素的和。
- PR-17. 创建一个包含 1, 2, 3, 4, 5 元素的 `vector`，在末尾插入 6，在开头插入 0，在索引 2 处插入 7，然后打印该 `vector` 的元素。
- PR-18. 创建一个包含 1, 2, 3, 4, 5 元素的 `list`，删除第一个元素和最后一个元素。
- PR-19. 创建一个包含 1, 2, 3, 4, 5 元素的 `set`，删除元素3。
- PR-20. 创建一个包含 1, 2, 3, 4, 5 元素的 `vector`，删除所有元素 3。
- PR-21. 创建一个包含 1, 2, 3, 4, 5 元素的 `list`，删除所有元素 3。
- PR-22. 创建一个包含 1, 2, 3, 4, 5 元素的 `set`，插入 6，然后打印该 `set` 的元素。
- PR-23. 创建一个包含 1, 2, 3, 4, 5 元素的 `vector`，插入 6，然后打印该 `vector` 的元素。
- PR-24. 创建一个包含 1, 2, 3, 4, 5 元素的 `list`，插入 6，然后打印该 `list` 的元素。
- PR-25. 创建一个栈并向其推入 1, 2, 3, 4, 5，依次弹出所有元素并打印它们。
- PR-26. 创建一个队列并向其推入 1, 2, 3, 4, 5，依次弹出所有元素并打印它们。
- PR-27. 创建一个双端队列并在两端插入 1, 2, 3, 4, 5，依次从两端弹出所有元素。
- PR-28. 创建一个双端队列并在两端插入 1, 2, 3, 4, 5，依次从两端弹出所有元素。
- PR-29. 创建一个 `map` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，然后打印所有键。
- PR-30. 创建一个 `map` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，然后打印所有值。
- PR-31. 创建一个 `map` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，然后打印所有元素。
- PR-32. 创建一个 `set` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，然后打印所有键。
- PR-33. 创建一个 `set` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，然后打印所有值。
- PR-34. 创建一个 `set` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，然后打印所有元素。
- PR-35. 创建一个 `map` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，打印键 2 对应的值。
- PR-36. 创建一个 `map` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，打印值 "two" 对应的键。
- PR-37. 创建一个 `map` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，删除键 2 的元素。
- PR-38. 创建一个 `map` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，删除值为 "two" 的元素。
- PR-39. 创建一个 `map` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，删除所有元素。
- PR-40. 创建一个 `set` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，删除键 2。
- PR-41. 创建一个 `set` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，删除所有元素。
- PR-42. 创建一个 `set` 并向其插入元素对 (1, "one"), (2, "two"), (3, "three")，打印所有元素。

# 第 19 章 标准模板库 (STL)

| `const T max (const T& first, const T& second)` |

| `const T min (const T& first, const T& second)` |

**PRG-3.** 编写一个程序创建一个包含几个名称的 `vector`。打印这些名称，对名称进行排序，并打印排序后的名称。

**PRG-4.** 由于 `list`（链表）不支持随机访问迭代器，我们不能对 `list` 应用通用排序算法。然而，STL 库为 `list` 提供了自定义的排序操作。编写一个程序创建一个包含整数的 `list`，然后对该 `list` 进行排序。

**PRG-5.** 由于数组指针具有随机访问能力，我们可以对数组使用通用算法。创建一个包含 10 个字符的数组，然后对其进行排序并打印。

**PRG-6.** 编写一个程序创建一个包含 10 个元素的 `vector`，然后创建另一个 `vector`。仅将位置在 2 到 6 之间的元素复制到新 `vector` 中。打印这两个 `vector` 的元素。

**PRG-7.** 创建一个包含 10 个随机值的 `vector`，然后使用 *for_each* 和 *accumulate* 算法打印这些值以及它们的和。

**PRG-8.** 在 `vector` 中存储随机值的另一种方法是使用 *generate* 算法将函数的返回值赋值给公共容器的每个成员。编写一个程序，使用名为 *randGen* 的函数在 `vector` 中存储 10 个范围在 100 到 200 之间的随机值。

**PRG-9.** 使用 *min_element* 和 *max_element* 算法找到 `vector` 中的最小值和最大值。

**PRG-10.** 排序数组的一种方法是将数组转换为一个 `set`（集合），然后将该集合复制回数组。编写一个程序来实现此操作。

**PRG-11.** 程序 19.29 查找了两个集的*并集* (union)。设计一个程序寻找两个集的*交集* (intersection)。两个集的*交集*是一个仅包含两个集合公共元素的集合，如下：

![](img/ce9c99d45f71111839bc062830bd19fd_930_0.png)

**PRG-12.** 程序 19.29 查找了两个集的*并集*。设计一个程序寻找两个集的*差集* (difference)。我们可以有两个*集合差集*：第一个-第二个和第二个-第一个。第一个-第二个包含所有在第一个集合中不在第二个集合中的元素。第二个-第一个包含所有在第二个集合中不在第一个集合中的元素，如下：

![](img/ce9c99d45f71111839bc062830bd19fd_930_1.png)

**PRG-13.** 程序 19.29 查找了两个集的*并集*。设计一个程序寻找两个集的*对称差集* (symmetric difference)。两个集的*对称差集*包含存在于第一个或第二个集合中，但不同于两者中的元素。

![](img/ce9c99d45f71111839bc062830bd19fd_931_0.png)

**PRG-14.** 可以使用函数对象配合 *generate* 算法创建一个项列表，其中每个项都依赖于前一个。例如，我们可以使用一个名为 *Even* 的仿函数创建一个偶数列表。该仿函数返回前一个加 2。编写一个 *Even* 类，重载函数运算符 `operator`，然后使用 *generate* 算法创建一个前 10 个偶值的列表。

**PRG-15.** 适合作为函数对象的函数之一是斐波纳契序列。我们知道 $fib(n) = fib(n-1) + fib(n-2)$。换句话说，我们必须保留前两个项的值来计算新项。编写一个程序设计一个 *Fib* 类，并重载该类的函数运算符。然后使用该函数对象在 `vector` 中存储 11 个斐波纳契数：$fib(0)$ 到 $fib(10)$。

# 索引

## A

- `abs (...)`, 213
- 抽象类 (Abstract classes), 567
- 纯函数的声明, 568
- 纯函数的定义, 568
- 无实例 (without instance), 568
- 接口 (interface), 568
- Shape 类 (Shape Class), 568–579
- 访问修饰符 (Access modifiers), 279
- 用于数据成员 (for data members), 279–280
- 组修饰访问 (group modifier access), 280
- 用于实例数据 (for instance data), 294
- 用于实例成员 (for instance member), 295
- 用于成员函数 (for member functions), 280
- 访问器成员函数 (Accessor member function), 298
- 访问器和变变器 (Accessors and mutators), 320
- Accumulate 算法 (Accumulate algorithm), 909–910
- Ada, 7
