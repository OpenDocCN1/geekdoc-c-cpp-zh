

# 列表 11.2: averagenumbers2.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    double sum = 0.0, num;
    const int NUMBER_OF_ENTRIES = 5;
    cout << "Please enter " << NUMBER_OF_ENTRIES
    cout << " numbers: ";
    for (int i = 0; i < NUMBER_OF_ENTRIES; i++) {
        cin >> num;
        sum += num;
    }
    cout << "The average of " << NUMBER_OF_ENTRIES << " values is " << sum/NUMBER_OF_ENTRIES << endl;
}
```

列表 11.2 (averagenumbers2.cpp) 的行为与列表 11.1 (averagenumbers.cpp) 不同，如下面使用数据的示例运行所示：

```
Please enter five numbers: 9 3.5 0.2 100 15.3
The average of the five is 25.6
```

列表 11.2 (averagenumbers2.cpp) 可以通过修改来更方便地处理 25 个值，而列表 11.1 (averagenumbers.cpp) 必须使用 25 个独立的变量——只需更改常量 NUMBER_OF_ENTRIES 即可。事实上，将代码更改为处理 1,000 个数字也没有那么困难。然而，与原始版本不同，这个新版本不会显示输入的数字。这是一个显著的区别；可能需要保留所有值以便使用户验证它们的正确性。

- 所有值都可以以不同的方式显示；例如，它们可以被放置在图形用户界面组件中，如视觉网格（电子表格）。
- 在输入所有值后，可能需要以不同的方式处理它们；例如，我们可能希望显示在某个值（大于0）之后输入的值，但在输入所有数字之前无法确定该限制。

在所有这些情况下，我们必须保留所有变量的值以便以后回溯。我们需要结合上述两个程序的优点；具体来说，我们需要：

- 保留单个值的能力，以及
- 无需创建独立变量存储所有单个值的能力

这些要求似乎是相互矛盾的，但 C++ 提供了几种标准数据结构，可以同时提供这两种优势。在本章中我们将检查这些结构中的两种：vector（向量）和数组（arrays）。

## 11.1 vectors（向量）

C++ 中的 vector 是一个管理内存块的对象，该内存块可以同时存放多个值；因此，vector 代表一个值的集合。vector 有一个名称，我们可以通过 vector 管理的内存块中的位置来访问它包含的值。vector 存储一个值序列，且所有值必须是相同类型。所有相同类型的集合被称为同质的（homogeneous）。

### 11.1.1 声明和使用 vector

为了在 C++ 程序中使用 vector 对象，你必须添加预处理器指令

```cpp
#include <vector>
```

vector 类型是标准 (std) 命名空间的一部分，因此它的完整名称是 `std::vector`，就像 `cout` 的完整名称是 `std::cout`（第 2.1 节）。如果你在源文件顶部包含

```cpp
using namespace std;
```

或者

```cpp
using std::vector;
```

你就可以在代码中使用较短的名称 vector。本章中的其余示例假设已使用了必要的 `using` 和 `std`，并使用了短名称 `vector`。

我们声明一个可以存放整数的 vector 对象非常简单：

```cpp
vector<int> vec_a;
```

类型角括号内可以是任何有效的 C++ 数据类型。当这样声明时，vector `vec_a` 初始为空。
我们如下所示声明一个具有特定初始大小的 vector：

```cpp
vector<int> vec_b(10);
```

在这里，`vec_b` 初始持有 10 个整数。所有 10 个元素默认均为 0。vector 的大小出现在 vector 名称后的括号内。
我们声明一个给定大小的 vector 对象并指定其所有元素的初始值：

```cpp
vector<int> vec_c(10, 8);
```

在这个示例中，`vec_c` 初始持有 10 个整数，值均为 8。vector 名称后括号中的第一个数字指定元素数量，第二个数字指定所有元素的初始值。
我们声明一个 vector 并单独指定每个元素：

```cpp
vector<int> vec_d{10, 20, 30, 40};
```

注意元素出现在大括号内，而不是括号内。大括号内的元素列表构建了一个 vector。这种声明仅对小型 vector 有实用意义。图 11.1 提供了 vector `vec_a`、`vec_b` 和 `vec_d` 的概念图。

```cpp
vector<int> vec_a;
vector<int> vec_b(10);
vector<int> vec_c(10, 8);
vector<int> vec_d{10, 20, 30, 40};
```

| vec_a | vec_b | vec_c | vec_d |
| :--- | :--- | :--- | :--- |
| 0 | 0 | 8 | 10 |
| 1 | 0 | 8 | 20 |
| 2 | 0 | 8 | 30 |
| 3 | 0 | 8 | 40 |
| 4 | 0 | 8 | |
| 5 | 0 | 8 | |
| 6 | 0 | 8 | |
| 7 | 0 | 8 | |
| 8 | 0 | 8 | |
| 9 | 0 | 8 | |

*(注：此处根据表格逻辑补全了原文中截断的表格行，以保持完整性)*
图 11.1：vector 的声明及其结果

*(注：原文提供的表格内容在输入中不完整，此处根据上下文逻辑进行了格式化对齐)*

