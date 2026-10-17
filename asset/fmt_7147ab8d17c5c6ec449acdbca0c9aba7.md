
```cpp
DisplayContents(vecNames);
cout << "Searching for \"John\" using 'binary_search':" << endl;
bool elementFound = binary_search(vecNames.begin(), vecNames.end(), 
                                 "John");

if (elementFound)
    cout << "Result: \"John\" was found in the vector!" << endl;
else
    cout << "Element not found " << endl;
// 删除重复项
auto newEnd = unique(vecNames.begin(), vecNames.end());
vecNames.erase(newEnd, vecNames.end());
cout << "The contents of the vector after using 'unique':" << endl;
DisplayContents(vecNames);
return 0;
```

# 输出

vector 的初始内容为：

John

jack

sean

Anna

jack

排序后的 vector 包含名称顺序：

Anna

John

jack

jack

sean

使用 'binary_search' 查找 "John":

Result: "John" was found in the vector!

使用 'unique' 之后 vector 的内容为：

Anna

John

jack

sean

# 分析

前面的代码对第 26 行的示例 vector `vecNames` 进行了排序，然后在第 30 行使用 `binary_search()` 在其中查找 "John"。同样，在第 39 行使用 `std::unique()` 来删除相邻重复项的第二次出现。注意，`unique()` 像 `remove()` 一样不会调整容器的大小。它会导致值的移动，但不会减少元素的总数。为了确保容器末尾没有意外的未知值，请务必始终在调用 `unique()` 之后紧跟使用 `unique()` 返回的迭代器调用 `vector::erase()`，如第 40 行所示。

| 像 `binary_search()` 这样的算法仅在排序后的容器中有效。 | 在未排序的 vector 上使用此算法可能会导致不可预期的后果 |

## 注意

`stable_sort()` 的用法与你之前看到的 `sort()` 相同。`stable_sort()` 确保排序后的元素的相对顺序得以保持。保持相对顺序是以性能为代价的——这是一个需要考虑的因素，特别是当元素的相对顺序并非本质要求时。

# Note

# 划分范围

`std::partition()` 有助于将输入范围划分为部分：一个满足一元谓词，另一个不满足。

```cpp
bool IsEven(const int& num) // 一元谓词
{
    return ((num % 2) == 0);
}
npartition(numsInVec.begin(), numsInVec.end(), IsEven);
```

然而，`std::partition()` 不保证每个分区内元素的相对顺序。为了在重要时保持相对顺序，你应该使用 `std::stable_partition()`：

`stable_partition(numsInVec.begin(), numsInVec.end(), IsEven);`

列表 23.11 展示了这些算法的使用。

列表 23.11 使用 partition() 和 stable_partition() 将整数范围划分为偶数和奇数值

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
```

![](img/ccb6520e9d7dbb1b25f5e4ac7152a7c5_614_0.png)

# 课程 23：STL 算法

```cpp
3: using namespace std;
4:
5: bool isEven(const int& num) // 一元谓词
6:
7:     return ((num % 2) == 0);
8: }
9:
10: template <typename T>
11: void DisplayContents(const T& container)
12: {
13:     for (auto element = container.begin();
14:         element != container.end();
15:             ++element)
16:             cout << element << endl;
17: }
```

# 输出

John

jack

sean

Anna

jack

排序后的 vector 包含名称顺序：

Anna

John

jack

jack

sean

使用 'binary_search' 查找 "John":

Result: "John" was found in the vector!

输出：

Anna

John

jack

sean

## 分析

代码将整数范围划分为偶值和奇值。这种划分首先在第 31 行使用 `partition()` 完成，然后使用 `stable_partition()` 完成。`partition()` 的影响体现在元素的相对顺序上。`stable_partition()` 比 `partition()` 慢，因此只有当元素的相对顺序很重要时才应该使用它。

# 在排序集合中插入元素

在排序集合中以正确的位置插入元素很重要。STL 提供了如 `lower_bound()` 和 `upper_bound()` 这样的函数来帮助满足这一需求而不破坏顺序。

```cpp
auto minPos = lower_bound(names.begin(), names.end(), "Brad");
// 或者
auto maxPos = upper_bound(names.begin(), names.end(), "Brad");
```

因此，`lower_bound()` 和 `upper_bound()` 返回排序范围内可以破坏顺序插入元素的最小和最大位置的迭代器。

列表 23.12 展示了使用 `lower_bound()` 在 names 的最小位置插入元素。

列表 23.12 使用 lower_bound() 和 upper_bound() 在排序集合中插入

```cpp
0: #include <algorithm>
1: #include <list>
2: #include <string>
3: #include <iostream>
4: using namespace std;
5:
6: template <typename T>
7: void DisplayContents(const T& container)
8: {
9:   for (auto element = container.begin();
10:    element != container.end();
11:     ++element)
12:    cout << element << endl;
13: }
14: }
15: int main ()
16: {
17:  list<string> names {"John", "Brad", "jack", "sean", "Anna"};
18:
19:  cout << "Sorted contents of the list are: " << endl;
20:  names.sort();
21:  DisplayContents(names);
22:
23:  cout << "Lowest index where \"Brad\" can be inserted is: " << endl;
24:  auto minPos = lower_bound(names.begin(), names.end(), "Brad");
25:  cout << distance(names.begin(), minPos) << endl;
26:
27:  cout << "Highest index where \"Brad\" can be inserted is: " << endl;
28:  auto maxPos = upper_bound(names.begin(), names.end(), "Brad");
29:  cout << distance(names.begin(), maxPos) << endl;
30:
31:  cout << endl;
32:
33:  cout << "List after inserting Brad in sorted order: " << endl;
34:  names.insert(minPos, "Brad");
35:  DisplayContents(names);
36:
37:  return 0;
38: }
```

## 分析

元素可以插入到排序集合中的两个潜在位置：一个由 `lower_bound()` 返回，它是最低的（最接近集合起始位置的）；另一个是由 `upper_bound()` 返回的迭代器，它是最高的（距离集合起始位置最远的位置）。在列表 23.12 中，插入到排序集合的字符串 "Brad" 已经存在于其中，因此其下界和上界是不同的（否则，它们将是相同的）。这些函数的用法分别在第 24 行和第 29 行所示。如输出所示，当将 `lower_bound()` 返回的迭代器用于第 35 行所示将字符串插入列表时，结果是列表保持其排序状态。因此，这些算法可以帮助你在集合的某一点进行插入，而不会破坏内容的有序性。使用由 `upper_bound()` 返回的迭代器同样可以正常工作。

| 应当 (DO) | 避免 (DON'T) |

|---|-|

| 在使用 `remove()`、`remove_if()` 或 `unique()` 算法后，记得使用容器的 `erase()` 方法来调整容器大小。 | 不要忘记在调用 `unique()` 移除相邻重复值之前对容器进行排序。`sort()` 将确保所有相同值的元素都相邻排列，从而使 `unique()` 有效。 |

| 在使用 `find()`、`find_if()`、`search()` 或 `search_n()` 函数返回的迭代器之前，始终通过与容器的 `end()` 比较来检查其有效性。 | 不要向随机选择的位置向排序容器插入元素，而应使用 `lower_bound()` 或 `upper_bound()` 返回的位置进行插入，以确保元素的排序顺序不受干扰。 |

| 仅当排序元素的相对顺序很重要时，才选择 `stable_partition()` 而非 `sort()`，因为 `stable_*` 版本可能会降低应用程序性能。 | 不要忘记 `binary_search()` 仅用于排序容器。 |

## 总结

在本节中，你学习了 STL 算法中最重要且最强大的方面之一。你对不同类型的算法有了深入了解，并且示例应该让你对算法的应用有更清晰的理解。

## 问答

问：我是否会在像 `std::set` 这样的关联容器上使用如 `std::transform()` 这样的变异算法？

答：即使可行，也不应该这样做。关联容器的内容应被视为常量。这是因为关联容器在插入时会对元素进行排序，且元素的相对位置在 `find()` 等函数中起着重要作用，并影响容器的效率。出于这个原因，不应在 STL 集合上使用 `std::transform()` 这样的变异算法。

问：我需要将顺序容器中每个元素的内容设置为特定值。我可以用 `std::transform()` 来完成这项任务吗？

答：虽然可以使用 `std::transform()` 完成此任务，但 `fill()` 或 `fill_n()` 更适合该任务。

问：`copy_backward()` 会反转目标容器中元素的内容吗？

答：不会。STL 算法 `copy_backward()` 反转的是元素复制的顺序，而不是元素存储的顺序；也就是说，它从范围末尾开始到达顶部。要反转集合的内容，你应该使用 `std::reverse()`。

问：我应该在列表上使用 `std::sort()` 吗？

答：`std::sort()` 在列表上的使用方式与在任何顺序容器上的使用方式是相同的。然而，列表需要维持一个特殊属性，即对列表的操作不会使现有的迭代器失效——`std::sort()` 无法保证维持这一属性。因此，STL 列表以成员函数 `list::sort()` 的形式提供了 `sort()`，应该使用它，因为它保证了即使元素在列表中的相对位置发生了变化，指向这些元素的迭代器也不会失效。

问：为什么向排序范围插入元素时，使用 `lower_bound()` 或 `upper_bound()` 等函数很重要？

答：这些函数分别提供了第一个和最后一个位置，在这些位置上可以将元素插入到排序集合中而不破坏排序。

## 工作坊

工作坊包含测验题，帮助你巩固对所涵盖内容的理解，并提供了练习以让你获得所学知识的。在检查附录 E 中的答案之前，尝试回答测验和练习题，并在进入下一节之前确保你理解了答案。

## 测验

- 1. 你需要从列表中移除符合特定条件的项。你会使用 `std::remove_if()` 还是 `list::remove_if()`？

- 2. 你有一个类类型为 `ContactItem` 的列表。`list::sort()` 函数如何在指定的二元谓词中对该类型的项进行排序？

- 3. `generate()` STL 算法调用 `generator()` 函数的频率是多少？

- 4. `std::transform()` 与 `std::for_each()` 的区别是什么？

## 练习

- 1. 编写一个二元谓词，接受字符串作为输入参数并根据不区分大小写的比较返回结果。

- 2.  STL 算法（如 `copy()`）如何使用迭代器执行功能，而无需知道目标容器的性质（通过在两个不同容器的两个序列之间进行复制来实现）。

- 3. 你正在编写一个应用程序，按照升起的顺序记录出现在地平线的星星特征。在天文中，星星的大小以及它们相对升落序列的信息都非常重要。如果你根据大小对这些恒星集合进行排序，你会使用 `std::sort` 还是 `std::stable_sort`？

要创建一个使用不同底层容器的栈，请使用 `std::stack<double, vector<double>> doublesStackedInVec;`。

列表 24.1 展示了不同的实例化技术。

# 列表 24.1 STL 栈的实例化

```
0: #include <stack>
1: #include <vector>
2:
3: int main ()
4: {
5:     using namespace std;
6:
7:     // 一个整数栈
8:     stack<int> numsInStack;
9:
10:    // 一个双精度浮栈
11:    stack<double> dblInStack;
12:
13:    // 一个包含 vector 中的双精度浮栈
14:    stack<double, vector<double>> doublesStackedInVec;
15:
16:    // 初始化一个栈为另一个栈的拷贝
17:    stack<int> numsInStackCopy(numsInStack);
18:
19:    return 0;
20: }
```

# 分析

该示例没有输出，但演示了 STL 栈的模板实例化。第 8 行和第 11 行分别实例化两个存储 `int` 和 `double` 类型元素的栈对象。第 14 行也实例化了一个双精度浮栈，但指定了第二个模板参数——栈内部应该使用的容器类类型，即 `vector`。如果未提供此模板参数，栈将自动默认为 `std::deque`。最后，第 17 行演示了一个栈对象可以作为另一个栈的拷贝进行构造。

# 栈成员函数

栈适配其他容器（如 `deque`、`list` 或 `vector`），通过限制插入或删除元素的方式来实现功能，从而提供严格符合栈机制的行为。表 24.1 解释了 `stack` 类的公共成员函数，并演示了它们在整数栈中的用法。

# 表 24.1 std::stack 成员函数

| 函数 | 描述 |

| --- | --- |

| push() | 在栈顶插入一个元素 `numsInStack.push(25);` |

| pop() | 移除栈顶元素 `numsInStack.pop();` |

| empty() | 测试栈是否为空；返回 bool `if (numsInStack.empty()) DoSomething();` |

| size() | 返回栈中元素的数量 `size_t = numsInStack.size();` |

| top() | 获取栈中顶层元素的引用 `cout << "Element at the top = " << numsInStack.top();` |

表格表明，`stack` 的公共成员函数仅暴露允许在符合栈行为的位置进行插入和删除的方法。尽管底层容器可能是 `deque`、`vector` 或 `list`，但该容器本身的功能并未被暴露，以强制栈的行为特性。

# 使用 push() 和 pop() 在栈顶进行插入和删除

元素的插入通过成员方法 `stack<T>::push()` 完成：

`numsInStack.push(25); // 25 位于栈顶`

根据定义，栈允许通过成员函数 `top()` 访问顶部的元素：

```
cout << numsInStack.top() << endl;
```
