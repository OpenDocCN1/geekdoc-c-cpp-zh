
变量 x 会在每次迭代时从 values 数组中取得一个值。它将依次被赋值为 2、3、5 等。因此，循环最终会累加 values 数组中所有元素的总和。变量 x 是循环的局部变量，在循环外部不存在。

花括号初始化列表本身就是一个有效的范围，因此你可以将前面的代码写得更紧凑，如下所示：

```cpp
int total {};
for (int x : {2, 3, 5, 7, 11, 13, 17, 19, 23, 29})
    total += x;
```

当然，编译器知道 values 数组中元素的类型，因此你也可以让编译器来确定 x 的类型，把前面的循环写成这样：

```cpp
for (auto x : values)
    total += x;
```

使用 auto 关键字会让编译器推导出 x 的正确类型。auto 关键字经常与基于范围的 for 循环一起使用。这是遍历数组或其他范围中所有元素的一种很好的方式。你不需要知道元素的数量，循环机制会处理这一点。

注意，范围中的值会被赋给范围变量 x。这意味着你不能通过修改 x 的值来修改 values 的元素。例如，下面的代码不会改变 values 数组中的元素：

```cpp
for (auto x : values)
    x += 2;
```

这只是给局部变量 x 加 2，而不是给数组元素加 2。x 中存储的值会在下一次迭代时被 values 中下一个元素的值覆盖。在下一章中，你将学习如何通过使用引用变量在基于范围的 for 循环中修改值。

## while 循环

while 循环使用逻辑表达式来控制循环体的执行。图 5-3 展示了 while 循环的一般形式。

```cpp
// Output column headings
std::cout << std::format(table_format, "integer", "sum", "factorial");

unsigned int n {};
unsigned int sum {};
unsigned long long factorial {1ULL};

while (++n <= limit)
{
    sum += n;                         // Accumulate sum to current n
    factorial *= n;                   // Calculate n! for current n
    std::cout << std::format(table_format, n, sum, factorial);
}
```

该程序的输出与 Ex5_04.cpp 相同。变量 n、sum 和 factorial 在循环之前定义。这里变量的类型可以不同，因此 n 和 sum 定义为 unsigned int。factorial 中能存储的最大值有限，因此它保持为 unsigned long long 类型。由于计算方式的实现，计数器 n 初始化为零。while 循环条件先递增 n，然后将新值与 limit 比较。只要条件为真，循环就会继续，因此循环会以 n 从 1 到 limit 的值执行。当 n 达到 limit+1 时，循环结束。循环体内的语句与 Ex5_04.cpp 中相同。

> **注意**  任何 for 循环都可以写成等价的 while 循环，反之亦然。例如，for 循环具有以下通用形式：

```cpp
for (initialization; condition; iteration)
    body
```

这通常可以用 while 循环写成如下形式：

```cpp
{
    initialization;
    while (condition)
    {
        body
        iteration;
    }
}
```

while 循环需要用额外的一对花括号包围，以模拟原始 for 循环对初始化代码中声明的变量进行作用域限定的方式。

```cpp
// Make sure table size is within the limits
if (table < table_min || table > table_max)
{
    std::cout << "Invalid table size entered. Program terminated." << std::endl;
    return 1;
}

// Create the top line of the table
std::cout << std::format("{:>6}", '|');
for (size_t i {1}; i <= table; ++i)
{
    std::cout << std::format("{:3} |", i);
}
std::cout << std::endl;

// Create the separator row
for (size_t i {}; i <= table; ++i)
{
    std::cout << "------";
}
std::cout << std::endl;

for (size_t i {1}; i <= table; ++i)
{
    // Iterate over rows
    std::cout << std::format("{:3} |", i);       // Start the row

    // Output the values in a row
    for (size_t j {1}; j <= table; ++j)
    {
        std::cout << std::format("{:3} |", i*j); // For each column
    }
    std::cout << std::endl;                       // End the row
}

// Check if another table is required
std::cout << "\nDo you want another table (y or n)? ";
std::cin >> reply;

} while (std::tolower(reply) == 'y');
}
```

下面是输出示例：

```text
What size table would you like (2 to 12)? 4
     |  1 |  2 |  3 |  4 |
-----+----+----+----+----
  1  |  1 |  2 |  3 |  4 |
  2  |  2 |  4 |  6 |  8 |
  3  |  3 |  6 |  9 | 12 |
  4  |  4 |  8 | 12 | 16 |
```

## 跳过循环迭代

有时你会希望跳过一次循环迭代并继续下一次。continue 语句可以实现这一点：

```cpp
continue;      // Go to the next iteration
```

当该语句在循环中执行时，执行会立即转移到当前迭代的末尾。只要循环控制表达式允许，执行就会继续进入下一次迭代。通过一个例子最容易理解这一点。假设你想输出一张表，列出字符及其十六进制和十进制格式的字符编码。当然，你不希望输出没有图形表示的字符——其中一些字符（例如制表符和换行符）会打乱输出。因此，程序应该只输出可打印字符。代码如下：

```cpp
// Ex5_08.cpp
// Using the continue statement to display ASCII character codes
import <iostream>;
import <format>;
#include <cctype>

int main()
{
  const auto header_format = "{:^11}{:^11}{:^11}\n";     // 3 cols., 11 wide, centered (^)
  const auto body_format = "{:^11}{:0^11X}{:0^11d}\n";   // Print same argument three times

  std::cout << std::format(header_format, "Character", "Hexadecimal", "Decimal");

  // Output 7-bit ASCII characters and corresponding codes
  char ch{};
  do
  {
    if (!std::isprint(ch))  // If it's not printable...
      continue;             // ...skip this iteration
    std::cout << std::format(body_format, ch);
  } while (ch++ < 127);
}
```

这会显示一张便捷的表格，列出所有 95 个可打印 ASCII 字符的编码。你可能还记得第 1 章中讲过，ASCII 是一种 7 位编码，这意味着所有 ASCII 码值都位于 0 到 127 之间（包括两端）。

| 字符 | 十六进制 | 十进制 |
|---|---|---|
|  | 20 | 32 |
| ! | 21 | 33 |
| " | 22 | 34 |
| # | 23 | 35 |
| ⋮ |  |  |
| } | 7D | 125 |
| ~ | 7E | 126 |

main() 函数顶部的格式字符串用于生成一个包含三列的表格，每列宽度为 11，并且每列的值居中（由 ^ 对齐选项指定）。注意，即使表格有三列，我们也只向 do-while 循环中的 std::format() 表达式传入一个参数。在 body_format 中，我们使用位置参数标识符 0（位于列说明的左侧）将这个参数打印三次：一次作为字母，一次作为大写十六进制数（得益于 X 后缀），一次作为十进制数（得益于 d 后缀，该后缀可以省略，因为十进制输出是默认值）。

然而，这里有趣的部分当然是（有条件的）continue 语句。你不希望输出没有可打印表示的字符的详细信息。<cctype> 中声明的 isprint() 函数可以帮助做到这一点：它仅对可打印字符返回 true。因此，当 ch 包含不可打印字符的编码时，if 语句中的表达式将为 true。在这种情况下，continue 语句会执行，从而跳过当前循环迭代中剩余的代码。

值得注意的是，简单的 for 循环在这里并不适用。也就是说，对该程序循环的一个自然的第一尝试可能是这样的 for 循环：

```cpp
for (char ch {}; ch <= 127; ++ch)
{
    // Output character and code...
}
```

遗憾的是，在 char 为有符号类型的系统上，这个朴素的循环永远不会结束。毕竟，对于有符号 char，127 是可能的最大值，因此 ch <= 127 将始终为真。在原始的 do-while 循环中，条件是在循环体执行之后、递增 ch 之前检查的（得益于后置递增表达式）。然而，朴素 for 循环的条件是在循环体执行之前、递增 ch 之后检查的。

尽管如此，写出这样的 for 循环仍然非常诱人。相信我，在你的职业生涯中，你至少会掉进这个陷阱（或类似的陷阱）一次。所以要注意不要写出始终为真的停止条件！

你也可以让 for 循环正常工作：将控制变量使用 int 类型，然后在将其传给 std::format() 时把该值转换为 char 类型。

### 跳出循环

有时，你需要提前结束循环；循环语句中可能出现某种情况，表明继续执行没有意义。在这种情况下，你可以使用 break 语句。它在循环中的作用与在 switch 语句中大致相同：在循环中执行 break 语句会立即结束循环，执行将继续进行循环之后的语句。break 语句经常与无限循环一起使用，所以接下来我们看看其中一种循环是什么样子。

### 无限循环

无限循环可能会永远运行下去。省略 for 循环中的第二个控制表达式会得到一个可能执行无限次迭代的循环。必须在循环块本身内部以某种方式结束循环；否则，循环将无限重复。

无限循环有许多实际用途，例如监控某种报警指示器的程序，或从工业工厂中的传感器收集数据的程序。当你事先不知道需要多少次循环迭代时，例如在读取数量可变的输入数据时，无限循环会很有用。在这些情况下，你在循环块内编写退出循环的代码，而不是在循环控制表达式中编写。
