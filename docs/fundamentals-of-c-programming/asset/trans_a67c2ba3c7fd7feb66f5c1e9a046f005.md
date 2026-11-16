

一个名为 v 的向量和一个整数 i。除非 0 <= i < v.size()，否则表达式 v[i] 尝试访问向量边界之外的元素。operator[] 方法不执行边界检查；因此，使用表达式 v[i] 的执行程序将表示未定义行为。请考虑改用表达式 v.at(i)。at 方法的工作方式与 operator[] 相同，只是 at 会检查向量的边界。如果 i >= v.size() 或 i < 0，表达式 v.at(i) 表示一种异常情况，我们说向量的 at 方法抛出（或引发）一个异常。

不利用 C++ 的异常处理基础设施，以下语句：

```cpp
v.at(i) = 4;
```

可能会伴随错误消息终止程序。虽然这比未定义行为好，但并非理想。程序会崩溃。当真实应用程序崩溃时，用户可能会丢失未保存的数据。表现不佳的程序会意外终止。最好能防范越界索引并保持程序运行。

算法本身可以处理许多潜在问题。例如，程序员可以使用 if 语句来测试向量的索引是否在适当的边界内：

```cpp
if (0 <= i && i < v.size()) // Ensure i is in range
    v.at(i) = 4;
```

但是，如果程序员在给定函数或方法中的多个不同位置访问向量，并且索引变量可能因位置而异，那么为确保安全的向量访问所需的 if 语句数量可能会模糊函数或方法的整体逻辑。

## 22.2 异常示例

请参考清单 22.1 (vectorboundscrash.cpp)。每当用户输入等于向量 nums 范围之外的索引的值时，程序就会崩溃。

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<double> nums { 1.0, 2.0, 3.0 };
    int input;
    std::cout << "Enter an index: ";
    std::cin >> input;
    std::cout << nums.at(input) << '\n';
}
```

at 方法保证非法访问不会不被发现。为了在运行时拦截问题并防止程序因错误而终止，我们使用 try/catch 块，它由两部分组成：try 块和 catch 块。要形成 try/catch 块，我们

- 将可能抛出异常的代码包装在 try 块中，以及
- 在 catch 块中提供仅在发生异常时执行的代码。

清单 22.2 (vectorboundsexcept.cpp) 将异常处理代码添加到清单 22.1 (vectorboundscrash.cpp)。

### 清单 22.2: vectorboundsexcept.cpp

```cpp
#include <iostream>
#include <vector>

int main() {
  std::vector<double> nums { 1.0, 2.0, 3.0 };
  int input;
  std::cout << "Enter an index: ";
  std::cin >> input;
  try {
    std::cout << nums.at(input) << '\n';
  }
  catch (std::exception& e) {
    std::cout << e.what() << '\n';
  }
}
```

如果用户在执行清单 22.2 (vectorboundsexcept.cpp) 时输入小于零或大于二的值，程序将打印错误消息，并在技术上成功终止，而不是崩溃。

try 和 catch 都是 C++ 的关键字。与 if 和 while 等结构化语句的主体不同，try 块中的语句和 catch 块中的语句必须出现在花括号内，即使该部分只出现一条语句。

> 每个 try 块或 catch 块都必须用花括号包围其语句——即使它只包含一条语句。

清单 22.2 (vectorboundsexcept.cpp) 中 catch 块内的变量 e 是对异常对象的引用。exception 类是标准 C++ 库的一部分，是所有标准异常的基类。exception 类提供一个 what 方法，该方法返回一个字符串。exception::what 方法的字符串是一条包含异常信息的消息。C++ 标准未指定确切消息，但至少 exception::what 方法指示捕获的异常类型。以下显示当用户输入值 3 时，程序在 Visual C++ 下的报告内容：

```
Enter an index: 3
invalid std::vector<T> subscript
```

虽然清单 22.2 (vectorboundsexcept.cpp) 在技术上不会崩溃，但其行为与实际的异常程序终止并无太大区别。清单 22.3 (betterboundsexcept.cpp) 提供了一个更实用的示例。这个改进版本使用循环不断请求整数值，直到用户提供一个不会抛出异常的值为止。

### 清单 22.3: betterboundsexcept.cpp

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<double> nums { 1.0, 2.0, 3.0 };
    int input;
    while (true) {
        std::cout << "Enter an index: ";
        std::cin >> input;
        try {
            std::cout << nums.at(input) << '\n';
            break; // Printed successfully, so break out of loop
        }
        catch (std::exception&) {
            std::cout << "Index is out of range. Please try again.\n";
        }
    }
}
```

异常代码

```
try {
    std::cout << nums.at(input) << '\n';
}
catch (std::exception& e) {
    std::cout << e.what() << '\n';
}
```

比条件代码

```
if (0 <= input && input < nums.size()) {
    std::cout << nums.at(input) << '\n';
}
else {
    std::cout << "Vector out of bounds exception\n";
}
```

更好，这一点并非从这个简单示例中立即显而易见。要了解异常的真正能力，请参考清单 22.4 (callchainexception.cpp)。

### 清单 22.4: callchainexception.cpp

```cpp
#include <iostream>
#include <vector>
#include <string>
// Used to keep track of object creation and destruction
class Tracker {
    std::string name;
public:
    Tracker(const std::string& s): name(s) {
        std::cout << "Creating Tracker (" << name << ")\n";
    }
    ~Tracker() {
        std::cout << "Destroying Tracker (" << name << ")\n";
    }
};

bool find(const std::vector<int>& v, int lower, int upper) {
    std::cout << "-----<<[Entering find]-----<<\n";
    Tracker obj("find"); // Local tracking object
    bool result = false; // Not there by default
    int seek;
    std::cout << "Enter item to locate: ";
    std::cin >> seek;
    for (int i = lower; i < upper; i++) {
        if (v.at(i) == seek) {
            result = true; // Found it
            break;
        }
    }
    std::cout << "-----<<[Leaving find]-----<<\n";
    return result;
}

void process(const std::vector<int>& v) {
    std::cout << "-----<<[Entering process]-----<<\n";
    Tracker obj("process"); // Local tracking object
    int low, high;
    std::cout << "Enter a range: ";
    std::cin >> low >> high;
    if (find(v, low, high))
        std::cout << "Found it\n";
    else
        std::cout << "Not there\n";
    std::cout << "-----<<[Leaving process]-----<<\n";
}

// Global tracking object
Tracker obj("global");

int main() {
    std::cout << "-----<<[Entering main]-----<<\n";
    Tracker obj("main"); // Local tracking object
    std::vector<int> nums { 11, 42, 23 };
    try {
        process(nums);
    }
    catch (std::exception& e) {
        std::cout << "nums vector bounds exceeded\n";
    }
    std::cout << "-----<<[Leaving main]-----<<\n";
}
```

清单 22.4 (callchainexception.cpp) 是专门制作的，旨在深入了解程序的确切执行路径。每个函数在其开始和结束处都会打印一条消息，以便我们可以看到函数内的代码何时处于活动状态。每个函数还声明一个局部 Tracker 对象，该对象由该函数的名称标识。执行中的函数在声明点构造一个局部对象，并在函数返回给其调用者时自动销毁该对象。因此，这些局部对象的生命周期与管理它们的函数的生命周期相镜像。最后，清单 22.4 (callchainexception.cpp) 声明了一个全局 Tracker 对象。执行中的程序在调用 main 之前创建全局对象，并且

