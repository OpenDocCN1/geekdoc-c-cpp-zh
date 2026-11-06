

## C++ 输入/输出

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_43_0.png)

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_44_0.png)

## C++ 输入/输出

当你编写的代码能够请求用户输入，然后用该输入生成用户可以看到的内容时，会有一种令人满足的感觉。即使只是询问某人的名字，并显示一条个性化的欢迎信息，也是一次巨大的飞跃。

用户交互、字符字面量、定义常量以及文件输入和输出都将在以下页面中介绍。所有这些都能帮助你更好地理解 C++ 程序的工作方式。

### 步骤 5

其原理与之前的代码相同。用户的输入（即他们的名字）存储在一个字符串中，因为它包含多个字符，并在第二个 `cout` 行中取出显示。只要变量“name”不改变，你就可以在代码中任意位置调用它。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_46_0.png)

### 步骤 6

你可以连续向用户请求输入，但前提是必须有一个有效的变量来存储输入。假设你希望用户输入两个整数：

```cpp
#include <iostream>
using namespace std;

int main ()
{
    int num1, num2;

    cout << "Enter two whole numbers: ";
    cin >> num1 >> num2;

    cout << "you entered " << num1 << " and " << num2 << "\n";
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_46_1.png)

### 步骤 7

同样，一旦输入的数据存储在变量中，就可以对其进行操作。例如，要求用户输入两个数字并对它们进行一些数学运算：

```cpp
#include <iostream>
using namespace std;

int main ()
{
    float num1, num2;

    cout << "Enter two numbers: \n";
    cin >> num1 >> num2;

    cout << num1 << " + " << num2 << " is: " << num1 + num2 << "\n";
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_46_2.png)

### 步骤 8

虽然 `cin` 在大多数输入任务中表现良好，但它确实有一个局限性。`cin` 总是将空格视为终止符，因此它只适用于单个单词而非多个单词。然而，`getline` 将 `cin` 作为第一个参数，将变量作为第二个参数：

```cpp
#include <iostream>
using namespace std;

int main ()
{
    string mystr;
    cout << "Enter a sentence: \n";
    getline(cin, mystr);

    cout << "Your sentence is: " << mystr.size() << " characters long.\n";
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_46_3.png)

### 步骤 9

构建并执行代码，然后输入一个包含空格的句子。完成后，代码会读取字符数。如果你删除 `getline` 行，将其替换为 `cin >> mystr` 并再次尝试，结果将显示直到第一个空格前的字符数。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_46_4.png)

### 步骤 10

`getline` 通常是 C++ 初学者容易忘记的命令。当你无法找出代码不工作的原因时，终止空白符很令人烦恼。简而言之，将来最好使用 `getline(cin, variable)`：

```cpp
#include <iostream>
using namespace std;

int main ()
{
    string name;
    cout << "Enter your full name: \n";
    getline(cin, name);

    cout << "\nHello, " << name << "\n";
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_46_5.png)

## 字符字面量

在 C++ 中，字面量是一个对象或变量，一旦定义，在整个代码中保持不变。然而，字符字面量由反斜杠定义，比如你在 `cout` 语句末尾使用的 `\n`，用来表示换行。

### 转义序列

当用于诸如 `cout` 语句中时，字符字面量也被称为转义序列代码。它们允许你插入引号、警报、换行等等。

### 步骤 1

创建一个新的 C++ 文件并输入相关的头文件：

```cpp
#include <iostream>
using namespace std;

int main ()
{

}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_47_0.png)

### 步骤 2

你已经体验过 `\n` 字符字面量在调用处插入换行的功能。代码行：`cout << "Hello\n" << "I'm a C++\n" << "Program\n";` 会输出三行文本，每行都从上一个 `\n` 之后开始。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_47_1.png)

### 步骤 3

如果你想在 `cout` 语句中插入说话引号，就必须使用反斜杠，因为它本身已经使用了引号：

```cpp
#include <iostream>
using namespace std;

int main ()
{
    cout << "Hello, user. This is how to use \"quotes\".";
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_47_2.png)

### 步骤 4

甚至有一种字符字面量可以触发警报。在 Windows 10 中，当你使用 `\a` 时，它会发出通知声音。试试这段代码，并把声音调大。

```cpp
#include <iostream>
using namespace std;

int main ()
{
    cout << "ALARM! \a";
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_47_3.png)

### 便捷图表

有许多字符字面量（或转义序列代码）可供选择。因此，我们认为为你准备一个便捷图表会很有用，方便你在需要插入代码时查阅。

| 转义序列代码 | 字符 |
| --- | --- |
| `\` | 反斜杠 |
| `\'` | 单引号 |
| `\"` | 双引号（说话引号） |
| `\?` | 问号 |
| `\a` | 警报/闹铃 |
| `\b` | 退格 |
| `\f` | 换页 |
| `\n` | 换行 |
| `\r` | 回车 |
| `\t` | 水平制表符 |
| `\v` | 垂直制表符 |
| `\0` | 空字符 |
| `\uxxxx` | Unicode（UTF-8） |
| `\Uxxxxxxxx` | Unicode（UTF-16） |

### Unicode 字符（UTF-8）

Unicode 字符是在所有平台上都通用的符号或字符。例如，版权符号可以通过在键盘上输入 Unicode 代码，然后按 ALT+X 来输入。对于版权符号，请输入：00A9 Alt+X。在 C++ 代码中，你应输入：

```cpp
#include <iostream>
using namespace std;

int main ()
{
    cout << "\u00A9";
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_48_0.png)

### Unicode 字符表

完整的可用 Unicode 字符列表可以在 **www.unicode-table.com/en/** 上找到。将鼠标悬停在字符上即可查看其在 C++ 中输入的独特代码。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_48_1.png)

## 定义常量

常量是代码中的固定值。它们可以是任何基本数据类型，但顾名思义，它们的值在整个代码中保持不变。在 C++ 中有两种不同的方式来定义常量：`#define` 预处理器和 `const`。

### #DEFINE

预处理指令是给编译器的指令，在编译代码之前先对信息进行预处理。#include 是预处理指令，#define 也是。

### 步骤 1

你可以使用 `#define` 预处理指令在代码中定义任何你想要的常量。首先创建一个新的 C++ 文件，并包含通常的头文件：

```cpp
#include <iostream>
using namespace std;

int main ()
{
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_49_0.png)

### 步骤 2

现在假设你的代码有三个不同的常量：长度、宽度和高度。你可以用以下方式定义它们：

```cpp
#include <iostream>
using namespace std;
#define LENGTH 50
#define WIDTH 40
#define HEIGHT 60

int main ()
{
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_49_1.png)

### 步骤 3

注意定义常量时使用大写字母，将所有常量定义为大写是良好的编程实践。这里，赋的值是 50、40 和 60，所以让我们调用它们：

```cpp
#include <iostream>
using namespace std;

#define LENGTH 50
#define WIDTH 40
#define HEIGHT 60

int main ()
{
    cout << "Length is: " << LENGTH << "\n";
    cout << "Width is: " << WIDTH << "\n";
    cout << "Height is: " << HEIGHT << "\n";
}
```

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_49_2.png)

### 步骤 4

构建并运行代码。正如预期的那样，它会显示每个已创建常量的值。值得注意的是，使用 `#define` 关键字定义常量时不需要分号。

![](img/bdf3833c5133a7f9b1eef9ebdb21a76d_49_3.png)

