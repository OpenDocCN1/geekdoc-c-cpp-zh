

## 3.1 常量与变量——内置数据类型、取值范围及初始化

基本类型的其他参数，如最小值、最大值、最低值等，可以通过 `numeric_limits< T >` 类（来自 `limits` 头文件）来确定，如清单 3.1 所示。

清单 3.1 显示 C++ 基本内置类型的值并测量其字节大小（摘自 CppBookCode，Variables.cpp）。

```cpp
#include <limits>    // for basic types' limits
using std::cout, std::endl, std::numeric_limits;

    // Print basic facts about char
cout << "bytes of char = " << sizeof( char )    << endl;
cout << "char lowest = "    << +numeric_limits< char >::lowest()    << endl;
cout << "char min = "    << +numeric_limits< char >::min()    << endl;
cout << "char max = "    << +numeric_limits< char >::max()    << endl;

    // Print basic facts about int
cout << "bytes of int = "    << sizeof( int )    << endl;
cout << "int lowest = "    << numeric_limits< int >::lowest()    << endl;
cout << "int min = "    << numeric_limits< int >::min()    << endl;
cout << "int max = "    << numeric_limits< int >::max()    << endl;
```

要使用 `numeric_limits`，我们需要包含 `limits` 头文件，如第 [1] 行所示。在第 [7-9] 行中，我们打印了 `char` 类型的 `lowest`、`min` 和 `max` 值。然而，为了正确显示这些值，我们在这里使用了一个小技巧：在 `numeric_limits` 对象前面加上一个 `+` 号。这会使这些值被当作整数处理，从而正确显示。

要存储一个值，我们需要检查所选表示法是否有足够的位数。在下面的示例中，我们只是询问 `long` 类型是否足以存储最多 11 位的数字。计算很简单，但需要调用 `log` 函数来返回自然对数的值，如清单 3.2 的第 [18] 行所示。关于 `long` 是否足够长的问题，其答案通过第 [18-19] 行的比较（`<`）得出。这个真或假的结果将赋给布尔变量 `longFitFlag`。

```cpp
    // Check whether long is long enough to store 11-digit values
const int bits_in_byte = 8;
bool longFitFlag = ( std::log( 9999999999.0 ) / std::log( 2.0 ) + 1 ) < sizeof( long ) * bits_in_byte - 1;
```

在第 [21] 行，根据标志 `longFitFlag` 的值显示一条消息。为了检查它，使用了条件 `? :` 运算符，其详细信息将在 GROUP 15（表 3.15）中介绍。最后，终端窗口中显示以下内容：

```
bytes of char = 1
char lowest = -128
char min = -128
char max = 127
bytes of int = 4
int lowest = -2147483648
int min = -2147483648
int max = 2147483647
We cannot store 11 digits in long in this system
```

我们看到，在这个系统中，`long` 不足以存储由 11 位数字组成的值。此外，我们需要非常小心，因为 `long` 表示有符号类型。也就是说，它可以存储正值和负值。这意味着需要一位用于符号表示。因此，在第 [19] 行中减去了 1。关于有符号和无符号类型之间的更多差异将在第 7.1.4 节中讨论。作为一种经验法则，如果没有特殊要求，应选择有符号整数，并且不应混合类型。

`wchar_t` 可用于存储各种国际字符。以下代码片段展示了如何创建和初始化一个宽字符，以及如何使用 `std::wstring` 对象来分配由宽字符组成的文本。

```cpp
wchar_t pl_letter = L'A';
wcout << pl_letter << L" needs " << sizeof( pl_letter ) << L" bytes." << endl;

std::wstring holiday_pl( L"święto" );

// We cannot use sizeof here - we need to call size()
size_t holiday_pl_len = holiday_pl.size();

std::wcout << holiday_pl << L" has " << holiday_pl_len << L" letters\n";
```

还要注意，要正确显示宽字符，我们需要使用 `std::wcout` 而不是 `std::cout`。此外，在某些平台上，我们需要调用平台特定的函数来正确显示国家字母。运行上述代码的结果如下：

```
A needs 2 bytes.
święto has 6 letters
```

最后，请注意宽文本字面量以前缀 `L` 开头。总之，如果我们编写的应用程序可以在国际市场中使用，从一开始就使用 `wchar_t`、`wstring`、`wcout` 等是一个不错的选择。我们将在本书后面的章节中看到示例。

## 要记住的事项

+   - 为对象（变量、常量、函数、类等）选择有意义且可读的名称（标识符）
+   - 选择合适的数据类型进行计算
+   - 优先选择有符号类型
+   - 始终初始化变量。对于零初始化，只需添加 `{ }` 即可

## 3.2 示例项目——收集学生成绩

到目前为止，我们已经看到了如何定义和使用不同类型单个变量和常量。然而，很多时候我们需要连续存储许多这样的对象。有时我们不知道需要多少个。为此，我们可以使用一种称为*向量*（或*数组*）的数据结构。³ 图 3.2 描绘了一个包含四个数值对象的向量。

**图 3.2** 向量由多个对象组成，它们在内存中占据连续空间。这里我们有 *N* = 4 个可以存储浮点数据的对象。可以通过提供索引来访问向量的每个单元。第一个元素位于索引 0，最后一个元素位于索引 *N* − 1。

首先，向量是一种具有以下特征的数据结构：

+   - 它包含相同类型的对象
+   - 对象在内存中密集排列，即一个接一个（没有空洞）
+   - 可以通过将*索引*提供给*下标运算符* `[ ]` 来访问向量中的每个对象。有效索引为 0 到 *N* − 1，其中 *N* 表示向量中元素的数量

在 C++ 中，创建向量的方法有很多种。最灵活的是使用 SL 库中的 `std::vector` 对象，它

+   - 可以在开始时为空
+   - 可以在新对象可用时附加到它们
+   - 包含许多有用的函数

在我们详细了解 `std::vector` 能为我们做什么之前，让我们从清单 3.3 中的一个简单示例程序开始。它的目的是收集学生成绩并计算其四舍五入的平均值。

> ³ 术语*数组*通常保留给固定大小的结构（第 3.10 节）；*向量*用于动态变化大小的对象。

清单 3.3 一个收集并计算学生平均成绩的程序（位于 *StudentGrades, main.cpp*）。

```cpp
#include <vector>       // A header to use std::vector
#include <iostream>     // Headers for input and output
#include <iomanip>      // and output formatting
#include <cmath>         // For math functions

// Introduce these, to write vector instead of std::vector
using std::cout, std::cin, std::endl, std::vector;

int main()
{
    cout << "Enter your grades" << endl;

    vector< double >   studentGradeVec; // An empty vector of doubles

    // Collect students' grades
    for( ; ; )
    {
        double grade {};

        cin >> grade;

        // If ok, push new grade at the end of the vector
        if( grade >= 2.0 && grade <= 5.0 )
            studentGradeVec.push_back( grade );

        cout << "Enter more? [y/n] ";
        char ans {};
        cin >> ans;

        if( ans == 'n' || ans == 'N' )
            break; // The way to exit the loop
    }
}
```

要使用 `std::vector` 并能够读写值，需要包含一些标准头文件，如第 [1-3] 行所示。然后，为了避免反复重复 `std::` 前缀，在第 [7] 行，借助 `using` 指令将 `std` 命名空间中的常用名称引入我们的作用域。我们已经知道 `main` 函数的作用，它从第 [10] 行开始：它定义了我们可执行的 C++ 程序。然后，核心部分是在第 [15] 行定义的向量对象。注意，要存储的对象类型需要放在 `< >` 括号中。为了能够存储对象，向量类通过模板机制以通用方式编写，这将在第 4.7 节中讨论。

然后，在第 [18] 行，`for` 循环开始（见第 3.13.2.2 节）。它的作用是收集用户输入的所有成绩。然而，我们不知道会输入多少个。因此，`for` 中没有条件：它会一直迭代，直到用户按下 `'n'`（在第 [33] 行检查）时到达第 [34] 行的 `break` 语句。

在每次迭代中，第 [20] 行创建了一个新的值为 0 的成绩，然后在第 [22] 行被用户输入的值覆盖。如果其值正确，即在 2.0 到 5.0 之间，则在第 [26] 行通过调用 `studentGradeVec` 的 `push_back` 成员函数将其推入向量对象的末尾。对象及其成员函数由点运算符（`.`）分隔——其语法将在第 3.9 节以及 *GROUP 2* 运算符（表 3.15）的描述中介绍。

