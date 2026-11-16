

## 9.4.7 带函数的乘法表

当我们上次在清单 7.5（bettertimestable.cpp）中访问我们的乘法表程序时，我们使用嵌套 for 循环来显示用户指定的大小。我们可以将代码分解为函数，如清单 9.8（timestablefunction.cpp）所示。我们的目标是拥有一组每个函数都非常简单的函数。我们还希望程序的整体结构在逻辑上井然有序。

```cpp
Listing 9.8: timestablefunction.cpp

#include <iostream>
#include <iomanip>

// Print the column labels for an n x n multiplication table.
void col_numbers(int n) {
    std::cout << "    ";
    for (int column = 1; column <= n; column++)
        std::cout << std::setw(4) << column; // Print heading for this column.
    std::cout << "\n";
}

// Print the table's horizontal line at the top of the table
// beneath the column labels.
void col_line(int n) {
    std::cout << "    +";
    for (int column = 1; column <= n; column++)
        std::cout << "----"; // Print separator for this row.
    std::cout << "\n";
}

// Print the title of each column across the top of the table
// including the line separator.
void col_header(int n) {
    // Print column titles
    col_numbers(n);
    // Print line separator
    col_line(n);
}

// Print the title that appears before each row of the table's
// body.
void row_header(int n) {
    std::cout << std::setw(4) << n << " |"; // Print row label.
}

// Print the line of text for row n
// This includes the row number and the
// contents of each row.
void print_row(int row, int columns) {
    row_header(row);
    for (int col = 1; col <= columns; col++) {
        std::cout << std::setw(4) << row*col; // Display product
    }
    std::cout << "\n"; // Move cursor to next row
}

// Print the body of the n x n multiplication table
void print_contents(int n) {
    for (int current_row = 1; current_row <= n; current_row++)
        print_row(current_row, n);
}

// Print a multiplication table of size n x n.
void timetable(int n) {
    // First, print column heading
    col_header(n);

    // Print table contents
    print_contents(n);
}

// Forces the user to enter an integer within a
// specified range first is either a minimum or maximum
// acceptable value last is the corresponding other end
// of the range, either a maximum or minimum value
// Returns an acceptable value from the user
int get_int_range(int first, int last) {
    // If the longer number is provided first,
    // switch the parameters
    if (first > last) {
        int temp = first;
        first = last;
        last = temp;
    }

    // Insist on values in the range first...last
    std::cout << "Please enter a value in the range "
              << first << "..." << last << ": ";
    int in_value; // User input value
    bool bad_entry;
    do {
        std::cin >> in_value;
        bad_entry = (in_value < first || in_value > last);
        if (bad_entry) {
            std::cout << in_value << " is not in the range "
                      << first << "..." << last << '\n';
            std::cout << "Please try again: ";
        }
    } while (bad_entry);

    // in_value at this point is guaranteed to be within range
    return in_value;
}

int main() {
    // Get table size from user; allow values in the
    // range 1...18.
    int size = get_int_range(1, 18);

    // Print a size x size multiplication table
    timetable(size);
}
```

图 9.5 当用户输入 3 以生成 3 x 3 乘法表时，清单 9.8（timestablefunction.cpp）中各函数激活的跟踪。时间从左向右流逝。水平条显示所涉及各函数的生命周期。

![](img/e84ad11adb18201d71595b31ce6c9eff_240_0.png)

在清单 9.8（timestablefunction.cpp）中，每个函数都扮演着非常特定的角色；例如，row_header 打印特定行的标签，然后打印将行标签与表格主体分隔开的垂直条。我们重用了清单 9.12（betterinput.cpp）中的 get_int_range 函数。请注意，程序中似乎不再有任何嵌套循环。嵌套循环并未真正消失，它现在被程序的函数组合所隐藏。请观察，print_contents 函数包含一个循环。每次循环时，它会调用 print_row，但 print_row 本身也包含一个循环。因此，嵌套迭代仍然存在。

现实地说，清单 9.8（timestablefunction.cpp）中的函数分解是极端的。程序的相对简单性并不能真正证明八个各自聚焦如此狭窄的独立函数是合理的；然而，更复杂的软件系统正是以这种方式进行分解的。清单 9.8（timestablefunction.cpp）不仅让我们了解如何将复杂问题分解为更简单、更易管理的部分，我们还可以使用该程序来更好地理解函数调用过程的工作原理。要了解这一点，请考虑用户希望使用清单 9.8（timestablefunction.cpp）打印 3 x 3 乘法表的情况。

在图 9.5 中，向下的箭头对应于函数调用。向下箭头上的标签表示调用期间传递的参数。向上的箭头表示从函数返回。向上箭头上的标签是函数的返回值。void 类型的函数在其返回箭头上没有标签。

图 9.5 中的每个水平条都表示函数处于活动状态时程序执行的持续时间。main 函数始终是 C++ 程序中首先执行的函数，在清单 9.8（timestablefunction.cpp）中，main 立即调用 get_int_range 函数。在 get_int_range 执行的生命周期内，请注意 main 仍然处于活动状态。这意味着它可能维护的任何局部变量仍然存储在内存中且未丢失其值。这意味着 main 的 value 变量在程序的有效生命周期内存在。对于 get_int_range 中使用的变量 temp、in_value、bad_entry 以及参数 first 和 last，情况并非如此。这些由 get_int_range 维护的变量在 get_int_range 开始执行时（其条形的左端）自动出现，并在 get_int_range 完成时（其条形的右端）释放其空间。在打印 3 x 3 表格期间，程序调用 print_row 三次，每次调用时，函数的参数 row 和 column 以及局部变量 col 都会产生，然后在函数返回时消失。

## 9.5 组织函数

迄今为止我们看到的代码在调用之前提供函数定义。清单 9.19（organization1.cpp）以这种方式组织其函数：

```cpp
Listing 9.19: organization1.cpp
// Function definition precedes main where the function is called
#include <iostream>

int twice(int n) {
    return 2 * n;
}

int main() {
    std::cout << twice(5) << '\n';
}
```

当编译器尝试解析以下语句时：

```
std::cout << twice(5) << '\n';
```

它需要能够确定表达式 twice(5) 在给定上下文中是否有效；也就是说，它必须确定表达式 twice(5) 求值结果是否可以使用 << 运算符发送到 std::cout 对象。在解析过程中，以下几点很重要：

- twice 函数的早期定义将标识符 twice 声明给编译器。因此，编译器期望调用 twice 的调用者传递一个与 int 类型兼容的单个参数。编译器还知道调用 twice 将返回一个整数值。
- 语句中 twice 名称后面的括号表示该表达式是一个函数调用。
- 括号内是整数字面量 5，它显然与 int 类型兼容。
- 因此，表达式 twice(5) 求值结果为 int，<< 运算符可以将整数值发送到 std::cout 输出流对象。

编译器可以验证 main 函数中的代码是否正确使用了 twice 函数。

如果我们将 twice 的定义放在 main 函数定义之后，编译器将在 main 中出现 twice 调用的位置报告错误。这是因为编译器在 .cpp 文件中从上到下逐行解析 C++ 源代码。当编译器首次在其

[1] 从技术上讲，运行时环境在局部变量的声明点之后才分配其空间。对于在块内声明的变量，例如 if 语句体中的 temp 变量，该变量在块执行结束时被丢弃。

