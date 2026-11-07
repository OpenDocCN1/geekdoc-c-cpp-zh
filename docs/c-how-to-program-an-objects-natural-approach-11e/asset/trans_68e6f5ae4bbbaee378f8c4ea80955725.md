
## ✓ **检查点**

- 1. *(填空题)* 参数 `std::begin(colors)` 和 `std::end(colors)` 返回的迭代器分别表示 colors 数组的开头和结尾。  
  **答案：** 迭代器。
- 2. *(对/错)* 标准库函数 `binary_search`（来自头文件 `<algorithm>`）可以判断某个值是否位于已排序数组中。  
  **答案：** 对。
- 3. *(对/错)* 对未排序数组执行 `binary_search` 是一种语法错误，可能导致不正确的结果。  
  **答案：** 错。实际上，对未排序数组执行二分查找是一种逻辑错误，可能导致不正确的结果。

## 6.13 多维数组

你可以使用二维数组（即具有两个索引的数组）来表示按行和列排列的数据表。要标识表中的特定元素，必须指定两个索引。按照惯例，第一个索引标识行，第二个索引标识列。需要两个索引来标识特定元素的数组称为二维数组，或称 **2-D 数组**。具有两个或更多维度的数组称为多维数组。下图展示了一个名为 `a` 的二维数组：

![](img/7b5e2088e71c7f78681d4ddbcf104c06_337_0.png)

该数组包含三行四列，因此称为 3×4 数组。通常，具有 *m* 行和 *n* 列的数组称为 *m*×*n* 数组。

在上图中，我们用 `a[row][column]` 形式的元素名称标识了每个元素。类似地，你可以通过赋值 `a.at(i).at(j)` 访问每个元素。

第 0 行中的所有元素名称的第一个索引均为 0；第 3 列中的所有元素名称的第二个索引均为 3。

图 6.10 演示了在声明中初始化二维数组。第 11–12 行各自创建一个包含两行三列的数组的数组。

```cpp
// fig06_10.cpp
// Initializing multidimensional arrays.
#include <iostream>
#include <array>

constexpr size_t rows{2};
constexpr size_t columns{3};
void printArray(const std::array<std::array<int, columns>, rows>& a);

int main() {
   constexpr std::array values1{std::array{1, 2, 3}, std::array{4, 5, 6}};
   constexpr std::array values2{std::array{1, 2, 3}, std::array{4, 5, 0}};

   std::cout << "values1 by row:\n";
   printArray(values1);

   std::cout << "\nvalues2 by row:\n";
   printArray(values2);
}

// output array with two rows and three columns
void printArray(const std::array<std::array<int, columns>, rows>& a) {
   // loop through array
   for (const auto& row : a) {
      // loop through columns of current row
      for (const auto& element : row) {
         std::cout << element << ' ';
      }

      std::cout << '\n'; // start new line of output
   }
}
```

```text
values1 by row:
1 2 3
4 5 6

values2 by row:
1 2 3
4 5 0
```

图 6.10 | 初始化多维数组。

### 声明数组的数组

在第 11–12 行中，编译器推断 `values1` 和 `values2` 是数组的数组，具有两行、每行三列，并且其中的元素类型为 `int`。考虑 `values1` 的两个初始化器：

```cpp
std::array{1, 2, 3};
std::array{4, 5, 6};
```

根据这些初始化器，编译器推断 `values1` 有两行。每个初始化器创建一个包含三个元素的数组，因此编译器推断 `values1` 的每一行有三列。最后，这些行初始化器中的值是 `int`，因此编译器推断 `values1` 的元素类型为 `int`。

### 显示数组的数组

程序调用函数 `printArray` 输出每个数组的元素。函数原型（第 8 行）和定义（第 22–32 行）指明，`printArray` 通过 `const` 引用接收一个两行三列、元素为 `int` 的数组。在类型

```cpp
const std::array<std::array<int, columns>, rows>&
```

中，外层数组类型表明它具有 `rows`（2）个元素，元素类型为

```cpp
array<int, columns>
```

因此，外层数组的每个元素都是一个包含 `columns`（3）个元素的 `int` 数组。该参数以 `const` 引用接收数组，因为 `printArray` 不会修改元素。

### 嵌套的基于范围的 for 语句

为了处理二维数组的元素，我们使用了嵌套循环：

- 外层循环遍历各行，并且
- 内层循环遍历给定行的各列。

函数 `printArray` 的嵌套循环使用基于范围的 `for` 语句实现。第 24 和 26 行引入了 `auto` 关键字，它告诉编译器根据变量的初始化器值推断（确定）变量的数据类型。外层循环的范围变量 `row` 用参数 `a` 中的一个元素初始化。查看数组的声明可以看到，它包含的元素类型为

```cpp
array<int, columns>
```

因此编译器推断 `row` 指代一个包含三个 `int` 值的数组（同样，`columns` 为 3）。`row` 声明中的 `const&` 表明该引用不能用于修改行，并防止每一行被复制到范围变量中。内层循环的范围变量 `element` 用 `row` 所表示数组中的一个元素初始化。因此，编译器推断 `element` 是对 `const int` 的引用，因为每一行包含三个 `int` 值。在许多 IDE 中，将鼠标光标悬停在用 `auto` 声明的变量上会显示该变量的推断类型。第 27 行显示给定行和列中的元素值。

### 嵌套的计数控制 for 语句

我们也可以用计数器控制的迭代实现嵌套循环，如下所示：

```cpp
for (size_t row{0}; row < a.size(); ++row) {
    for (size_t column{0}; column < a.at(row).size(); ++column) {
        cout << a.at(row).at(column) << ' '; // or a[row][column]
    }
    cout << '\n';
}
```

