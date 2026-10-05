

## 5.10. 总结

range 0...10 并接受所有其他数字。以下代码片段中的布尔表达式能胜任吗？

```cpp
// 我想使用除 0, 1, 2, ..., 10 外的所有数字
if (value < 0 && value > 10)
/* 在此处执行代码 */
```

仔细观察该条件可以发现它永远不会为真。什么数字能同时小于零又大于零？是不可能的，因此该表达式是一个矛盾体，是表达假的一种复杂方式。要纠正此代码片段，请将 `&&` 运算符替换为 `||`。

## 5.10 总结

- `bool` 数据类型表示 `true` 和 `false` 两个。
- 该名称源于布尔代数，即对真值运算的数学研究。
- 在 C++ 中，`true` 用整数 `1` 表示，`false` 用零 `0` 表示。
- 除零 以外的任何整数值都被视为 `true`。
- 整数和 `bool` 是可以转换的，可以互相赋值。
- 涉及关系运算符（`==`, `!=`, `<`, `>`, 和 `>=`）的表达式会求出布尔值。
- `!` 是单元取反运算符。
- 布尔表达式可以通过 `&&`（逻辑与）和 `||`（逻辑或）组合。
- `if` 语句可以用于选择性地执行语句。
- 复合语句是位于大括号 `{}` 内的一系列语句。
- `if` 语句有一个可选的 `else` 子句，用于在两条交替的执行路径之间进行选择。
- `if/else` 语句可以嵌套以实现复杂性。
- `if/else` 语句的体部分应该缩进，以便人类读者阅读。缩进不影响程序的逻辑；当多个语句要作为 `if` 或 `else` 语句体的一部分时，这些语句必须是复合语句的一部分。
- 注意不要在 `if` 语句条件的右括号后紧跟放置分号。
- 复杂的布尔表达式需要特别注意，因为它们很容易出错。

## 5.11 练习题

- 1. 类型为 `bool` 的变量可以取哪些值？
- 2. `bool` 这个词源于哪里？
- 3. 在 C++ 中 `true` 对应的整数是什么？
- 4. 在 C++ 中 `false` 对应的整数是什么？
- 5. 值 `-16` 被解释为 `true` 还是 `false`？
- 6. 整数值可以赋值给 `bool` 变量吗？
- 7. `true` 可以赋值给 `int` 变量吗？
- 8. 给定以下声明：

```cpp
int x = 3, y = 5, z = 7;
bool b1 = true, b2 = false, b3 = x == 3, b4 = x < 3;
```

求值布尔表达式：

- (a) x == 3
(b) x < y
(c) x >= y
(d) x <= y
(e) x != y - 2
(f) x < 10
(g) x >= 0 && x < 10
(h) x < 0 && x < 10
(i) x == 0 || x < 2
(j) x > 0 || x < 10
(k) x > 0 || x < 10
(l) x < 0 || x > 10
(m) b1
(n) !b1
(o) !b2
(p) b1 && b2

- 9. 将布尔表达式化为更简单的形式；即使用更少的运算符。`x` 是一个 `int`。

- (a) !(x == 2)
(b) x < 2 || x == 2
(c) !(x < y)
(d) !(x <= y)
(e) x < 10 && x > 20
(f) x > 10 || x < 20
- (g) x != 0
(h) x == 0

10. 最简单的重真式是什么？
11. 最简单的矛盾式式是什么？
12. 编写一个 C++ 程序，向用户请求一个整数值。如果该值在 1 到 100 之间（包含边界），打印 "OK"；否则什么都不打印。
13. 编写一个 C++ 程序，向用户请求一个整数值。如果该值在 1 到 100 之间（包含边界），打印 "OK"；否则，打印 "Out of range."。
14. 编写一个 C++ 程序，向用户请求一个整数值。如果该值在 1 到 100 之间（包含边界），打印 "OK"；否则，打印 "Out of range."。
15. 以下程序尝试根据输入打印相应的消息。例如，如果用户输入值 3，程序应该打印 "You entered three"。目前程序包含逻辑错误。找到问题并修复它们，使程序按预期工作。

```cpp
#include <iostream>

using namespace std;

int main() {
    cout << "Please value in range 1...5: ";
    int value;
    cin >> value;
    if (value == 1)
        cout << "You entered one";
        cout << endl;
    else if (value == 2)
        cout << "You entered two";
        cout << endl;
    else if (value == 3)
        cout << "You entered three";
        cout << endl;
    else if (value == 4)
        cout << "You entered four";
        cout << endl;
    else if (value == 5)
        cout << "You entered five";
        cout << endl;
    else
        cout << "value of range";
        cout << endl;
}
```

- 16. 考虑以下代码段：

```cpp
// i, j, and k are ints
if (i < j) {
    if (j < k)
        i = j;
    else
        j = k;
}else {
    if (j > k)
        j = i;
    else
        i = k;
}
cout << "i = " << i << " j = " << j << " k = " << k << endl;
```

如果变量 i, j 和 k 有以下值，代码将打印什么？

- (a) i 为 3, j 为 5, k 为 7
(b) i 为 3, j 为 7, k 为 5
(c) i 为 5, j 为 3, k 为 7
(d) i 为 5, j 为 7, k 为 3
(e) i 为 7, j 为 3, k 为 5
(f) i 为 7, j 为 5, k 为 3

- 17. 考虑以下打印一行文本的 C++ 程序：

```cpp
#include <iostream>
using namespace std;

int main() {
    int input;
    cin >> input;
    if (input < 10) {
        if (input != 5)
            cout << "wow";
        else
            input++;
    } else {
        if (input == 17)
            input += 10;
        else
            cout << "whoa";
    }
    cout << input << endl;
}
```

如果用户提供以下输入，程序将打印什么？

(a) 3
(b) 21
(c) 5
(d) 17
(e) -5

- 18. 为什么以下代码段总是打印 "ByeHi"？

```cpp
int x;
cin >> x;
if (x < 0)
    cout << "Bye";
cout << "Hi" << endl;
```

- 19. 编写一个 C++ 程序，向用户请求五个整数值。打印最大值和最小值。如果用户输入值 3, 2, 5, 0 和 1，程序应指示 5 是最大值，0 是最小值。你的程序应该正确处理相等情况；例如，如果用户输入 2, 4, 2, 3，程序应该报告 2 为最小值，4 为最大值。
- 20. 编写一个 C++ 程序，向用户请求五个整数值。如果输入的任何值有重复，打印 "DUPLICATES"；否则打印 "ALL UNIQUE"。
- 21. 编写一个 C++ 程序 ...

## 第 6 章：迭代

迭代重复代码序列的执行。迭代有助于解决编程问题。迭代和条件执行是算法构造的关键组件。

## 6.1 while 语句

列表 6.1：countoftive.cpp 通过在每行输出打印一个数字来数到五。

列表 6.1：countoftive.cpp
```cpp
#include <iostream>
using namespace std;

int main() {
  cout << 1 << endl;
  cout << 2 << endl;
  cout << 3 << endl;
  cout << 4 << endl;
  cout << 5 << endl;
}
```

编译并运行该程序，它显示：

![](img/e32630bd50fbc4f7d5a64c18eb635_119_0.png)

如何编写代码数到 10000？你会复制、粘贴并修改 10000 条语句吗？那是不现实的！计数是一项常见的活动，计算机经常数到很大的值，因此必须有一种更好的方法。这个过程是迭代（或循环），在 C++ 中我们可以通过多种方式实现循环。

列表 6.2：（iterativeoftive.cpp）使用 `while` 语句数到五：

```cpp
#include <iostream>

using namespace std;

int main() {
    int count = 1;           // 初始化计数器
    while (count <= 5) {   // 显示计数器，然后
        cout << count << endl;
        count++;
    }
}
```

列表 6.2 (iterativecountive.cpp) 使用 `while` 语句显示正在数到五。与列表 6.1 (countoftive.cpp) 采用的方法不同，修改列表 6.2 (iterativecountive.cpp) 数到 10000 非常简单——只需将字面量 5 改为 10000。

`while` 语句的一般形式如下：

![](img/e32630bd50fbc4f7d5a64c18eb635_120_0.png)

while (count <= 5) 开始 `while` 语句。括号内的表达式必须是一个布尔表达式。如果布尔表达式为真，程序的执行到达 `while` 语句，程序执行 `while` 语句的体，然后再次检查条件。只要布尔表达式为真，程序就会重复执行 `while` 体内的语句。

当执行 `while` 语句时，如果布尔表达式为真，则执行 `while` 语句的体，并且只要布尔表达式为真，就会重复执行该体。

```
cout << count << endl;
count++;
```

构成了 `while` 语句的体。由于包含多个语句，所以大括号是必要的。

