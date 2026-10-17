
这个程序将永远循环。如果你运行程序，可以通过在程序运行的控制台窗口中输入 `CTRL+C`（在 Windows 和 Unix 上）或 `CMD + .`（在 Mac 上）来停止它。

### 4.2 do-while 循环

它们与 while 循环非常相似，区别在于是否继续执行的测试是在循环的末尾进行的。例如：

```cpp
void launchRocket_DoWhileVersion() {
 int count = 10;
 do {
  cout << count;
  cout << "\n";
  count--;
 } while (count >= 1);
 cout << "Blast off!\n";
}
```

do-while 循环的一般语法是：

```cpp
do {
 <语句>;
} while (<表达式>);
```

因为测试只在 do-while 循环的末尾进行，循环主体至少会被执行一次。通常认为 do-while 循环难以阅读，因此它们使用的并不频繁。其他循环结构更受青睐。

### 4.3 for 循环

C 语言的设计者注意到，大多数 while 语句在轮廓上看起来像这样：

```cpp
<初始化循环变量>;
while (<测试循环变量>) {
 <执行代码的主要步骤>
 <更新循环变量>
}
```

为了使这种重复的设计在代码中更明显，他们引入了 for 循环。其一般形式如下：

```cpp
for (<初始化循环变量>;
 <测试循环变量>;
 <更新循环变量>) {
 <执行代码的主要步骤>
}
```

要编写一个 for 循环，只需取上述形式的 while 循环，并移动代码以匹配 for 循环的语法。例如，我们发射火箭的代码变为：

```cpp
for (int i = 10; i > 0; i--) {
 cout << i;
 cout << "\n";
}
cout << "Blast off!\n";
```

对于 C++ 的新手来说，这看起来并没有多大改进。唯一明显的优势是，这比等效的 while 循环占用更少的行数。然而，它读起来不如 while 循环像英语。如果你是 C 和 C++ 的新手，你可能会觉得 while 循环更容易跟踪。随着熟悉度的增加，你会开始更喜欢 for 循环。并不是因为它在你实际阅读代码时更容易理解，而是因为你能识别出一般形状，从而可以在不查看细节的情况下猜测其含义。很快，你只需瞥一眼 for 循环就能立即可以看到它正在做什么，而使用 `while` 循环时，你需要实际阅读代码才能理解。

以下是从 0 数到 9（包含 9）的代码。你应该将这段代码牢记在心：

```
    for ( int i = 0; i < 10; i++) {
        cout << i;
        cout << "\n";
    }
```

将其与通用语法进行对照，我们看到“初始化循环变量”的代码是：

```
int i = 0
```

因此，这段代码初始化了一个名为 `i` 的变量，并将其初始值设置为 0。

“测试循环变量”的代码是 `i < 10`。因此，循环体将重复执行，直到 `i` 等于 10。请注意，值 10 本身不会被打印出来。

“更新循环变量”的代码是 `i++`。因此，在每次循环之后，`i` 都会递增。

“执行代码主要步骤”是

```
    cout << i;
    cout << "\n";
```

这些主要步骤总共会重复 10 次。

以下是以 10 为步长从 0 数到 90（包含 90）的代码。

```
    for ( int i = 0; i < 100; i += 10) {
        cout << i;
        cout << "\n";
    }
```

# 提示：从 0 开始计数

C++ 程序员从 0 开始计数。这是一个约定。C++ 中所有的标准数据结构都以 0 作为起始标签。

一开始你可能不习惯，但我强烈建议你在编写 C++ 程序时从 0 开始计数，并因此使用 `<` 符号而不是 `<=` 符号作为补偿。

从 0 开始计数有一些相当好的理由，因为这样一些公式编写起来更简单。例如，假设你按如下方式标记矩阵的条目：

![](img/70e8b6971c8420e92597c05233ce9700_81_0.png)

假设你用索引 `$i \in \{0, 1, 2, 3\}$` 标记行，用索引 `$j \in \{0, 1, 2, 3\}$` 标记列——那么 `$(i, j)$` 处的条目是 `$4i + j$`。显而易见，这个公式如何推广到比矩阵更高维的数据结构。

让我们重复一次练习，这次我们从 1 开始计数。我们会按以下方式标记矩阵的条目：

![](img/70e8b6971c8420e92597c05233ce9700_82_0.png)

现在，我们用索引 `$i' \in \{1, 2, 3, 4\}$` 标记行，并类似地用 `$j' \in \{1, 2, 3, 4\}$` 标记列。`$(i, j)$` 处的条目现在是 `$4(i' - 1) + (j' - 1) + 1 = 4i' + j' - 3$`。与之前相比，这是一个优雅程度低得多的公式，并且它不能像以前那样直接推广到更高维度。

注意，C++ 中还有另一种 `for` 循环，其语法更简单，但相应地灵活性较低。详见第 18 章。

### 4.4 break, continue, return

在循环中间，你可以决定跳出循环并开始执行循环之后的语句，使用 `break` 关键字即可做到这一点。

例如，这段代码不断累加用户输入的数字，直到他们输入一个负数为止。此时，软件会打印出所有正数的总和。

```
cout << "Enter positive numbers followed ";
cout << "by a negative number to quit\n";
int total = 0;
while (true) {
    int next;
    cin >> next;
    if (next < 0) {
        break;
    }
    total += next;
}
cout << "The total is " << total << "\n";
```

`continue` 关键字的意思是跳过循环体内剩余的代码，转到下一个测试语句，并决定是否继续循环。因此，`continue` 意味着“继续循环”，而 `break` 意味着“跳出循环”。

以下是 continue 语句的一个示例：

```
        cout << "Enter positive numbers ";
        cout << "Type CTRL+C to quit\n";
        int total = 0;
        while (true) {
            int next;
            cin >> next;
            if (next < 0) {
                continue;
            }
            total += next;
            cout << "Positive total is " << total << "\n";
        }
```

你也可以在循环中间使用 `return` 语句。这会停止所有循环，并将执行返回到函数被调用的位置。

以下是从循环内部返回的一个示例：

```
void countdown() {
    int i = 10;
    while (true) {
        if (i == 0) {
            return;
        }
        cout << i << "\n";
        i--;
    }
}
```

虽然 `break` 和 `continue` 有时可以使代码更清晰，但它们通常使代码更难追踪。因此，建议 C++ 新手避免使用这些语句。

### 4.5 throw 语句

很多时候，你会希望函数突然停止并指示发生了错误。为此，你需要使用 `throw` 语句。

要使用 throw 语句，你需要在代码开头与其他 `#include` 语句并排添加以下文本：

```
#include <stdexcept>
```

要指示发生了错误，请使用以下形式：

```c
throw logic_error("You can't do that");
```

你可以在引号之间包含几乎任何你喜欢的文本。尽量提供一些线索来说明是什么导致了问题。当我们讨论第 7.5 节的字符串操作时，你将能够创建更有用的错误消息。

以下是如何可能使用 `throw` 语句的一个示例：

```cpp
double debitAccount(double balance, double amount) {
    double newAmount = balance - amount;
    if (newAmount < 0.0) {
        throw logic_error("No overdraft agreed");
    }
    return newAmount;
}
```

程序最好通过 `throw` 一个错误并终止，而不是打印出错误消息并试图继续运行。这有几个原因：

- 没有人阅读消息！金融领域使用的许多代码是在服务器上运行的，而不是在用户的计算机上。如果你将消息写入服务器的日志文件，很可能从来没有人会阅读它。

- 明显失败比微妙失败更好。你不希望有人以为交易已经成功，而实际上它失败了。

- 如果错误立即抛出，很容易看到错误发生的位置以及错误发生时正在发生的事情。如果你一天后再查看日志文件，你可能无法弄清楚当时发生了什么。

你可能想尝试用比仅仅终止程序更精致的方式来处理错误，但事实是你可能做不到。如果发生在我们编写的这类代码中的错误，很可能是一个编程错误，无论让用户多久后再试都无法解决这个问题。除此之外，没有别的办法，只能报告错误并修复代码。

在软件中处理错误是计算机科学中的一个高级主题。如果你在编写操作系统，至关重要的一点是单个程序的 bug 不会导致整个计算机崩溃。如果你在编写 web 浏览器，重要的是单个流氓 web 页面不会导致 web 浏览器崩溃。然而，编写 web 浏览器和操作系统是这些领域专家的任务，而不是金融数学专家的任务。

如果你希望用比简单终止程序更精致的方式来处理错误，你需要使用 `try` 和 `catch` 语句。此外，你可能希望抛出除了 `logic_error` 之外不同类型的错误，以便你可以区分不同类型的错误。你可以在任何 C++ 参考书中找到更多信息。本书中不需要这些技术。

### 4.6 switch 语句

if 语句的一种更复杂的替代方案是 `switch` 语句。以下是一个示例：

```c++
void printMessage(int score) {
 switch (score){
 case 0:
 case 1:
 case 2:
 case 3:
 case 4:
 cout << "You have failed.\n";
 break;
 case 5:
 case 6:
 cout << "You have passed.\n";
 break;
 case 7:
 cout << "Merit.\n";
 break;
 case 8:
 case 9:
 cout << "Distinction.\n";
 break;
 default:
 cout << "Invalid score.\n";
 break;
 }
 cout << "Good luck in your future career.\n";
}
```

这个程序根据你的分数打印出考试的等级。0-4 分不及格，5 或 6 分及格，7 分为优秀（Merit），8 或 9 分为卓越（Distinction）。

通用语法是：

```
switch (<expression>) {
```

case <possible value>:

    <statements>

case <possible value>:

    <statements>

...

case <possible value>:

    <statements>

default:

    <statements>

}
switch 语句的主体是位于花括号之间的代码。它由一系列可能的 case（分支）和执行代码组成。当执行这个 switch 语句时，计算机首先会评估 `expression`（表达式）。然后，它会寻找第一个匹配的 case 语句，并执行从该处到第一个 break 语句或 switch 语句结束的所有代码。

如果没有匹配项，计算机将寻找 `default`（默认）语句，并评估从该处到 switch 语句结束的所有代码。

在执行完 switch 语句主体中所需的语句后，程序将继续执行 switch 语句之后的下一条语句。在我们的示例中，这意味着它将祝你在职业生涯中好运。

请注意，你必须小心地在 `switch` 语句中插入 `break` 或 `return` 语句，以确保代码不会执行比你想要的更多的语句。

例如，如果你从我们的示例中移除所有的 `break` 语句，那么得分为 0 时将得到如下响应：

```
You have failed.
You have passed.
Merit.
Distinction.
Invalid score.
Good luck in your future career.
```

如果你不喜欢 `switch` 语句的语法，你不是一个人。幸运的是，在现代 C++ 代码中，它们并不非常有用。在现代 C++ 中，应该使用面向对象的编程技术 `polymorphism`（多态性）来代替。我们将在第 10 章中深入探讨这一主题。如果你发现自己倾向于编写 `switch` 语句，这表明你还没有充分利用面向对象编程的优势。

## 提示：始终包含一个默认情况（default case）

如果你必须编写 `switch` 语句，请务必始终包含一个 `default` 分支。通常，你的默认分支会通过使用 `throw` 语句来生成错误。简单地打印一个错误（如我们的示例中那样）是一个坏主意。

### 4.7 作用域

上述控制流语句使用了花括号。如果你在花括号内定义一个变量，它只能在这些花括号内使用。一旦程序的执行离开花括号，该变量就会被删除。你可以引用变量的代码部分被称为该变量的 `scope`（作用域）。

下面是一个示例代码片段，它计算前 10 个整数（当然从 0 开始）的平方和。

```cpp
int n=0;
int total;
for (int i=0; i<10; i++) {
    int squareValue = i*i;
    total += squareValue;
}
std::cout << n;
// std::cout << squareValue;
// std::cout << i;
```

变量 `squareValue` 仅在花括号内有效。变量 `i` 仅在 for 语句本身及花括号内有效。如果你尝试移除最后两行中的注释字符 `//`，代码将无法编译。

变量的作用域用于控制 C++ 中的内存使用。当变量超出作用域时，内存可以被安全地重用。通常你不需要考虑 C++ 中的内存管理。然而，有时你会想要自己控制内存管理。我们将在第 11 章中讨论这个问题。

### 4.8 运算符中的控制流

一个技术要点是，C++ 中的某些运算符实际上以微妙的方式控制着程序的流程。

#### 4.8.1 短路求值（Short circuit evaluation）

表达式 `lhs && rhs` 如果 `lhs` 和 `rhs` 都求值为 true，则结果为 true。为了提高效率，如果 `lhs` 不为 true，C++ 甚至不会费心去评估表达式 `rhs`。这通常正是你希望发生的情况。然而，如果评估表达式 `rhs` 实际上调用了另一个函数，你可能会惊讶地发现这个函数并不总是被调用。

类似地，如果已知 `lhs` 为 true，`lhs || rhs` 就不会评估 `rhs`。

作为示例，请尝试以下代码：

```cpp
bool test1() {
    cout << "In test1\n";
    return false;
}
bool test2() {
    cout << "In test2\n";
    return true;
}
int main() {
    bool value = test1() && test2();
    cout << "Value " << value << "\n";
    return 0;
}
```

你会发现函数 `test2` 从未被调用。

#### 4.8.2 三元运算符（The ternary operator）

表达式 `a*b` 中的 `*` 运算符被称为二元运算符，因为它接受两个参数。另一方面，`++` 运算符被称为一元运算符。

C++ 还包含一个接受三个参数的运算符，因此被称为三元运算符。

三元运算符本质上是一种编写 if 语句的快捷方式。其语法如下：

`<test expression> ? <value if true> : <value if false>`

作为示例，这里是一个使用三元运算符计算两个数字最大值的程序：

```cpp
int max(int a, int b) {
    return a>b ? a : b;
}
```

这里有一些使用 if 语句的等效代码。

```cpp
int max(int a, int b) {
  if (a > b) {
    return a;
  } else {
    return b;
  }
}
```

那些懒得打字的人喜欢三元运算符，但它会导致代码非常难以理解。不要使用它。

#### 4.8.3 逗号运算符（The comma operator）

在 for 语句的圆括号之间，始终有三个用分号分隔的表达式。这是一个示例：

```cpp
for (int i = 0; i < 100; i++) {
  cout << i << "\n";
}
```
