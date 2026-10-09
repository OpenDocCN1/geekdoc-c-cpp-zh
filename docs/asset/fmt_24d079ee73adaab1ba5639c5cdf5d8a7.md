
- 类模板成员函数 `size`（第 360 页）返回调用的 vector 中的元素数量。
- 使用方括号 `[]` 可以访问或修改 vector 元素的值。

## 第 7 章 类模板与 vector：捕获异常

- 标准类模板 `vector` 的对象可以直接使用等等 `==` 和不等于 `!=` 运算符进行比较。赋值运算符 `=` 也可以用于 vector 对象。
- 不可修改的左值（一个常引用引用）是一个识别内存中对象（例如 vector 中的某个元素）的表达式，但不能用于修改它。可修改的左值（一个非常量引用）也识别内存中的对象，但可以用于修改该对象。
- 异常（第 361 页）表示程序在执行时发生的问题。“异常”一词暗示问题是在意料之外发生的——如果说“规则”是指正常执行执行的语句，那么问题就代表了“对规则的例外”。
- 异常处理（第 361 页）允许你创建可以解决异常的容错型程序（第 361 页）。
- 要处理异常，请将可能抛出异常（第 362 页）的代码放置在 `try` 语句中。
- `try` 块（第 362 页）包含可能抛出异常的代码，而 `catch` 块（第 362 页）包含在发生异常时处理该异常的代码。
- 当 `try` 块结束时，数组中声明的所有变量将超出作用域。
- `catch` 块声明了一个变量和一个异常参数。在 `catch` 块内部，你可以使用参数标识符与捕获的异常对象进行交互。
- 异常的 `what` 成员函数（第 362 页）返回错误信息。

## 自测练习题

### 7.1（填空）回答以下每个问题：

- a) 数值的列表和表格可以存储在 __________ 或，__________ 中。
- b) 数组元素的识别依据是它们具有相同的 __________ 且具有...
- c) 用来引用数组中特定元素的数字被称为 __________。
- d) 应该使用 __________ 来确定数组的大小，因为它消除了魔术数字。
- e) 将数组元素顺序排列的过程被称为对数组进行 __________。
- f) 判断数组是否包含特定键值的过程被称为对数组进行 __________。
- g) 使用两个下标的数组被称为 __________ 数组。

### 7.2（判断对错）说明以下陈述的对或否。如果答案为否，请解释原因。

- a) 数组是共享相同类型的内存位置的集合。
- b) 你可以使用基于范围的语句通过使 `rangeVariable` 成为引用来修改每个元素。
- c) 函数定义中的静态变量在整个程序运行期间存在，但在函数体内部不存在。
- d) 用于索引数组的括号是一个运算符，其优先级与圆括号不同。

### 7.3（编写 C++ 语句）编写一条或多条语句对创建的数组执行以下任务：

- a) 定义一个常量 `arraySize` 表示数组的大小，并将其初始化为 8。
- b) 声明一个具有 `arraySize` 个 `double` 类型元素的数组，并将元素初始化为 1.0。
- c) 为数组的第三个元素命名。
- d) 引用数组元素 3。
- e) 将值 1.667 赋值给数组元素 7。
- f) 将值 3.333 赋值给数组的第 6 个元素。
- g) 显示数组元素 5 和 7，小数点后保留一位数字精度，并显示屏幕上实际显示的输出。
- h) 使用计数器控制的 `for` 语句显示所有数组元素。定义整数变量 `j` 作为循环控制变量。显示输出。
- i) 使用基于范围的 `for` 语句用逗号 分隔显示所有数组元素。

### 7.4（二维数组问题）关于一个名为 `table` 的二维数组回答以下问题：

- a) 声明一个存储 `int` 值的数组，并有 4 行 4 列。假设变量 `count sizeArray` 已经定义为 4。
- b) 数组包含多少元素？
- c) 使用计数器控制的 `for` 语句将数组的每个元素初始化为其下标的积。
- d) 编写一条语句，以 4 行 4 列的表格格式显示数组 `table` 中每个元素的值。每行每列都应用行号或列号标记。假设数组使用包含从 1 到 16 值的初始化列表初始化。显示输出。

### 7.5（错误）发现并修正以下代码段中的错误：

```
a) #include <iostream>
```
```
b) arraySize = 12; // sizeArray 被声明为 const
```
```
c) 假设有 var int b[10] = {}; for ( size_t i = 0; i < b.size(); ++i )
   b[i] = 1;
```
```
d) 假设 a 是一个 2 行 2 列的 int 二维数组：
   a[2][2] = 10;
```

## 自测练习答案

7.1 a) arrays, Vectors b) array name, type. c) subscript or index. d) const variable. e) sorting, f) two-dimensional.

7.2 a) 对确 b) 否。函数定义中的静态局部变量在整个程序运行期间存在，但仅在函数体内可见。d) 否。用于确保索引正确的括号是正确的，因为优先级在前。

7.3 a) `const double sizeArray = 8;`
b) `double fractions[arraySize] = { 1.0 };`
c) `fractions[ 2 ]`
d) `fractions[ 3 ]`
e) `fractions[ 7 ] = 1.667;`
f) `fractions[ 5 ] = 3.333;`
g) `cout << fixed << setprecision( 1 ) << fractions[ 9 ] << endl;`
Output: 3.3
h) 
```
for ( size_t j = 0; j < fractions.size(); ++j )
   cout << "fractions[" << j << "]" << fractions[ j ] << endl;
```
Output:
```
fractions[ 0 ] = 1.0
fractions[ 1 ] = 1.0
fractions[ 2 ] = 1.0
```
```
fractions[ 3 ] = 1.0
fractions[ 4 ] = 1.0
fractions[ 5 ] = 3.333
fractions[ 6 ] = 1.0
fractions[ 7 ] = 1.667
```
```
for ( double element : fractions )
    cout << element << ' ';
```

7.4 a) `array<int, arraySize> table;`
b) 十.

```
for ( size_t row = 0; row < table.size(); ++row)
    for ( size_t column = 0; column < table[row].size(); ++column)
        table[row][column] = row * column;
```
d) `cout << "0 1 2 3" << endl;`
```
for ( size_t i = 0; i < 4; ++i) {
    cout << "row " << i << ": ";
    for ( size_t j = 0; j < 4; ++j)
        cout << table[i][j] << " ";
    cout << endl;
}
```
Output:
```
row 0: 0 1 2 3 
row 1: 4 5 6 7 
row 2: 8 9 10 11 
row 3: 12 13 14 15 
```

7.5 a) 在 include 前加 #。
b) 在 arraySize 前加 const。
c) 将 int 更改为 vector<int> 并使用 size_t 用于循环索引。
d) 将分号改为中括号。

## 第 7 章 类模板 数组与 vector：捕获异常

### 7.11（一维数组问题）编写执行以下多维数组操作的语句：

- 将 double 数组 `values` 的 10 个元素初始化为 0.5。
- 将 double 数组 `values` 的每第二个元素加 1。
- 从 double 数组 `values` 的 `store` 中读取 5 个值。
- 以列格式（保留2位小数）打印 10 个 double 数组值，前 5 个值在第一行，后 5 个在下一行下方。

### 7.12（找错）找出以下每个语句中的错误：

- `array<int,5> f={0,1,2,3,4};`
- 假设 `array_val5` 是一个包含三个 double 的数组。`cin >> array_val5[];`
- 假设 `array_val5` 是一个两行三列的数组：`array<double,2,> array_val5;`
- 假设 `array_val5` 是一个两行三列的数组：`ray_val5[][]={1,2,3,4,5};`

### 7.13（数组去重）使用一维数组解决此问题。读取 20 个数字，每个数字都在 10 到 100 之间（包含边界）。每读取一个数字，对其进行验证，如果尚未重复则将其存储在数组中。读取所有值，仅显示用户输入的唯一值。为所有 20 个数字都不同的“最坏情况”提供解决方案。使用尽可能小的数组来解决此问题。

### 7.14（vector 去重）使用 vector 重新实现 7.13，使用一个空 vector 并使用其 `push_back` 函数将每个值添加到 vector 中。

### 7.15（二维数组初始化）为 3x5 二维数组 `sales` 的元素进行标记，以指示它们在以下程序段中被设置为 0 的顺序：

```cpp
for (size_t row=0; row<rows.size(); ++row) {
  for (size_t column=0; column<rows[row].size(); ++column) {
    sales[row][column]=0;
  }
}
```

### 7.16（掷骰子）编写一个程序模拟掷两个骰子的过程。两个值之和 [注：每个骰子可以显示 1 到 6 之间的整数值，因此两个值之和将在 2 到 12 之间变化，其中 7 频率最高，12 频率最低。] 图 22 显示了两个骰子的 36 种组合。使用一维数组统计每个可能的总和出现的次数。以表格格式打印结果。此外，判断总数是否合理（例如，掷出 7 有六种方式，因此大约六分之一的投掷结果应该是 7）。

| | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| 5 | 6 | 7 | 8 | 9 | 10 | 11 |
| 6 | 7 | 8 | 9 | 10 | 11 | 12 |

7.22 掷两个骰子的 36 种可能组合。

### 7.17（这段代码是做什么的？）以下程序是做什么的？

```cpp
// Ex. 7.17: Ex07_17.Cpp
// 这个程序是做什么的？
#include <iostream>
#include <array>
using namespace std;
const size_t arraySize{10};
int whatIsThis(const array<int, arraySize>&, size_t size); // 声明
int main() {
    array<int, arraySize> a{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int result(whatIsThis(a, arraySize));
    cout << "Result is " << result << endl;
}
// 这个函数是做什么的？
int whatIsThis(const array<int, arraySize>& b, size_t size) {
    if (size == 1) // 基础情况
        return b[0];
    else // 递归步骤
        return b[size - 1] + whatIsThis(b, size - 1);
}
```
Fig. 7.23 | 这个程序是做什么的？

### 7.18（骰子游戏修改）修改图 6.9 的程序以玩 1000 局骰子。程序应该跟踪统计数据并回答以下问题：

- a) 在第 1 次掷、第 2 次掷、……第 20 次掷以及第 20 次掷之后赢了多少局？
- b) 在第 1 次掷、第 2 次掷、……第 20 次掷以及第 20 次掷之后输了多少局？
- c) 玩骰子获胜的概率是多少？[注：你会发现骰子游戏是最优秀的游戏之一。你认为这意味着什么？]
- d) 一局骰子游戏的平均长度是多少？
- e) 获胜概率会随着游戏长度而提高吗？

### 7.19（将 7.10 节的 vector 示例转换为数组）将图 21 的 vector 示例转换为数组。消除任何 vector。

### 7.20（这是做什么的？）以下程序是做什么的？

```cpp
// Ex. 7.20: Ex07_20.cpp
// 这个程序是做什么的？
#include <iostream>
#include <array>
using namespace std;
const size_t arraySize{10};
void someFunction(const array<int, arraySize>& b, size_t current); // 声明
```
Fig. 7.24 | 这个程序是做什么的？（第一部分）

```cpp
int main() {
    array<int, arraySize> a{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    cout << "Values in:" << endl;
    someFunction(a, 0);
    cout << endl;
}
// 这个函数是做什么的？
void someFunction(const array<int, arraySize>& b, size_t current) {
    if (current < b.size()) {
        cout << b[current] << " ";
        someFunction(b, current + 1);
    }
}
```
Fig. 7.24 | 这个程序是做什么的？（第二部分）

### 7.21（工作坊总结）使用二维数组解决此问题。一个工作坊有三个工人（1 到 3），每天完成四种产品（1 到 4）。

- a) 工人编号
- b) 产品编号
- c) 完成的数量

编写一个程序，记录每天完成的产品数量。产量应存储在二维数组中。在处理所有信息后，以表格格式展示每个工人的总产量。

### 7.22（骑士巡游）棋类爱好者最有趣的谜题之一是骑士巡游问题。问题在于棋子是否可以在棋盘上移动且仅访问每个格子一次！我们正在深入研究这个问题。

- a 在纸上画一个 8x8 的棋盘，并在第一个格子写 1，第二个写 2，以此类推。在开始巡游之前，估计需要多久；记住一次巡游由 64 步组成。你的估计接近吗？
- b 我们写一个程序让骑士在棋盘上移动。棋盘由 8x8 二维数组表示。每个格子初始化为零。我们通过水平和垂直分量来描述八种移动。例如，类型 0 的移动（如图 7.25 所示）向右移动两格并向上移动一格。向左移动和向上移动用负数表示。这八种移动可以用水平和垂直数组来描述，如下：

```cpp
horizontal[0] = 2   vertical[0] = -1
horizontal[1] = 1   vertical[1] = -2
horizontal[2] = -1  vertical[2] = -2
horizontal[3] = -2  vertical[3] = -1
horizontal[4] = 4   vertical[4] = 1
horizontal[5] = -1  vertical[5] = 2
horizontal[6] = 2   vertical[6] = 1
```

变量 `currentRow` 和 `currentColumn` 指明骑士当前的位置行和列。为了执行 `moveNumber` 的移动（`moveNumber` 在 0 到 7 之间），你的程序使用：

```cpp
currentRow += moveNumber;
currentColumn += moveNumber;
```
