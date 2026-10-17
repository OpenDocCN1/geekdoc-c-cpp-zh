
```cpp
void CableCompany::addPackage(const string& packageName,
    const bitset<kNumChannels>& channels)
{
    // 仅创建一个键值对并将其插入到 packages map 中。
    mPackages.insert({ packageName, channels });
}
void CableCustomer::removePackage(const string& packageName)
{
    // 仅从 package map 中删除该包。
    mPackages.erase(packageName);
}
void CableCustomer::newCustomer(const string& name, const string& package)
{
    // 获取指定包的引用。
    auto it = mPackages.find(package);
    if (it == end(mPackages)) {
        // 该包不存在。抛出异常。
        throw out_of_range("Invalid package*");
    }
    // 注意 'it' 指向一个名称/bitset 对。bitset 是
    // 第二个字段；
    auto result = mCustomers.insert({ name, it->second });
    if (!result.second) {
        // 如果客户已存在。
        // 注意：此处代码逻辑似乎与注释描述有出入，按逻辑翻译。
    }
}
```

# 算法概述

算法背后的“魔法”之处在于，它们作用于迭代器中间件，而不是作用于容器本身。这样，它们就不会依赖于特定的容器实现。所有的 STL 算法都被实现为函数模板，其中模板参数通常是迭代器类型。迭代器本身作为函数的参数传递。模板函数可以从参数推导出模板类型，因此你通常可以像调用普通函数一样调用算法，而不需要指定模板。

迭代器参数通常是随机迭代器。如第 16 节所示，对于大多数容器，迭代器范围是半开的，即包含范围内的第一个元素，但不包含最后一个元素。结束迭代器实际上是一个“越过结尾”的标记。

算法对传递给它的迭代器有特定的要求。例如，`copy_backward()` 是一个需要双向迭代器的算法示例，而 `stable_sort()` 是需要随机访问迭代器的算法示例。这意味着此类算法无法在不支持它们的容器上工作。`forward_list` 是一个仅支持正向迭代器的容器示例，不支持双向或随机访问迭代器，因此 `copy_backward()` 和 `stable_sort()` 无法在 `forward_list` 上工作。

大多数算法定义在 `<algorithm>` 头文件中，而一些数值算法定义在 `<numeric>` 中。它们都位于 `std` 命名空间中。

理解算法最好的方法是先看示例。在你看到几个示例的运行结果后，很容易上手其他的。本节详细描述了 `find()`、`find_if()` 和 `accumulate()` 算法。接下来的章节将介绍 Lambda 表达式和函数对象，并结合性性讨论每一类算法。

# find 和 find_if 算法

`find()` 在迭代器范围内查找特定元素。你可以在任何容器的元素上使用它。它返回一个指向找到的元素的迭代器；如果没有找到该元素，则返回结束迭代器。请注意，调用 `find()` 时指定的范围可能不是容器元素的全部范围；它可能是一个子集。

> 警告 如果 `find()` 未找到元素，它返回的是与函数调用中指定的结束迭代器相同的迭代器，而不是底层容器的结束迭代器。

这里是 `find()` 的示例。注意，此示例假设用户操作良好并输入有效内容；它没有对用户输入进行任何错误检查。对流输入的错误检查将在第 12 节中讨论。

```cpp
#include <algorithm>
#include <vector>
#include <iostream>
using namespace std;
int main()
{}
```

`int num;`

`vector<int> myVector;`

`while (true) {`

`cout << "Enter a number to add (0 to stop): ";`

`cin >> num;`

`if (num == 0) {`

`break;`

`}`

`myVector.push_back(num);`

`}`

`while (true) {`

`cout << "Enter a number to add (0 to stop): ";`

`cin >> num;`

`if (num == 0) {`

`break;`

`}`

`auto endit = cend(myVector);`

`auto it = find(cbegin(myVector), endit, num);`

`if (it == endit) {`

`cout << "Could not find " << num << endl;`

`} else {`

`cout << "Found " << it << endl;`

`}`

`}`

`return 0;`
```

对 `find()` 的调用使用了 `myVector` 和 `endIt` 作为参数，其中 `endIt` 定义为 `cend(myVector)`，以便搜索向量中的所有元素。如果你想在子范围内搜索，只需更改这些迭代器即可。

以下是程序的运行示例：

- Enter a number to add (0 to stop): 3
Enter a number to add (0 to stop): 4
Enter a number to add (0 to stop): 5
Enter a number to add (0 to stop): 6
Enter a number to add (0 to stop): 0
Enter a number to lookup (0 to stop): 5
Found 5
Enter a number to lookup (0 to stop): 8
Could not find 8
Enter a number to lookup (0 to stop): 0

某些容器（如 `map` 和 `set`）作为类方法提供了它们自己的 `find()` 版本。

> 警告 如果容器提供了一个与泛型算法功能相同的方法，你应该使用该方法，因为它的速度更快。例如，泛型 `find()` 算法以线性时间运行，即使在 `map` 上也是；而 `map` 的 `find()` 方法是以对数时间运行。

`find_if()` 与 `find()` 相似，不同在于它接受一个谓词函数回调，而不是简单的匹配元素。谓词返回真或假。`find_if()` 算法对范围内的每个元素调用谓词，直到谓词返回真，此时 `find_if()` 返回一个指向该元素的迭代器。以下程序从用户处读取测试分数，然后检查是否有任何分数是“完美”的。完美分是指 100 分或更高。该程序与之前的示例相似，不同之处已高亮显示。

```cpp
bool perfectScore(int num)
{
    return (num >= 100);
}

int main()
{
    int num;
    vector<int> myVector;
    while (true) {
        cout << "Enter a test score to add (0 to stop): ";
        cin >> num;
        if (num == 0) {
            break;
        }
        myVector.push_back(num);
    }
    auto end = cend(myVector);
    auto it = find_if(cbegin(myVector), end, perfectScore);
    if (it == end) {
        cout << "Could not find perfect score" << endl;
    } else {
        cout << "Found perfect score" << *it << endl;
    }
    return 0;
}
```

`find_if()` 算法对范围内的每个元素调用谓词，直到谓词返回真，此时 `find_if()` 返回一个指向该元素的迭代器。

```cpp
[] (int num1, int num2) { return num1 * num2; };
return pow(mult, 1.0 / nums.size());
}
```

在本章稍后的部分，你将学习如何在 `geometricMean()` 函数中使用 `accumulate`，而无需编写函数回调或 表达式。

## 算法中的移动语义

与 STL 容器一样，STL 算法也经过优化，会在适当的时候使用移动语义。这可以极大地提高某些算法的速度，例如 `sort()`。因此，强烈建议在你想要存储在容器中的自定义元素类中实现移动语义。通过实现移动构造函数和移动赋值运算符，可以为任何类添加移动语义。两者都应该标记为 `noexcept`，因为它们不应该抛出异常。请参阅第 10 章中的“移动语义”部分，了解如何向你的类添加移动语义。

## Lambda 表达式

Lambda 表达式允许你内联编写匿名函数，消除了编写单独函数或函数对象的需要。Lambda 表达式可以让代码更易读和理解。

## 语法

让我们从非常简单的 lambda 表达式开始。下面的示例定义了一个仅向控制台打印字符串的 lambda 表达式。Lambda 表达式以方括号 `[]` 开始，后面跟着大括号 `{}`，大括号包含 lambda 表达式的体。该 lambda 表达式被赋值给变量 `basicLambda-auto`。第二行使用普通的函数调用语法执行该 lambda 表达式。

```cpp
auto basicLambda = []() { cout << "Hello from Lambda" << endl; };
basicLambda();
```

输出如下：

Hello from Lambda

Lambda 表达式可以接受参数。参数在括号内并用逗号隔开，就像普通函数一样。这里有一个参数的示例：
```cpp
