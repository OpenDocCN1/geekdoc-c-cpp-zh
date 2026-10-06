
# 第 4 章 决策

## 4.2 if 语句

### 编程风格与 if 语句

即使 if 语句通常跨越多行，但在技术上它们仍然是长语句。例如，下面的 if 语句除了风格外，是完全相同的：

```cpp
if (a >= 100)
    cout << "The Number is out of range.\n";

if (a >= 100) cout << "The Number is out of range.\n";
```

在上述两个示例中，编译器将 `if` 和 `cout` 语句识别为一个单元，并在末尾正确放置了分号。缩进和间距是为了程序的类人阅读者，而不是为了编译器。以下是你在编写 if 语句时应该采用的两个重要风格规则：

- 条件分支执行的语句应该出现在 if 语句之后的下一行。
- 条件分支执行的语句应该比 if 语句缩进一个“级别”。

> **注意**：在大多数编辑器中，每当你按一次 tab 键，你就缩进了一个级别。

通过缩进条件分支执行的语句，你让它在视觉上脱颖而出。这样做是为了让你一眼看出 if 语句执行了程序的哪个部分。这是编写 if 语句的标准方法，也是你应该使用的方法。

> **注意**：缩进和间距是为了程序的类人阅读者，而不是为了编译器。尽管程序 4-3 中 if 语句后的 `cout` 语句被缩进了，但分号仍然终止了 if 语句。

### 比较浮点数

由于浮点数在内存中的存储方式，有时会发生舍入误差。这是因为某些分数无法用二进制精确表示。因此，当在使用等号运算符 (`==`) 比较浮点数时，要小心。例如，程序 4-4 使用了两个 `double` 类型变量 `a` 和 `b`。两个变量都初始化为值 1.5。然后，给 `a` 加上 0.00000000000000001。这本应该使 `a` 的内容不同于 `b` 的内容。但由于舍入误差，这两个变量是相同的。

### 程序 4-4

```cpp
1 // 本程序演示了浮点
2 // 舍入误差如何使相等操作变得不可靠。
3 #include <iostream>
4 using namespace std;
5
6 int main()
7 {
8     double a = 1.5; // a 是 1.5。
9     double b = 1.5; // b 是 1.5。
10
11    a += 0.00000000000001; // 给 a 增加一点点。
12    if (a == b)
13        cout << "Both a and b are the same.\n";
14    else
15        cout << "a and b are not the same.\n";
16
17    return 0;
18 }
```

### 程序输出

```text
Both a and b are the same.
```

为了防止舍入误差导致此类问题，你应该对浮点数坚持使用大于号和小于号进行比较。

### 现在回到“真”的概念

现在你已经接触了关系表达式和 if 语句，让我们来看“真”这个主题。你已经看到，关系表达式为真时值为 1，为假时值为 0。然而，在 if 语句的世界里，真的概念被扩展了。0 仍然是假，但除 0 以外的所有值都被视为真。这意味着任何值，即使是负数，只要它不是 0，就代表真。

就像现实生活中一样，真是一个复杂的问题。以下是你目前为止所看到的规则的总结：

- 当关系表达式为真时，它的值为 1。
- 当关系表达式为假时，它的值为 0。
- 任何值为 0 的表达式都被 if 语句视为假。
- 任何非 0 的值都被 if 语句视为真。
- 0 是假，等同于 0。
- 真是真，等同于 1。

if 语句包含非零值开启了许多可能性。关系表达式不是可以测试的唯一条件。例如，下面的语句是合法的：

```cpp
if (value)
    cout << "It True!";
```

上面的 if 语句测试不是关系表达式，而是变量的内容。如果变量包含非 0 的值，就会显示 "It True!"。这里是另一个例子：

```cpp
if (x + y)
    cout << "It True!";
```

你也可以将函数调用的返回值作为条件表达式。如果结果不是 0，就会执行 `cout` 语句。这里是使用 `pow` 的例子：

```cpp
if (pow(a, b))
    cout << "It True!";
```

该语句使用 `pow` 函数计算 a 的 b 次方。如果结果是任何值，就会执行 `cout` 语句。这是你将在第六 章学习的强大编程技巧。

### 不要混淆 == 和 =

之前你看到过警告，不要混淆相等运算符 (`==`) 和赋值运算符 (`=`)，例如：

```cpp
if (x = 2)
```

上面的语句并没有判断 x 是否等于 2，而是将 2 赋值给 x。此外，`cout` 语句会被执行，因为 2 是一个非零值，被解释为真。这是因为 `=` 运算符将值赋值给 if 语句的左侧。

### 程序 4-5

```cpp
1 // 本程序计算三个分数的平均分，
2 // 但本可以使用 == 运算符。
3 #include <iostream>
4 #include <iomanip>
5 using namespace std;
6
7 int main()
8 {
9     int score1, score2, score3; // 用于存储分数
10    double average; // 用于存储平均分
11
12    // 获取三个分数。
13    cout << "Enter test scores and I will average them ";
14    cin >> score1 >> score2 >> score3;
15
16    // 计算并显示平均分。
17    average = (score1 + score2 + score3) / 3.0;
18    cout << fixed << setprecision(1);
19    cout << "Your average is " << average << endl;
20
21    // 我们的意图是祝贺用户
22    // 满分。但这样做不可通。
23    if (average = 100) // 错误！这是赋值！
24        cout << "Congratulations! That's a perfect score!\n";
25    return 0;
26 }
```

### 显示示例输入的程序输出

```text
Enter test scores and I will average them: 80 90 70
Your average is 80.0
Congratulations! That's a perfect score!
```

无论平均分是多少，这个程序都会打印祝贺获得满分的消息。

### 扩展 if 语句

> **概念**：if 语句可以条件地执行由大括号括起的语句块。

如果你想让 if 语句条件地执行一组语句，而不只是一行呢？例如，如果测试平均分程序需要使用多个 `cout` 语句来显示祝贺信息，该怎么办？答案是将所有条件执行的语句封装在一组大括号中。

## 4.3 扩展 if 语句

格式如下：

```cpp
if (expression)
{
    statement;
    statement;
    // 根据需要放置尽可能多的语句。
}
```

程序 4-6 是测试平均分程序的另一种修改，演示了这种类型的语句。

### 程序 4-6

```cpp
1 // 此程序计算 3 次测试成绩的平均分。
2 // 它演示了 if 语句执行
3 // 一个语句块。
4 #include <iostream>
5 #include <iomanip>
6 using namespace std;
7
8 int main()
9 {
10    const int HIGH_SCORE = 95; // 高分为 95 或更高
11    int score1, score2, score3; // 用于存储三个测试成绩
12    double average; // 用于存储平均分
13
14    // 获取三个测试成绩。
15    cout << "Enter 3 test scores and I will average them: ";
16    cin >> score1 >> score2 >> score3;
17
18    // 计算并显示平均分。
19    average = (score1 + score2 + score3) / 3.0;
20    cout << fixed << showpoint << setprecision(1);
21    cout << "Your average is " << average << endl;
22
23    // 如果平均分很高，祝贺用户。
24    if (average > HIGH_SCORE)
25    {
26        cout << "Congratulations!\n";
27        cout << "That's a high score.\n";
28        cout << "You deserve a pat on the back!\n";
29    }
30    return 0;
31 }
```

### 显示加粗示例输入的程序输出

```text
Enter 3 test scores and I will average them: **100 100 100**
Your average is 100.0
Congratulations!
That's a high score.
You deserve a pat on the back!
```

### 显示加粗不同示例输入的程序输出

```text
Enter 3 test scores and I will average them: **80 90 70**
Your average is 80.0.
```

程序 4-6 在平均分大于 95 时会打印更详细的信息。if 语句被扩展，以便在 `highScore` 设置为 `true` 时执行三条语句。将一组语句封装在大括号内创建了一个代码块。只有当 `average` 大于 95 时，if 语句才会按照它们出现的顺序执行该块中的所有语句。否则，该块将被跳过。

注意大括号内的所有语句都缩进了。和以前一样，这在视觉上将语句与未缩进的行隔离开来，使得更明显地看出它们是 if 语句的一部分。

> **注意**：每当你的程序有一个代码块时，大括号内的所有语句都应该缩进。

## 不要忘记大括号！

如果你打算用 if 语句条件执行一个语句块，请不要忘记大括号。记住，没有大括号，if 语句只会执行紧随后的第一条语句。程序 4-7 显示了无意中遗漏 if 语句块中大括号的测试平均分程序。

### 程序 4-7

```cpp
// 此程序计算 3 次测试成绩的平均分。
// 无意中遗漏了 if 语句块中的大括号。
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    const int HIGH_SCORE = 95; // 高分为 95 或更高
    int score1, score2, score3; // 用于存储三个测试成绩
    double average; // 用于存储平均分

    // 获取三个测试成绩。
    cout << "Enter 3 test scores and I will average them: ";
    cin >> score1 >> score2 >> score3;

    // 计算并显示平均分。
    average = (score1 + score2 + score3) / 3.0;
    cout << fixed << showpoint << setprecision(1);
    cout << "Your average is " << average << endl;

    // 如果平均分很高，祝贺用户。
    if (average > HIGH_SCORE)
        cout << "Congratulations!\n";
    cout << "That's a high score.\n";
    cout << "You deserve a pat on the back!\n";

    return 0;
}
```

### 显示加粗输入的程序输出

```text
Enter 3 test scores and I will average them: **100 100 100**
Your average is 100.0
Congratulations!
That's a high score.
You deserve a pat on the back!
```

语句 25 和 26 即使平均分不大于 95 也会执行。因为大括号被移除，if 语句控制执行 24 行。正如图 5 所示。

```cpp
if (average > HIGH_SCORE)
    cout << "Congratulations!\n";
cout << "That's a high score.\n";
cout << "You deserve a pat on the back!\n";
```

### 检查

- 每当你的程序有一个代码块时，大括号内的所有语句都应该缩进。
- 写一个 if 语句：如果 `sales` 大于 50，将 10 赋值给 `commission`。
- 以下代码在语法上是正确的，但存在逻辑错误。你能找到它吗？

```cpp
if (sales > 50)
    cout << "This earns a bonus.";
commission += 10;
```

## 4.4 if/else 语句

将 if/else 语句考虑为道路的分叉口。不像 if 语句只是暂时的绕路，if/else 语句会导致程序执行两条路径之一。图 4-6 显示此 if/else 语句的逻辑。

### 图 4-6 if/else 语句

![](img/191adf284699566ea7b1008ce9bdb5_200.png)

### 程序 4-9（续）

```cpp
20      // 如果 num2 不为零，执行除法。
21      if (num2 == 0)
22          cout << "Division by zero is not possible.\n";
23          cout << "Please run the program again and enter\n";
24          cout << "a number other than zero.\n";
25      else
26          quotient = num1 / num2;
27          cout << "The quotient of " << num1 << " divided by "
28          cout << num2 << " is " << quotient << ".\n";
29      return 0;
```
