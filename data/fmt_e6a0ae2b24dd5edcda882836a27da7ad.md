
`cout << gt.comparisons << " " << comparisons << " "`

`cout << gt.swaps << " " << swaps << " " << endl;`

}

*注：原文文本包含大量重复和 OCR 错误。以上内容已根据提供的 C++ 代码逻辑进行了清理和结构化翻译。*

## 19.2. 异常示例

事件，并且程序应该将其作为正常处理的一部分进行处理。

异常几乎总是代表问题，通常是某种运行时错误。假设我们有一个 `vector` `v` 和一个整数 `i`。除非 `0 <= i < v.size()`，否则表达式 `v[i]` 会尝试访问 `vector` 的外部元素。`[]` 运算符不执行边界检查；因此使用表达式 `v[i]` 执行程序可能会产生未定义行为。相反考虑表达式 `v.at(i)`。该方法的作用与 `operator[]` 相同，不同之处它会检查 `vector` 的边界。如果 `i >= v.size()` 或 `i < 0`，表达式 `v.at(i)` 表示一个异常情况，我们说 `vector` 方法抛出 `throws` 或引发 `raises` 了一个异常。

在没有 C++ 异常处理机制的情况下，以下语句：

```
v.at(i) = 4;
```

可能会带有错误消息终止程序。这比产生未定义行为要好，但它并不理想。程序会崩溃。当真实应用程序崩溃时，用户可能会丢失数据。行为不佳的程序会意外终止。如果能防御越界索引并保持程序运行，将会更好。

算法可以帮助解决许多潜在问题。例如，程序员可以使用 `if` 语句来查看 `vector` 的索引是否在适当的范围内：

```
if (0 < i && i < v.size()) // 确保 i 在范围内
v.at(i) = 4;
```

然而，如果程序在函数的多个不同位置访问 `vector`，且索引变量会随位置而变化，那么为了确保安全访问所需的 `if` 语句可能会忽略函数或方法的整体逻辑。

## 19.2 异常示例

> 注意！该章节正在建设中

考虑列表 19.1 `vectorboundscrash.cpp`。每当用户输入超出 `vector` `nums` 范围的索引时，程序就会崩溃。

列表 19.1: `vectorboundscrash.cpp`
```cpp
#include <iostream>
#include <vector>
using namespace std;
int main() {
    vector<double> nums { 1.0, 2.0, 3.0 };
    int input;
    cout << "Enter index: ";
    cin >> input;
    cout << nums.at(input) << endl;
}
```

该方法保证了非法访问不会被遗漏。为了及时拦截问题并防止程序因错误而终止，我们使用 `try/catch` 块，它由两部分组成：`try` 块和 `catch` 块。为了形成 `try/catch` 块，我们：

1. 将可能抛出异常的代码被封装在 `try` 块中，
2. 在 `catch` 块中提供仅在发生异常时才执行的代码。

列表 19.2 `vectorboundexcept.cpp` 为列表 19.1 `vectorboundscrash.cpp` 添加了异常处理代码。

列表 19.2: `vectorboundexcept.cpp`
```cpp
#include <iostream>
#include <vector>
using namespace std;
int main() {
    vector<double> nums = {1.0, 2.0, 3.0};
    int input;
    cout << "Enter an index: ";
    cin >> input;
    try {
        cout << nums.at(input) << endl;
    } catch (exception& e) {
        cout << e.what() << endl;
    }
}
```

当用户在执行列表 19.2 `vectorboundexcept.cpp` 时输入小于零或大于二的值时，程序将打印错误消息并成功终止，而不是崩溃。

`try` 和 `catch` 都是 C++ 中的关键字。与 `if` 和 `while` 等结构语句的体不同，`try` 块中的语句和 `catch` 块中的语句必须用大括号出现，即使该部分只有一个语句。

> 每一个 `try` 或 `catch` 块都必须用大括号包裹其语句——即使它只包含一条语句。

列表 19.2 `vectorboundexcept.cpp` 中 `catch` 块中的变量 `e` 是异常对象的引用。异常类是标准 C++ 库的一部分，是所有异常的基类。异常类提供了一个返回字符串的方法。`exception::what` 方法的字符串是一个包含有关异常信息的消息。C++ 标准没有指定具体的消息，但至少 `exception::what` 方法指示了捕获到的异常类型。以下显示了当用户输入值 3 时，程序在 Visual C++ 下的内容：

```
Enter an index: 3
invalid vector<T> subscript
```

使得异常代码

```cpp
try {
    cout << nums.at(input) << endl;
}
catch (exception& e) {
    cout << e.what() << endl;
}
```

比条件代码

```
if (0 < input && input < nums.size()) {
    cout << nums.at(input) << endl;
} else {
    cout << "Vector out of bounds exception" << endl;
}
```

更好的原因从这个简单的示例中显而易见。要看到异常的真实能力，考虑列表 19.3 `callexception.cpp`。

### 列表 19.3: `callexception.cpp`
```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;
// 用于跟踪对象的创建和析毁
class Tracker {
    string name;
public:
    Tracker(const string& s) : name(s) {
        cout << "Creating Tracker " << name << endl;
    }
    ~Tracker() {
        cout << "Destroying Tracker " << name << endl;
    }
};
bool find(const vector<int>& vec, int lower, int upper) {
    cout << "---find------" << endl;
    Tracker obj("find"); // 本地对象
    bool result = false; // 默认
    int seek;
    // 要查找什么
    cout << "Enter item to locate: ";
    cin >> seek;
    for (int i = lower; i < upper; i++) {
        if (vec.at(i) == seek) {
            result = true;
            break;
        }
    }
    cout << "---find------" << endl;
    return result;
}
void process(const vector<int>& v) {
    cout << "---process----" << endl;
    Tracker obj("process"); // 本地对象
    int low, high;
    cout << "Enter a range: ";
    cin >> low >> high;
    if (find(v, low, high))
        cout << "Found it" << endl;
    else
        cout << "Not there" << endl;
    cout << "---process----" << endl;
}
int main() {
    cout << "---main----" << endl;
    Tracker obj("main"); // 全局对象
    vector<int> nums = {11, 42, 23};
    try {
        process(nums);
    } catch (const exception& e) {
        cout << "nums bounds exceeded" << endl;
        cout << "---main----" << endl;
    }
}
```

列表 19.3 `callexception.cpp` 专门为提供程序执行的洞察而设计的。每个函数在开始和结束时打印一条消息，以便我们看到函数内部代码何时处于激活。每个函数还声明了一个本地对象，该对象通过函数名称识别，并在函数返回调用者时自动析毁对象。然而，这些本地对象的生命周期与它们管理的函数生命周期镜像。列表 19.3 `callexception.cpp` 声明了一个全局 `Tracker`。执行的函数在调用 `main` 之前创建全局对象，并在 `main` 完成后自动析毁它们。

列表 19.3 `callexception.cpp` 涵盖了 `main` 中声明的 `vector` `nums`。在调用期间，`main` 函数无法控制 `process` 函数尝试访问范围之外元素的尝试。然而，`process` 函数并没有访问 `main` 提供的 `vector` 内的任何元素。相反，`process` 将 `vector` 传递给 `find` 函数。是在 `find` 中在越界索引调用了 `at` 方法，这将抛出一个异常。与 19.2 `vectorexception.cpp` 不同，调用 `vector<int>::at` 的方法不在 `try/catch` 块内。这意味着 `find` 无法捕获 `vector<int>::at` 可能抛出的任何异常。

以下是列表 19.3 `callexception.cpp` 的示例运行。

```
Creating Tracker (global)
---main----
Creating Tracker (main)
---process----
Creating Tracker (process)
Enter a range: 0 2
---find------
Creating Tracker (find)
Enter item to locate: 4
---find------
Destroying Tracker (find)
Not there
---process----
Destroying Tracker (process)
---main----
Destroying Tracker (main)
Destroying Tracker (global)
```

在列表 19.3 `callexception.cpp` 的输出中，我们看到了以下序列：

1. 程序创建全局对象。
2. 程序调用 `main`。
3. `main` 函数创建其对象。
4. `main` 调用 `process`。
5. `process` 函数创建其对象。
6. `process` 函数获取用户的范围值输入。这里用户输入的范围是 0..2。
7. `process` 调用 `find`。
8. `find` 创建其对象。
9. `find` 函数获取用户的元素输入。这里用户输入 4 `vector` 中不存在。
10. `find` 执行其最后语句。
11. 当 `find` 返回到 `process` 时，程序析毁其本地对象。
12. `process` 使用 `find` 的结果打印元素不在 `vector` 中的消息。
13. `process` 函数执行其最后语句。
14. 当 `process` 返回到 `main` 时，程序析毁其本地对象。
15. `main` 函数执行其最后语句。
16. 当 `main` 返回时，程序析毁其本地对象。
17. 程序终止，它析毁全局对象。

19.1 提供了 `process` 更图形化的表示。在这种情况下，用户在 `process` 函数中没有输入会导致 `find` 产生问题的范围，因此没有产生异常。程序的执行没有产生异常，它没有执行 `catch` 块中的打印语句。

要查看异常发生时发生了什么，请考虑列表 19.3 `callexception.cpp` 的以下示例运行。

## 19.2. 异常示例

![](img/e326304bd50fbc4f7d5a64c1487eb635_543_0.png)

图 19.1：没有异常的函数调用链。`vector<int>::at` 方法、`find` 函数和 `process` 函数完成了它们的所有工作，并像常一样返回给它们的调用者。

```
Creating Tracker (global)
------[Entering main]------
Creating Tracker (main)
------[Entering process]------
Creating Tracker (process)
Enter a range: 10 20
------[Entering find]------
Creating Tracker (find)
Enter item to locate: 4
Destroying Tracker (find)
Destroying Tracker (process)
nums vector bounds exceeded
------[Leaving main]------
Destroying Tracker (main)
Destroying Tracker (global)
```

提供的 10..20 范围超出了 `main` 的 `nums` `vector` 的边界。由于程序没有打印 `find` 消息，我们知道 `find` 函数没有像通常那样完成执行。这是因为 `find` 调用的 `vector<int>::at` 方法抛出了异常。此外，`find` 似乎没有正常返回，因为 `process` 没有打印它的退出消息。然而，我们确实看到程序正确地销毁了 `find` 和 `process` 拥有的本地 `Tracker` 对象。程序的执行路径立即返回到 `main`，我们看到它在执行完 `catch` 块中的语句后正常退出。程序通过销毁 `main::Tracker` 对象，然后销毁全局 `Tracker` 对象来结束。见图 19-2。

©2014 Richard L. Halterman

草案日期：2014年1月26日

## 19.2. 异常示例

更好地说明了程序的执行情况。

## 程序执行时间线

![](img/e326304bd50fbc4f7d5a64c1487eb635_544_0.png)

图 19.2：被异常中断的函数调用。`vector<int>::at` 方法、`find` 函数或 `process` 函数都没有完成它们的工作并像常一样返回给其调用者。控制权传回调用链中的 `catch` 块。

列表 19.3 `callexception.cpp` 证明了异常具有从根本上改变正常调用和返回路径的可能。某种意义上，异常的作用就像一个“超级 goto”语句。程序的执行跳转到执行序列中之前的某个点，跳过了调用链中的所有函数。回想第 6.3.2 节，它建议除了退出嵌套循环外，不要使用 `goto` 语句。在这些代码中，使用 `goto` 代替超结构化的分支和循环结构 `if/else`, `switch`, `while` 和 `for` 会导致代码变得难以扩展和维护。C++ 的异常机制在几个重要方面与“超级 goto”不同：

- `goto` 语句不能跳转到其所在函数代码之外。异常则没有这种限制。
- 程序员必须为 `goto` 语句指定目标 `标签`。`vector<int>::at` 方法抛出异常。我们可以在单个程序内的许多不同函数调用 `at`，并在许多程序中使用 `at`。方法内部的代码在遇到异常情况时不可能知道该去哪里。异常简单地将程序的执行重定向到调用链中可以处理该异常的最近 `try/catch` 块。

列表 19.4 `strboundexcept.cpp` 如下。

| Listing 19.4 | `strboundexcept.cpp` |
| :--- | :--- |
| `#include <iostream>` | ©2014 Richard L. Halterman |
| `#include <string>` | 草案日期：2014年1月26日 |

## 19.2. 异常示例

```cpp
#include <iostream>
#include <string>
using namespace std;
int main() {
    string s = "Wow";
    try {
        cout << s.at(3) << endl;
    } catch (exception& e) {
        cout << e.what() << endl;
    }
}
```

列表 19.5: `filereadexcept.cpp` `filereadexcept.cpp` 如下。

## 19.5: `filereadexcept.cpp`
