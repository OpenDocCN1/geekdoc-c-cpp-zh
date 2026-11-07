
## 指定前置条件、后置条件和断言

前置条件契约（expects）和后置条件契约（ensures）在函数原型中指定——它们列在函数签名之后、分号之前。例如，一个计算 double 值的实数（而非虚数）平方根的函数，期望其参数大于或等于零。你可以用 expects 前置条件契约来指定这一点：

```cpp
double squareRoot(double value)
    [[expects: value >= 0.0]];
```

如果函数定义同时充当函数原型，则前置条件和后置条件契约列在函数签名与开头的左花括号之间。

断言在函数体中以语句形式指定。例如，要断言一个整数考试分数在 0 到 100 的范围内，你会写：

```cpp
[[assert: grade >= 0 && grade <= 100]];
```

前面语句中的 assert 不是 assert 宏。

## 早期访问实现

GNU C++<sup>64</sup> 中有一个早期访问的契约实现，你可以通过 Compiler Explorer 网站<sup>65</sup>（https://godbolt.org）进行测试，该网站支持多种编程语言中的许多编译器版本。你可以选择 “x86-64 gcc (contracts)” 作为编译器，并使用以下位置描述的编译器选项来编译基于契约的代码：

```text
https://gitlab.com/lock3/gcc-new/-/wikis/contract-assertions
```

我们提供了一个 godbolt.org URL，你可以使用早期访问实现尝试我们的每个示例。GNU C++ 早期访问契约实现为前置条件和后置条件使用了不同的关键字：

- 用 pre 而不是 expects，以及
- 用 post 而不是 ensures。

## 示例：除以零

图 12.8 重新实现了图 12.3 中的 quotient 函数。这里，我们在 quotient 函数的原型中（第 5–6 行）指定了一个默认级别的前置条件契约，表明分母不得为 0.0。default 关键字也可以显式指定，如下所示：

```cpp
[[pre default: denominator != 0.0]]
```

此示例可在 https://godbolt.org/z/jn4MK3o9T 找到。

当你在 Compiler Explorer 编辑器中输入代码，或加载现有示例时，Compiler Explorer 会自动编译并运行它，或显示任何编译错误。

```cpp
// fig12_08.cpp
// quotient function with a contract precondition.
#include <iostream>

double quotient(double numerator, double denominator)
  [[pre: denominator != 0.0]];

int main() {
  std::cout << "quotient(100, 7): " << quotient(100, 7)
            << "\nquotient(100, 0): " << quotient(100, 0) << '\n';
}

// perform division
double quotient(double numerator, double denominator) {
  return numerator / denominator;
}
```

**图 12.8** 带契约前置条件的 quotient 函数。

我们为此示例预设的编译器选项为

`-std=c++20 -fcontracts`

它会使用 C++20 和实验性契约支持编译代码。Compiler Explorer 通常至少显示两个标签页——代码编辑器和编译器。我们的示例还显示输出标签页，以便你能看到已执行程序的结果——编译错误也会在此处显示。编译器标签页顶部有两个下拉列表。一个用于选择编译器。另一个用于查看和编辑编译器选项，或者你可以单击向下箭头选择常用编译器选项。

第 9 行的 quotient 调用满足前置条件并成功执行，产生：

```text
quotient(100, 7): 14.2857
```

然而，第 10 行的 quotient 调用会导致**契约违反**。因此，**默认违反处理程序（handle_contract_violation）**被隐式调用，显示以下错误消息，然后终止程序：

```text
default std::handle_contract_violation called:
./example.cpp 6 quotient denominator != 0.0 default default 0
```

将编译选项改为

`-std=c++2a -fcontracts -fcontract-build-level=off`

会禁用契约检查，并允许第 10 行执行，产生输出

```text
quotient(100, 0): inf
```

除以零在 C++ 中是未定义行为，但许多编译器——包括本书通篇使用的三个主要编译器——在这种情况下会返回正无穷（inf）或负无穷（-inf）。这是 IEEE 754 浮点运算标准所规定的行为，现代编程语言广泛支持该标准。

## 契约继续模式

契约违反的默认继续模式是立即终止程序。要允许程序继续执行，可以添加编译器选项

`-fcontract-continuation-mode=on`

## 示例：需要已排序 vector 的搜索函数

考虑图 12.9，它定义了一个带有两个前置条件的 binarySearch 函数模板——参数必须包含元素，并且必须已排序。你可以在以下地址测试该示例：

https://godbolt.org/z/obMSY5Wo4

在此示例中，我们在 main 之前定义函数，并将前置条件放在参数列表之后、函数体之前。

```cpp
// fig12_09.cpp
// binarySearch function with a precondition requiring a sorted vector.
#include <algorithm>
#include <iostream>
#include <vector>

template<typename T>
int binarySearch(const std::vector<T>& items, const T& key)
   [[pre: items.size() > 0]]
   [[pre: audit: std::is_sorted(items.begin(), items.end())]] {
   size_t low{0}; // low index of elements to search
   size_t high{items.size() - 1}; // high index
   size_t middle{(low + high + 1) / 2}; // middle element
   int loc{-1}; // key's index; -1 if not found

  do { // loop to search for element
    // if the element is found at the middle
    if (key == items[middle]) {
      loc = middle; // loc is the current middle
    }
    else if (key < items[middle]) { // middle is too high
      high = middle - 1; // eliminate the higher half
    }
    else { // middle element is too low
      low = middle + 1; // eliminate the lower half
    }

    middle = (low + high + 1) / 2; // recalculate the middle
  } while ((low <= high) && (loc == -1));

  return loc; // return location of key
}

int main() {
  // sorted vector v1 satisfies binarySearch's sorted vector precondition
  std::vector v1{10, 20, 30, 40, 50, 60, 70, 80, 90};
  int result1{binarySearch(v1, 70)};
  std::cout << "70 was " << (result1 != -1 ? "" : "not ")
      << "found in v1\n";

  // unsorted vector v2 violates binarySearch's sorted vector precondition
  std::vector v2{60, 70, 80, 90, 10, 20, 30, 40, 50};
  int result2{binarySearch(v2, 60)};
  std::cout << "60 was " << (result2 != -1 ? "" : "not ")
      << "found in v2\n";
}
```

**图 12.9** | 带前置条件和后置条件的 binarySearch 函数。

binarySearch 函数模板对 vector 执行二分搜索，这要求 vector 处于已排序顺序；否则结果可能不正确。我们的实现还要求 vector 包含元素。因此我们声明了以下前置条件：

```cpp
[[pre: items.size() > 0]]
[[pre audit: is_sorted(begin(items), end(items))]]
```

第一个确保 vector 包含元素。第二个调用 C++ 标准库函数 is_sorted（来自头文件 `<algorithm>`<sup>66</sup>）来检查 vector 是否已排序。这可能是一个开销很大的操作。对十亿个元素的有序 vector 进行二分搜索只需要 30 次比较。然而，确定 vector 是否已排序需要 999,999,999 次比较。而使用高效排序算法对十亿个元素排序可能需要约 300 亿次操作。开发者可能希望在开发期间启用此测试，并在生产代码中禁用它。因此，我们指定了前置条件契约级别 audit。

64. 还有一个早期访问的 Clang 契约实现，位于 https://github.com/arcosuc3m/clang-contracts，但你需要自行构建并安装它。

65. 版权所有 © 2012-2019，Compiler Explorer Authors。保留所有权利。Compiler Explorer 由 Matt Godbolt 开发。https://xania.org/MattGodbolt.

66. C++ 标准库的 `<algorithm>` 头文件中有 200 多个函数。我们将在第 14 章概述其中许多函数。
