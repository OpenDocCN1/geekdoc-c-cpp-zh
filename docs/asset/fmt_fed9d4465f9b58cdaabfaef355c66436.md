
一个基础响应系统可能只需告诉客户找到他们的账号，并在他们准备好连接到代理时按 1。你可以使用流程图来绘制这种逻辑，用菱形表示决策。见图 6-2。

![](img/7921c83706ea2c639325e413353f7951_104_0.png)

图 6-2 if-then 结构的流程图

流程图中的菱形符号表示决策点，并包含一个问题。当答案为真时，箭头引导至语句块。如果答案为假，则跳过该语句块。`if-then` 结构在伪代码中可以这样表示：

```
if choice == 1 then
    connect to agent
```

`if-then` 结构在伪代码中可以这样表示：

```
if choice == 2 then
    troubleshoot cable_service
```

`if-then` 结构在伪代码中可以这样表示：

```
if choice == 3 then
    troubleshoot internet_service
```

`if-then` 结构在伪代码中可以这样表示：

```
if choice == 0 then
    quit
```

`if-then` 结构在伪代码中可以这样表示：

```
if choice == 1 then
    connect to agent
else
    find_account_number
```

这被称为 `if-then-else` 结构。`if-then-else` 结构按顺序执行。例如，如果用户按 9，程序将执行 `else` 分支。

```
if choice == 1 then
    connect to agent
else
    find_account_number
```

`if-then-else` 结构在伪代码中可以这样表示：

```
if choice == 1 then
    connect to agent
else if choice == 2 then
    troubleshoot cable_service
else
    find_account_number
```

`if-then-else-if` 结构允许处理多个条件。如果用户按 2，程序将执行 `else-if` 分支。如果用户按 3，程序将跳过第一个 `if` 分支并执行第二个 `if` 分支。如果用户按 9，程序将执行最后的 `else` 分支。

```
if choice == 1 then
    connect to agent
else if choice == 2 then
    troubleshoot cable_service
else if choice == 3 then
    troubleshoot internet_service
else
    find_account_number
```

`if-then-else-if` 结构在伪代码中可以这样表示：

```
if choice == 1 then
    connect to agent
else if choice == 2 then
    troubleshoot cable_service
else if choice == 3 then
    troubleshoot internet_service
else if choice == 0 then
    quit
else
    find_account_number
```

嵌套-`if` 结构包含一个另一个 `if` 语句。

```
if choice == 1 then
    connect to agent
else
    if choice == 2 then
        troubleshoot cable_service
    else
        find_account_number
```

追踪包含嵌套-`if` 结构的算法执行流。如果用户按 1，程序将连接到代理。如果用户按其他数字，程序将进入嵌套的 `if` 语句。如果按 2，程序将排除电缆故障；如果按其他数字，程序将查找账号。

```
if (choice == 1) {
    // connect to agent
} else {
    if (choice == 2) {
        // troubleshoot cable service
    } else {
        // find account number
    }
}
```

追踪包含 `else-if` 结构的算法执行流。

在 C++ 中，你可以在程序中使用 `if` 结构。

```cpp
#include <iostream>
using namespace std;

int main() {
    int choice;
    cin >> choice;
```

`if-then-else-if` 结构在伪代码中可以这样表示：

```
if choice == 1 then
    connect to agent
else if choice == 2 then
    troubleshoot cable_service
else if choice == 3 then
    troubleshoot internet_service
else if choice == 0 then
    quit
else
    find_account_number
```

在 C++ 中，你可以使用 `if` 结构。

```cpp
if (choice == 1) {
    cout << "Connecting to agent..." << endl;
} else if (choice == 2) {
    cout << "Troubleshooting cable service..." << endl;
} else if (choice == 3) {
    cout << "Troubleshooting internet service..." << endl;
} else if (choice == 0) {
    cout << "Exiting..." << endl;
} else {
    cout << "Please find your account number." << endl;
}
```

## 6.2 关系运算符

### 等运算符 6.2.1

`==` 是你在构造条件表达式时使用的关系运算符之一。关系运算符指定两个操作数之间的比较。操作数可以是：

- 两个字量，例如 7 和 9
- 两个变量，例如 `airtime` 和 `limit`
- 一个变量和一个字量，例如 `airtime` 和 1000

`==` 运算符与赋值运算符完全不同。在条件语句中使用 `==` 运算符可能会产生错误。

C++ 编程

![](img/7921c83706ea2c639325e413353f7951_107_0.png)

赋值运算符将 1 放入变量。

`==` 运算符比较 `choice` 与字量 1。当它们相等时，表达式为真。

![](img/7921c83706ea2c639325e413353f7951_107_1.png)

赋值运算符无法在将 1 放入变量的同时与字量 1 进行比较。

### 使用关系运算符 6.2.2, 6.2.3

图 6-6 提供了关系运算符的列表及其用法。

| 运算符 | 描述 | 示例 `airtime = 1056` | 结果 |
|---|---|---|---|
| `==` | 等于 | (`airtime == 1056`) (`airtime == 566`) | 真, 假 |
| `!=` | 不等于 | (`airtime != 1056`) (`airtime != 566`) | 假, 真 |
| `<` | 小于 | (`airtime < 2000`) (`2000 < airtime`) | 真, 假 |
| `>` | 大于 | (`airtime > 56`) (`56 > airtime`) | 真, 假 |
| `<=` | 小于等于 | (`airtime <= 1056`) (`airtime <= 29`) | 真, 假 |
| `>=` | 大于等于 | (`airtime >= airtime`) (`airtime >= 2000`) | 真, 假 |

**图 6-6** 关系运算符

`if-then` 结构你可以在编程语言中使用，如 **图 6-4** 所示。

```cpp
#include <iostream>
using namespace std;
int main() {
    int choice;
    cin >> choice;
```

图 6-4 `if-then` 结构 (继续)

```cpp
    if (choice == 1) {
        cout << "Connecting to agent..." << endl;
    }
```

```cpp
    if (choice == 1) {
        cout << "You chose 1" << endl;
    }
```

```cpp
OUTPUT:
Connecting to agent...1
You chose 1
```

图 6-4 `if-then` 结构

追踪图 6-4 中的程序。如果用户输入非 1 的数字会发生什么？

关系运算符为构建条件表达式提供了很大的灵活性。例如，在下面的伪代码中，你可以使用 `!=` 运算符来验证语音响应系统的输入：

```
output "Press or say 1 when you are ready to"
output "connect to an account agent: "
input choice
if choice != 1 then
    output "You chose option " + choice
    output "Invalid input"
```

**图 6-7** 用代码形式展示了该算法。

```cpp
#include <iostream>
using namespace std;
int main() {
    int choice;
    cout << "Press or say 1 when you are ready to" << endl;
    cout << "connect to an account agent: ";
    cin >> choice;
    if (choice != 1) {
        cout << "You chose option " << choice << endl;
        cout << "Invalid input" << endl;
    }
}
```

输出:
**Press or say 1 when you are ready to**
**connect to an account agent: 9 [Enter]**
You chose option 9
**Invalid input**

**图 6-7** 使用决策结构验证输入

### 布尔表达式与数据类型 6.2.4, 6.2.5, 6.2.6

关系运算符执行结果为 True（真）或 False（假）的布尔表达式。例如，`choice != 1` 是一个布尔表达式，当用户未选择 1 时为 True。当用户选择 1 时，该布尔表达式为 False。

## C++编程

布尔表达式与布尔数据类型有相似之处。两者都携带 True 或 False 的值。但在实践中，将布尔表达式用作条件语句，而在声明或赋值语句中使用布尔数据类型。

例如，你可能希望变量 `vip` 存储 True 或 False，取决于客户是否具有 VIP 状态。在伪代码中，你可以这样初始化布尔变量：

```
initialize bool vip = True
```

在内存中，布尔变量存储 0 表示 False，存储 1 表示 True。从理论上讲，布尔只需要 1 位存储，但实际存储因语言而异。

某些编程语言（如 Python）要求 True 和 False 大大写。在其他语言（如 C++ 和 Java）中，`true` 和 `false` 必须小写。在伪代码中，True 和 False 是大写的。现在请看下面的伪代码：

> 上述伪代码中的布尔变量是什么？条件语句是什么？布尔表达式又是什么？

布尔变量是 `vip`，它出现在声明和赋值语句。条件语句是 `if vip then`。布尔表达式是条件语句中的 `vip`。

当布尔变量在条件语句中使用时，它不需要关系运算符。布尔值已经是 True 或 False 了，因此不需要冗余的表达式，例如 `if vip == True`。

图 8 展示了在代码中如何使用它。

```cpp
#include <iostream>
using namespace std;
int main() {
  bool vip = true;
  if (vip) {
    cout << "You get the VIP discount!" << endl;
  }
}
OUTPUT:
You get the VIP discount!
```

图 8 在条件语句中使用布尔变量

## 6.3 多重条件

### If-Then-Else 结构 6.3.1, 6.3.2, 6.3.3

假设一个响应系统为客户提供两个选项：

- 准备好连接账户代理时，按 1 或说 1。
- 按 0 或说 0 退出。

**图 6-9** 展示了该算法的流程图。注意，True 和 False 分支都包含语句。程序根据布尔表达式的结果遵循这些分支之一。

![](img/7921c83706ea2c639325e413353f7951_110_0.png)

**图 6-9** `if-then-else` 结构

编码为两个可能路径的决策被称为 **`if-then-else` 结构**。响应算法的伪代码使用关键字 **`else`** 来指定备选执行路径。

```
output "Press or say 1 when you are ready to"
output "connect to an account agent."
output "Press or say 0 to quit."
input choice
if choice = 1 then
    output "You choose option 1."
    output "Connecting you now."
else
    output "You choose option 0."
    output "Bye."
```

图 6-10 展示了 `if-then-else` 结构的语法、规则和最佳实践。

| 语法: | 规则与最佳实践: |
| --- | --- |
| `if (condition)` | - 将 **`else`** 关键字单独放在一行，并保持与 `if` 语句相同的缩进级别。 |
| `statement;` | - 当 `else` 块包含多个一个语句时，使用大括号。 |
| `statement;` | - 关键字 **`else`** 之后不需要分号。 |
| `else` | |
| `statement;` | |
| `statement;` | |

图 6-10 `if-then-else` 语法

**图 6-11** 中的代码包含包含一个带有两个语句的 `if` 块。它还包含一个带有两个语句的 `else` 块。

```cpp
#include <iostream>
using namespace std;
int main()
{
    int choice;
    cout << "Press or say 1 when you are ready to" << endl;
    cout << "connect to an account agent." << endl;
    cout << "Press or say 0 to quit." << endl;
    cin >> choice;
    if (choice == 1) {
        cout << "You choose option 1." << endl;
        cout << "Connecting you." << endl;
    }
    else {
        cout << "You choose option 0." << endl;
        cout << "Bye." << endl;
    }
}
```

**图 6-11** `if-then-else` 结构的示例代码（续）

输出:

Press or say 1 when you are ready to 
connect to an account agent.
Press or say 0 to quit.
0 [Enter]

You chose option 0.
Bye.

图 6-11 `if-then-else` 结构的示例代码

### 嵌套 if 结构 6.3.4

有时程序需要在决策中进行决策。例如，假设在客户选择“退出”选项后，你想检查客户是否真的想退出。决策之中的决策通常被称为嵌套 `if` 结构。图 12 展示了针对想要退出的客户的嵌套 `if`。

![](img/7921c83706ea2c639325e413353f7951_112_0.png)

图 12 `if if` 结构

## C++ 编程

以下伪代码包含一个嵌套 `if` 结构，用于确认客户是否想退出。根据输入，客户将连接到帮助台。

```
output "Press or say 1 when you are ready to"
output "connect to an account agent."
output "Press or say 0 to quit."
input choice
if choice == 0 then
    output "Are you sure want to quit?"
    input sure_thing
        if sure_thing == 'y' then
