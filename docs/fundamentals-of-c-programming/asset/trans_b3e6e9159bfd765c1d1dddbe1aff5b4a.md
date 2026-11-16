
### 图 7.1 while 和 do/while 循环的流程图

![](img/e84ad11adb18201d71595b31ce6c9eff_177_0.png)

```
// Insist on values in the range 0...10
do
  std::cin >> in_value;
while (in_value < 0 || in_value > 10);
// in_value at this point is guaranteed to be within range
std::cout << "Legal value entered was " << in_value << '\n';
}
```

请注意，无需初始化 in_value，因为在通过输入流 std::cin 赋值之前不会使用其值。图 7.1 比较了 while 循环和 do/while 循环的流程图。

do/while 语句的一般形式如下：

```
do
statement
while ( condition );
```

- 保留字 do 和 while 用于标识 do/while 语句。do 和 while 关键字界定循环体，但如果循环体包含多条语句，仍然需要花括号。

- 条件与循环末尾的 while 相关联。条件是一个布尔表达式，必须用括号括起来。

- 该语句与 while 循环一般形式中的语句完全相同（参见第 6.1 节）。它可以是用花括号括起来的复合语句。

与 while 语句不同，do/while 语句的循环体保证至少执行一次。

do/while 循环为程序员提供了便利，并不是一种必不可少的编程结构。将任何使用 do/while 语句的代码转换为使用 while 语句且行为相同的代码都很容易。在实践中，程序员使用 while 循环的频率远高于 do/while 循环，因为更多算法需要顶部检查循环而非底部检查循环。然而，do/while 语句被包含在 C++ 中是有原因的。将能够更自然地用底部检查循环表达的算法转换为使用顶部检查循环，可能会导致笨拙的代码。在合适的时候使用 do/while。

## 7.4 for 语句

回顾清单 6.2 (iterativecountfive.cpp)。它只是从 1 数到 5。计数是计算机程序中经常执行的活动。任何程序要进行计数，都需要某些程序元素：

- 必须使用一个变量来跟踪计数；在清单 6.2 (iterativecountfive.cpp) 中，count 是命名恰当的计数器变量。
- 必须为计数器变量赋予初始值。在清单 6.2 (iterativecountfive.cpp) 的情况下，初始值为 1。
- 随着程序计数，必须修改变量（通常是递增）。语句 count++; 在清单 6.2 (iterativecountfive.cpp) 中递增 count。
- 必须提供一种方法来确定计数是否完成。在清单 6.2 (iterativecountfive.cpp) 中，while 语句的条件决定计数是否完成或必须继续。

C++ 提供了一种专门的循环，将这四个编程元素封装到一个方便的语句中。称为 for 语句，其一般形式是

```
for ( initialization ; condition ; modification ) statement
```

- 保留字 `for` 用于标识 `for` 语句。
- 循环由一个称为循环变量的特殊变量控制。
- 头部包含在括号中，包含三个部分，每个部分由分号分隔：
  - **初始化。** `initialization` 部分为循环变量赋予初始值。循环变量也可以在此处声明；如果在此处声明，则其作用域仅限于 `for` 语句。这意味着你只能在循环内使用该循环变量。这也意味着你可以在循环外自由重用该变量名来声明一个与循环变量同名的不同变量。初始化部分只执行一次。
  - **条件。** `condition` 部分是一个布尔表达式，与 `while` 语句的条件类似。每次执行循环体*之前*都会检查条件。
  - **修改。** `modification` 部分通常会更改循环变量。更改应使得条件最终变为假，以便循环终止。修改在每次迭代中执行，在循环体执行*之后*。请注意，最后一部分（`modification`）后面不跟分号；分号严格用于分隔三个部分。
- `statement` 与任何其他循环的循环体类似。它可以是花括号内的复合语句。

任何 `for` 循环都可以重写为 `while` 循环。上面给出的 `for` 循环的一般形式可以等价地写成

```
initialization
while ( condition ) {
statement
modification
}
```

清单 7.4 (forcounttofive.cpp) 使用 `for` 语句数到 5。

```
#include <iostream>
int main() {
    for (int count = 1; count <= 5; count++)
        std::cout << count << "\n"; // Display counter
}
```

使用 while 循环时，四个计数组件（变量声明、初始化、条件和修改）可以散布在代码中。使用 for 循环时，程序员应该能够通过查看一个语句来确定循环控制的所有重要信息。

回顾在屏幕上打印乘法表的清单 6.13 (timetable.cpp)。我们可以通过将所有 while 语句转换为 for 语句来更好地组织其代码。结果使用的代码要少得多，如清单 7.5 (bettertimestable.cpp) 所示。

清单 7.5: bettertimestable.cpp

```cpp
#include <iostream>
#include <iomanip>

int main() {
    int size; // The number of rows and columns in the table
    std::cout << "Please enter the table size: ";
    std::cin >> size;
    // Print a size x size multiplication table

    // First, print heading
    std::cout << "   ";
    for (int column = 1; column <= size; column++)
        std::cout << std::setw(4) << column; // Print heading for this column.
    std::cout << "\n";
    // Print line separator
    std::cout << "   +";
    for (int column = 1; column <= size; column++)
        std::cout << "----"; // Print separator for this column.
    std::cout << "\n";
    // Print table contents
    for (int row = 1; row <= size; row++) {
        std::cout << std::setw(4) << row << " |"; // Print row label.
        for (int column = 1; column <= size; column++)
            std::cout << std::setw(4) << row * column; // Display product
        std::cout << "\n"; // Move cursor to next row
    }
}
```

for 循环非常适合遍历行和列。两个循环的控制信息现在分别封装在各自的 for 语句中，而不是分散在 main 的各个位置。在 while 版本中，程序员很容易忘记更新一个或两个计数器变量（row 和/或 column）。for 循环使程序员更难忘记循环变量更新，因为更新是在 for 语句标题中直接完成的。

在 for 语句中做以下任何一项都被视为不良编程实践：

- 在循环体内修改循环控制变量——如果在循环体内修改循环变量，则循环控制的逻辑不再完全隔离在 for 语句的标题中。程序员必须在语句的其他地方查看才能完全理解循环的工作原理。
- 使用 break 过早退出循环——此操作也违反了将所有循环控制逻辑保持在一个地方（for 的标题）的概念。

语言允许这两种做法，但经验表明最好避免它们。如果似乎有必要违反此建议，请考虑使用另一种循环。while 和 do/while 循环并不意味着 for 循环所期望的同样程度的控制规律性。

清单 7.6 (permuteabcd.cpp) 是清单 6.14 (permuteabc.cpp) 的重写，它将 while 循环替换为 for 循环并添加了一个额外字符。

清单 7.6: permuteabcd.cpp

```cpp
// File permuteabcd.cpp
#include <iostream>
int main() {
    for (char first = 'A'; first <= 'D'; first++)
        for (char second = 'A'; second <= 'D'; second++)
            for (second != first; // No duplicate letters
                for (char third = 'A'; third <= 'D'; third++)
                    if (third != first && third != second)
                        for (char fourth = 'A'; fourth <= 'D'; fourth++)
                            if (fourth != first && fourth != second && fourth != third)
                                std::cout << first << second << third << fourth << '\n';
}
```

请注意，由于所有变量初始化和递增都在 for 语句标题中处理，我们不再需要循环体中的复合语句，因此花括号是不必要的。清单 7.6 (permuteabcd.cpp) 打印 ABCD 的所有 24 个排列：

```
ABCD
ABDC
ACBD
ACDB
ADBC
ADCB
BACD
BADC
BCAD
BCDA
BDAC
BDCA
CABD
CADB
CBAD
CBDA
CDAB
CDBA
DABC
DACB
DBAC
DBCA
DCAB
DCBA
```

清单 7.7 (forprintprimes.cpp) 是清单 6.22 (printprimes.cpp) 的重写，它将 while 循环替换为 for 循环。
