

```cpp
char boss[8] = "Bozo";
```

![](img/9afc44517b591d64e2e19f623c9308ef_136_0.png)

注意，字符串常量（用双引号）与字符常量（用单引号）不能互换。字符常量，例如 `'S'`，是字符编码的简写表示。在 ASCII 系统中，`'S'` 只是书写 83 的另一种方式。因此，下面的语句将值 83 赋给 `shirt_size`：

```cpp
char shirt_size = 'S';        // this is fine
```

但是 `"S"` 不是字符常量；它表示由两个字符组成的字符串，即 `S` 和 `\0` 字符。更糟的是，`"S"` 实际上表示存储该字符串的内存地址。因此，像下面这样的语句试图把一个内存地址赋给 `shirt_size`：

```cpp
char shirt_size = "S";        // illegal type mismatch
```

因为在 C++ 中地址是一种单独的类型，所以 C++ 编译器不会允许这种荒谬做法。（本章后面讨论指针之后，我们会回到这一点。）

## 拼接字符串字面量

有时字符串太长，不便放在一行代码中。C++ 允许你拼接字符串字面量——也就是说，把两个带引号的字符串合并成一个。实际上，任何两个仅由空白（空格、制表符和换行符）分隔的字符串常量都会自动连接成一个。因此，下面所有输出语句彼此等价：

```cpp
cout << "I'd give my right arm to be" " a great violinist.\n";
cout << "I'd give my right arm to be a great violinist.\n";
cout << "I'd give my right arm to be a great violinist.\n";
```

注意，连接不会向被连接的字符串添加任何空格。第二个字符串的第一个字符紧跟在第一个字符串的最后一个字符之后（不计 `\0`）。第一个字符串中的 `\0` 字符被第二个字符串的第一个字符替换。

## 在数组中使用字符串

将字符串放入数组的两种最常见方式是：将数组初始化为字符串常量，以及将键盘或文件输入读入数组。程序清单 4.2 演示了这些方法：将一个数组初始化为带引号的字符串，并使用 `cin` 将输入字符串放入第二个数组。该程序还使用标准 C 库函数 `strlen()` 获取字符串长度。标准 C++ 字符串头文件（对于较旧的实现则是 `cstring.h`）为该函数以及许多其他与字符串相关的函数提供了声明。

### 程序清单 4.2 `cstring.cpp`

```cpp
// strings.cpp -- storing strings in an array
#include <iostream>
#include <cstring>  // for the strlen() function
int main()
{
    using namespace std;
    const int Size = 15;
    char name1[Size];              // empty array
    char name2[Size] = "C++owboy";  // initialized array
    // NOTE: some implementations may require the static keyword
    // to initialize the array name2

    cout << "Howdy! I'm " << name2;
    cout << "! What's your name?\n";
    cin >> name1;
    cout << "Well, " << name1 << ", your name has ";
    cout << strlen(name1) << " letters and is stored\n";
    cout << "in an array of " << sizeof(name1) << " bytes.\n";
    cout << "Your initial is " << name1[0] << ".\n";
    name2[3] = '\0';                // set to null character
    cout << "Here are the first 3 characters of my name: ";
    cout << name2 << endl;
    return 0;
}
```

下面是程序清单 4.2 中程序的一次示例运行：

```text
Howdy! I'm C++owboy! What's your name?
Basicman
Well, Basicman, your name has 8 letters and is stored
in an array of 15 bytes.
Your initial is B.
Here are the first 3 characters of my name: C++
```

## 程序说明

从程序清单 4.2 中可以学到什么？首先，注意 `sizeof` 运算符给出整个数组的大小，即 15 字节，但 `strlen()` 函数返回的是存储在数组中的字符串的大小，而不是数组本身的大小。另外，`strlen()` 只统计可见字符，不统计空字符。因此，对于 Basicman 的长度，它返回值 8，而不是 9。如果 cosmic 是一个字符串，那么保存该字符串所需的最小数组大小为 `strlen(cosmic) + 1`。

因为 `name1` 和 `name2` 是数组，所以你可以使用索引访问数组中的各个字符。例如，程序使用 `name1[0]` 查找该数组中的第一个字符。此外，程序将 `name2[3]` 设置为空字符。这使得字符串在三个字符之后结束，即使数组中还剩下更多字符（见图 4.3）。

```cpp
const int ArSize = 15;
char name2[ArSize] = "C++owboy";
```

![](img/9afc44517b591d64e2e19f623c9308ef_138_0.png)

```cpp
name2[3] = '\0';
```

![](img/9afc44517b591d64e2e19f623c9308ef_138_1.png)

图 4.3 用 `\0` 缩短字符串。

注意，程序清单 4.2 中的程序使用符号常量表示数组大小。数组大小经常出现在程序中的多条语句里。使用符号常量表示数组大小可以简化修改程序以使用不同数组大小的工作；你只需在定义符号常量的地方改一次值。

## 字符串输入历险记

`strtype.cpp` 程序有一个瑕疵，它被一种常常有用的技巧——精心选择的示例输入——掩盖了。程序清单 4.3 揭开面纱，表明字符串输入可能很棘手。

### 程序清单 4.3 `instrt1.cpp`

```cpp
// instrt1.cpp -- reading more than one string
#include <iostream>
int main()
{
    using namespace std;
    const int ArSize = 20;
    char name[ArSize];
    char dessert[ArSize];

    cout << "Enter your name:\n";
    cin >> name;
    cout << "Enter your favorite dessert:\n";
    cin >> dessert;
    cout << "I have some delicious " << dessert;
    cout << " for you, " << name << ".\n";
    return 0;
}
```

程序清单 4.3 中程序的意图很简单：从键盘读取用户的名字和最喜欢的甜点，然后显示这些信息。下面是一次示例运行：

```text
Enter your name:
Alistair Dreeb
Enter your favorite dessert:
I have some delicious Dreeb for you, Alistair.
```

我们甚至没有机会回应甜点提示！程序显示该提示后，立即继续显示最后一行。

问题在于 `cin` 如何判断你何时输入完一个字符串。你无法从键盘输入空字符，所以 `cin` 需要某种其他方式来确定字符串的结尾。`cin` 的技术是使用空白——空格、制表符和换行符——来划分字符串。这意味着当 `cin` 为字符数组获取输入时，只读取一个单词。读取这个单词后，`cin` 在将字符串放入数组时会自动添加终止空字符。

在这个例子中的实际结果是，`cin` 把 Alistair 作为整个第一个字符串读取，并放入 `name` 数组。这使得可怜的 Dreeb 仍留在输入队列中。当 `cin` 在输入队列中搜索对最喜欢的甜点问题的回答时，它发现 Dreeb 还在那里。然后 `cin` 吞掉 Dreeb 并放入 `dessert` 数组（见图 4.4）。

另一个问题在示例运行中没有暴露出来，那就是输入字符串可能比目标数组更长。像这个例子那样使用 `cin` 并不能防止把 30 个字符的字符串放入 20 个字符的数组。

![](img/9afc44517b591d64e2e19f623c9308ef_140_0.png)

许多程序依赖字符串输入，因此进一步探讨这个主题是值得的。我们将要借助 `cin` 的一些更高级的特性，这些特性在第 17 章“输入、输出和文件”中描述。

## 一次读取一行字符串输入

一次读取一个单词的字符串输入通常不是最理想的选择。例如，假设程序要求用户输入城市，用户回答 *New York* 或 *Sao Paulo*。你会希望程序读取并存储完整名称，而不仅仅是 *New* 和 *Sao*。为了能够输入完整短语而不是单个单词作为字符串，你需要一种不同的字符串输入方法。具体来说，你需要一种面向行的方法，而不是面向单词的方法。你很幸运，因为 `istream` 类（`cin` 就是其一个实例）有一些面向行的类成员函数：`getline()` 和 `get()`。两者都读取整行输入——也就是说，直到换行字符为止。然而，`getline()` 随后会丢弃换行字符，而 `get()` 会把它留在输入队列中。让我们从 `getline()` 开始看细节。

### 使用 `getline()` 进行面向行的输入

`getline()` 函数读取整行，使用回车键发送的换行字符标记输入结束。你通过把 `cin.getline()` 用作函数调用来调用这个方法。该函数接受两个参数。第一个参数是目标名称（即用于保存该行输入的数组），第二个参数是要读取的字符数限制。如果这个限制是，比如 20，那么函数读取不超过 19 个字符，留出空间以便在末尾自动添加空字符。`getline()` 成员函数在达到这个数值限制或读取到换行字符时停止读取输入，以先发生者为准。

例如，假设你想使用 `getline()` 将一个名字读入包含 20 个元素的 `name` 数组。你会使用这个调用：

```cpp
cin.getline(name,20);
```

