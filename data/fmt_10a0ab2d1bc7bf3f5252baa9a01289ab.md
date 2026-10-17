
```cpp
// 将客户/频道对加入 customers map

auto result = mCustomers.insert({ name, channels }); // 等，这里的 OCR 是一团糟，我将遵循提供的逻辑。

}
```

```cpp
void CableCompany::removeChannel(const string& name, int channel)
{
    // 查找客户的引用。
    auto it = mCustomers.find(name);
    if (it != end(mCustomers)) {
        // 我们找到了这个客户；移除通道。
        // 注意 'it' 是指向 name/bitset 对的引用。
        // bitset 是第二个字段。
        it->second.reset(channel);
    } else {
        throw invalid_argument("Unknown customer*");
    }
}

void CableCompany::addPackageToCustomer(const string& name, const string& package)
{
    // 查找包。
    auto itPack = mPackages.find(package);
    if (itPack == end(mPackages)) {
        // 该包不存在。抛出异常。
        throw out_of_range("Invalid package");
    }
    // 查找客户。
    auto itCust = mCustomers.find(name);
    if (itCust != end(mCustomers)) {
        // 将包按位或到客户现有的通道中。
        // 注意迭代器是指向 name/bitset 对的引用。
        // bitset 是第二个字段。
        itCust->second = itPack->second;
    } else {
        throw invalid_argument("Unknown customer*");
    }
}

void CableCompany::deleteCustomer(const string& name)
{
    // 删除此名称的客户
    mCustomers.erase(name);
}

bitset CableCompany::getChannels() const {
    // 查找客户
    auto it = mCustomers.find(name);
    if (it != end(mCustomers)) {
        // 找到了。
        // 注意 'it' 是指向 name/bitset 对的引用。
        // bitset 是第二个字段。
        return it->second;
    }
    // 没找到。抛出异常。
    throw invalid_argument("Unknown customer*");
}
```

最后，这里有一个演示如何使用 `CableCompany` 类的简单程序：

```
auto basic_pkg = "1111000000";
auto premium_pkg = "1111111111";
auto sports_pkg = "0000010011";
myCC.addPackage("basic", bitset<kNumChannels>(basic_pkg));
myCC.addPackage("premium", bitset<kNumChannels>(premium_pkg));
myCC.addPackage("sports", bitset<kNumChannels>(sports_pkg));
myCC.newCustomer("Marc G.", "sports");
myCC.addPackageToCustomer("Marc G.", "basic");
cout << myCC.getCustomerChannels("Marc G.") << endl;
```

## 总结

本章介绍了标准模板库容器。它展示了说明这些容器各种用途的示例代码。希望你能够体会 `vector`, `deque`, `list`, `forward_list`, `array`, `stack`, `queue`, `priority_queue`, `map`, `multimap`, `set`, `multiset`, `unordered_map`, `unordered_multimap`, `unordered_set`, `unordered_multiset`, `string` 和 `bitset` 的强大。即使你没有立即将它们整合到你的程序中，至少也要在未来的项目中记住它们。

现在你已经熟悉了这些容器，下一章将通过讨论通用算法来展示 STL 的真正威力。

# 17

# 精通 STL 算法

### 本章包含哪些内容？

- 算法解释
- Lambda 表达式解释
- 函数对象解释
- STL 算法的细节
- 一个更大的示例：审核选民注册

本章的 WROX.COM 下载

请注意，本章的所有代码示例可以在书籍网站 `www.wrox.com/go/proc++3e` 的“Download Code”选项卡中作为本章代码下载的一部分获取。

如第 16 节所示，STL 提供了一个令人印象深刻的通用数据结构集合。大多数库只步于此。然而， STL 还包含一组额外的通用算法，在某些例外情况下，这些算法可以应用于任何容器的元素。通过使用这些算法，你可以查找、排序和处理容器中的元素，并执行一系列其他操作。这些算法的妙之处在于，它们不仅不依赖于元素的类型，也不依赖于所操作容器的类型。STL 算法仅使用迭代器接口执行工作。

许多算法接受一个回调函数，该函数可以是函数指针或行为类似于函数指针的内容，例如重载了 `operator()` 的对象或内联 lambda 表达式。方便的是，STL 提供了一组可以用于创建算法回调对象的类。这些回调对象被称为函数对象，或称为仿函数（functors）。

# 算法概述

算法背后的“魔法”在于它们作用于迭代器中介，而不是容器本身。这样一来，它们就不会绑定到特定的容器实现上。所有的 STL 算法都实现为函数模板，其中模板参数通常是迭代器类型。迭代器本身作为参数传递给函数。模板函数可以将模板类型与函数解耦，因此你通常可以像调用普通函数一样调用算法，而不需要指定类型。

迭代器参数通常是迭代器范围。如第 16 节解释的那样，对于大多数容器，迭代器范围是半开的，包含第一个元素但不包含最后一个元素。

理解算法的最佳方法是看一些示例。在你看了几个示例之后，接下来的章节将描述 `find` 和 `find_if`。

# find 和 find_if

`find()` 在范围内查找特定元素。它返回指向找到元素的迭代器，如果未找到，则返回结束迭代器。

> 注意 如果 `find()` 未找到元素，它将返回范围的结束迭代器。

`find_if()` 与 `find()` 相似，但它接受一个谓词函数而不是简单的匹配元素。谓词返回真值或假值。

```cpp
#include <algorithm>
#include <vector>
#include <iostream>
using namespace std;

int main()
{
    int num;
    vector<int> myVector;
    while (true) {
        cout << "输入数字（输入 0 停止）：";
        cin >> num;
        if (num == 0) {
            break;
        }
        myVector.push_back(num);
    }
    while (true) {
        cout << "要查找数字（输入 0 停止）：";
        cin >> num;
        if (num == 0) {
            break;
        }
        auto endit = cend(myVector);
        auto it = find(cbegin(myVector), endit, num);
        if (it == endit) {
            cout << "未找到 " << num << endl;
        } else {
            cout << "找到了 " << it << endl;
        }
    }
    return 0;
}
```

带有 `myVector` 和 `endIt` 参数的 `find()` 调用，`endIt` 定义为 `cend(myVector)`，以便搜索 vector 的所有元素。如果你想搜索子范围，可以更改这些迭代器。

这里是程序的示例：

```
输入数字（输入 0 停止）：3
输入数字（输入 0 停止）：4
输入数字（输入 0 停止）：5
输入数字（输入 0 停止）：6
输入数字（输入 0 停止）：0
要查找数字（输入 0 停止）：5
找到了 5
要查找数字（输入 0 停止）：8
未找到 8
要查找数字（输入 0 停止）：0
```

某些容器（如 `map` 和 `set`）作为类方法提供了自己的 `find()` 版本。

> 注意 如果容器提供了与通用算法功能相同的方法，你应该使用该方法，因为它的更快。例如，`find()` 算法即使在 map 上也以线性时间复杂度运行的，而 map 的 `find()` 方法是以对数时间复杂度运行的。

对范围内的元素执行谓词操作，直到谓词返回 `true`，在这种情况下，`find_if()` 返回一个指向该元素的迭代器。以下程序从用户处读取分数，检查任何分数是否为“完美”。完美分是指 100 分或更高分。该程序与之前的示例相似。不同之处已高亮显示。

```cpp
bool perfectScore(int num) {
    return (num >= 100);
}
int main() {
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
    if (it == end)
        cout << "No perfect scores" << endl;
    } else {
        cout << "Found a perfect* score of " << *it << endl;
    }
    return 0;
}
```

此程序传递了一个指向 `perfectScore()` 函数的指针，`find_if()` 算法会在每个元素上调用该函数，直到它返回 `true`。这是使用 lambda 表达式的相同示例。它让你对 lambda 表达式的力量有一个初步了解。不要担心它们的语法；它们将在稍后的章节进行介绍。注意 `perfectScore()` 函数的缺失。

```cpp
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
auto it = find_if(cbegin(myVector), end, [](int i) { return i >= 100; });
if (it == end)
    cout << "No perfect scores" << endl;
} else {
    cout << "Found a perfect* score of " << *it << endl;
}
```

遗憾的是，STL 没有提供 `find_all()` 或等效算法来返回匹配谓词的所有实例。

# accumulate 算法

计算容器中所有元素的和或其他算术量通常是有用的。`accumulate()` 函数就是为此设计的。在它最基本的形式下，它计算指定范围内元素的和。例如，下面的代码计算 `vector` 中整数序列的平均值。平均值仅仅是所有元素的和除以元素的数量。

```cpp
#include <numeric>
#include <vector>
using namespace std;
double accumulateMean(const vector<int>& nums)
{
    double sum = accumulate(nums.begin(), nums.end(), 0);
    return sum / nums.size();
}
```

注意 `accumulate()` 是在 `<numeric>` 中声明的，而不是在 `<algorithm>`。`accumulate` 算法的第三个参数作为初始值，在这种情况下应该是 `0`，以开始新的求和。`accumulate()` 的另一种形式允许调用者指定要执行的操作而不是默认的加法。假设你想计算几何平均值，即序列的乘积，情况下你会使用 `accumulate()` 来计算乘积。你可以这样写：

```cpp
#include <numeric>
#include <vector>
#include <cmath>
using namespace std;
int product(int num1, int num2)
{
    return num1 * num2;
}
double geometricMean(const vector<int>& nums)
{
    double mult = accumulate(nums.begin(), nums.end(), 1, product);
    return pow(mult, 1.0 / nums.size());
}
```

lambda 表达式可以返回一个值。返回类型在箭头之后，称为尾返回类型。下面的示例定义了一个接受两个参数并返回和的 lambda 表达式：

```cpp
auto returningLambda = [](int a, int b) -> int { return a + b; };
int sum = returningLambda(11, 22);
```

如果省略返回类型，lambda 表达式会执行某些操作。在上一个示例中，根据与函数推导相同的规则省略返回类型：

```cpp
auto returningLambda = [](int a, int b) { return a + b; };
int sum = returningLambda(11, 22);
```

如果 lambda 表达式不接受任何参数，你可以指定空括号或直接省略它们。

lambda 表达式可以接受参数。参数在括号之间并用逗号分隔，就像普通函数一样。这里有一个单参数的示例：

```cpp
auto parametersLambda = 
[](int value) { cout << "The value is " << value << endl; };
parametersLambda(4);
```

lambda 可以捕获其封装作用域内的变量。对于该示例，下面的 lambda 表达式捕获了变量，以便在此中使用：

```cpp
double data = 1.23;
auto capturingLambda = [data]()cout << "Data " << data << endl;
```

方括号被称为捕获块。它允许你指定如何在 lambda 表达式的体内部捕获变量。指定空捕获块 `[]` 意味着不捕获封装作用域内的任何变量。当你像上一个示例那样在捕获块中写入变量名时，你是在按值捕获该变量。

编译器将 lambda 表达式转换为某种泛对象。第 14 节解释了什么是捕获。按值捕获的变量被拷贝到泛对象的数据成员中。这些数据成员的常量 属性与捕获的变量相同。在之前的 `capturingLambda` 中，泛对象获得了一个名为 `data` 的非常量数据成员，因为捕获的变量是非常量的。然而，在下面的示例中，泛对象获得了一个名为 `data` 的常量数据成员，因为捕获的变量是常量：

```cpp
const data = 1.23;
auto capturingLambda = [data]()cout << "Data " << data << endl;
```

泛对象有一个调用运算符。对于 lambda，此运算符默认标记为 `const`。这意味着即使你在 lambda 表达式中按值捕获非常量变量，lambda 表达式也无法修改副本。你可以通过如下指定 lambda 表达式将调用运算符标记为非常量：

```cpp
double data = 1.23;
auto capturingLambda = [mutable]()cout << "Data " << data << endl;
```

在这个示例中，非常量变量按值捕获，泛对象获得了一个名为 `data` 的非常量数据成员。由于 `mutable` 关键字，调用运算符被标记为非常量，因此 lambda 表达式的体可以修改其副本。注意，如果你指定了 `mutable`，即使参数为空也必须指定参数括号。

# LAMBDA 表达式
