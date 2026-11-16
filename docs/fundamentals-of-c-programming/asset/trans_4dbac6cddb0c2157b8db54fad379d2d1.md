

清单 22.11 (rethrow.cpp) 产生以下输出：

```
************************************************
* For loop terminated prematurely
*   when i = 5
************************************************
Caught an exception: invalid std::vector<T> subscript
Program finished
```

请注意，在清单 22.11 (rethrow.cpp) 中，compute 函数不会创建新的异常对象；它只是重新抛出它捕获的同一个异常对象。中间异常处理程序的概念很重要，因为函数调用对其自身的本地上下文（例如其局部变量）有完整了解。这意味着调用链中的中间函数（或方法）可以访问该调用链中所有其他函数（或方法）可能无法获取的信息。清单 22.11 (rethrow.cpp) 中 compute 函数的 `catch` 块仅涉及局部变量。`main` 函数中的 `catch` 块无法知道导致 compute 失败的下标，因为 `i` 是 `compute` 的局部变量。一些通用的异常准则包括：

- 尽可能在抛出异常的代码附近（沿调用链向上）处理异常。
- 在适用的情况下，使用本地信息在该本地上下文中尽可能纠正问题：
  - 可用于从异常情况中恢复的本地信息是可用的；调用链上方的函数或方法无法获取此本地信息。
  - 容易发生异常的较低级别函数/方法可能由许多不同的较高级别函数/方法调用。如果较低级别函数/方法负责自身的异常处理，则较高级别函数/方法可能完全可以省略异常处理，从而使较低级别方法成为更健壮的复用单元。
  - 较低级别函数/方法可能处理多种不同类型的异常，根据抛出的异常类型执行它们能进行的任何本地清理，然后向较高级别方法抛出不同类型的异常。较高级别方法可能只需知道出现了问题，而不需要知道问题究竟是什么。例如，在清单 22.11 (rethrow.cpp) 中，compute 函数可以在每次 filter 抛出其 `std::out_of_range` 时抛出自定义 ComputeException 对象，而不仅仅是将其接收到的 `std::out_of_range` 对象沿调用链向上传递。

如果在调用链的较低级别无法或不希望完全恢复，则重新抛出异常，以便调用链上方的异常处理程序可以采取措施，以其上下文中合理的方式从问题中恢复。

当一段代码抛出异常时，最近异常处理程序中的 `catch` 块将按照它们在 C++ 源代码中出现的顺序进行检查。第一个与抛出的异常类型匹配的 `catch` 块将被执行。例如，清单 22.12 (multipleexceptions.cpp) 预期两种类型的异常，并使用捕获全部异常来应对可能出现的任何意外异常。

## 清单 22.12: multipleexceptions.cpp

```cpp
#include <vector>
#include <string>

// Get an integer from the user. Note that std::stoi can
// throw a std::invalid_argument exception if the user's
// input is not an integer, and it can throw std::out_of_range
// if the string is a valid integer but outside the range of
// a C++ int on this platform.
int get_int() {
    std::string input;
    std::cin >> input;
    int result = stoi(input);
    return result;
}

int main() {
    std::vector<int> a { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 };
    try { // What possibly could go wrong?
        int n = a.size();
        std::cout << "Enter index in the range 0..." << n - 1 << ": ";
        // Will user enter a valid integer value?
        int i = get_int();
        std::cout << "Index entered: " << i << '\n';
        // Will the user's index be in the range of valid indices?
        std::cout << "a[" << i << "] = a[" << i << "] = " << a.at(i) << '\n';
    }
    catch (std::out_of_range&) {
        std::cout << "Index provided is out of range\n";
    }
    catch (std::invalid_argument&) {
        std::cout << "Index provided is not an integer\n";
    }
    catch (...) { // What have we forgotten?
        std::cout << "Unknown error\n";
    }
}
```

捕获异常后，其类型首先与 `std::out_of_range` 进行比较。如果匹配，则执行 `std::out_of_range` catch 块。如果不匹配，则将异常的类型与 `invalid_argument` 进行比较。在匹配的情况下，将执行 `invalid_argument` catch 块。如果这两种类型都不匹配，则执行捕获全部代码。

当涉及继承时，情况变得更加有趣。每个 `catch` 块中执行的比较是 _赋值兼容性_ 测试。派生类实例的引用或指针可以赋值给声明为基类引用或指针的变量。由于派生类与其基类之间存在 _是一种_ 关系，这种向上转型操作始终合法。这意味着类型为 `std::out_of_range` 的异常对象与 `std::out_of_range` 变量和 `std::exception` 变量均具有赋值兼容性。由于 `catch` 块按照它们在源代码中出现的顺序进行检查，以下代码会出现问题：

```cpp
try {
    // Execute some code that can throw an
    // out_of_range exception
    ...
}
catch (std::exception& e) {
    // Do something here
}
catch (std::out_of_range& e) { // Error, this can never be reached
    // Do something else here
}
```

`std::out_of_range` catch 块永远不会执行，因为 `std::out_of_range` 对象本身也是一个异常实例。出于此原因，在 catch 块序列中，更具体的类型跟在更一般的类型之后是非法的。上述代码片段在任何上下文中都无法编译。因此，在 catch 块序列中，先列出更具体的异常，然后再列出更一般的异常。

所有 C++ 标准异常类都以 `std::exception` 作为其直接或间接基类。C++ 不要求异常对象派生自 `exception`；事实上，`int` 和 `char` 等原始类型也可以被抛出和捕获。出于此原因，“捕获全部”异常子句是

```
catch (...) {
    // Catches any exceptions not caught by more specific
    // catch blocks in this try/catch block
}
```

省略号 (...) 代表任何类型的异常。

任何函数或方法都可以抛出异常对象。给定类型 E 的异常，执行此操作的语句是：

```
throw E();
```

## 22.6 使用异常

异常应保留用于不常见的错误。例如，以下代码将名为 vec 的整数向量中的所有元素相加：

```
int sum = 0, n = vec.size();
for (int i = 0; i < n; i++) {
    sum += vec[i];
}
std::cout << "Sum = " << sum << '\n';
```

这个循环相当典型。另一种方法是使用异常：

```
sum = 0;
int i = 0;
try {
    while (true) {
        sum += vec.at(i++);
    }
} catch (std::out_of_range&) {}
std::cout << "Sum = " << sum << '\n';
```

两种方法都计算出相同的结果。第二种方法在数组访问越界时终止循环。它在语句

```
sum += vec.at(i++);
```

的中途中断，因此不会错误地修改 sum 的值。然而，第二种方法 _总是_ 抛出并捕获异常。异常绝对 **不是** 不常见的情况。

你不应使用异常来控制正常的逻辑流。虽然异常机制对其预定用途非常有用，但它会给程序执行增加一些开销，尤其是在抛出异常时。当异常很少时，这种开销是合理的；但当异常是程序正常执行的一部分时，则不合理。

有时不清楚何时适合使用异常。考虑一个返回向量中元素位置的函数。不使用异常的直接方法可以写成：

```
int find(const std::vector<int>& a, int elem) {
    int n = a.size();
    for (int i = 0; i < n; i++)
        if (a[i] == elem)
            return i; // Found it at position i
    return -1; // Element not present
}
```

这里返回值 -1 表示所查找的元素在数组中不存在。如果元素不存在，是否应该抛出异常？以下代码说明了这一点：

```
int find(const std::vector<int>& a, int elem) {
    int n = a.size();
    for (int i = 0; i < n; i++)
        if (a[i] == elem)
            return i; // Found it at position i
    // Element not there; throw an exception
    throw ElementNotPresentException();
}
```

在第一种方法中，粗心的程序员可能不检查结果，并盲目地将 -1 用作有效位置。异常代码不会允许这种情况发生。然而，第一种方法对于确定元素是否存在于向量中很有用。如果 find(x) 返回 -1，则 x 不在向量中；否则，它在向量中。如果使用异常方法，客户端程序员在没有抛出异常风险的情况下无法确定元素是否存在。由于异常应很少见，第二种方法似乎不太理想。总之，

- 第一种方法更有用，但客户端需要记住正确检查结果。
- 第二种方法提供了异常安全网，但在查找缺失元素时总会抛出异常。

哪种方法最终更好？第一个版本使用常见的编程惯用法，是大多数编程场景下更好的方法。异常版本是较差的选择，因为尝试查找向量中缺失的元素并不罕见；异常应保留用于不常见的错误情况。

