

# 文件 I/O 语句总结（续）

- 使用流 `outStream` 将输出发送到 `outfile.txt`，就像使用 `cout` 向屏幕发送输出一样。例如：

```
outStream << "someVariable = ="
<< someVariable << endl;
```

- 使用 `close` 函数关闭流：

```
inStream.close();
outStream.close( );
```

# 自测练习

- 1. 假设你正在编写一个使用名为 `fin` 流的程序，该流将连接到一个输入文件，另一个名为 `fout` 的流将连接到一个输出文件。你如何声明 `fin` 和 `fout`？你需要在程序文件中放置哪个包含指令（include directive）？

- 2. 假设你正在继续编写上一个练习中讨论程序，并希望程序从文件 `infile.txt` 获取输入并将输出发送到文件 `outfile.txt`。你需要在程序中放置哪些语句将流 `fin` 连接到文件 `infile.txt`，并将流 `fout` 连接到文件 `outfile.txt`？务必包含检查以确保打开成功。

- 3. 假设你仍在编写我们在之前的练习中讨论的同一个程序，现在你已经不再需要从文件 `infile.txt` 获取输入，也不再需要向文件 `outfile.txt` 发送输出。你如何关闭这些文件？

- 4. 假设你想更改显示 12.1 中的程序，使其将输出发送到屏幕而不是文件 `outfile.txt`。（输入应来自文件 `infile.txt`。）你对程序需要做哪些更改？

- 5. 一位程序员拥有文件中的半行内容。程序员必须对文件进行什么操作才能再次读取第一行？

# 字符 I/O

第 9 章描述了通过 `cin` 从键盘进行字符 I/O 以及通过 `cout` 向屏幕输出。文件的字符 I/O 工作方式与键盘和屏幕的 I/O 相同。使用连接到文件的输入流代替 `cin` 或使用连接到文件的输出流代替 `cout`。特别是，`get`、`getline`、`putback`、

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_557_0.png)

`peek` 和 `ignore` 在文件输入中的工作方式与键盘输入相同；`put` 在文件输出中的工作方式与屏幕输出相同。

# 检查文件结束

处理输入文件的常用方法是使用循环从文件中处理数据，直到到达末尾。测试文件末尾有两种标准方法。最直接的方法是使用 `eof` 成员函数。每个输入流都有一个成员函数 `eof`，可用于测试是否到达输入文件的末尾。该函数不接受参数，因此对成员流的调用写为：

```
fin.eof()
```

这是一个布尔表达式，可以控制循环、`do-while` 循环或 `if-else` 语句。如果程序读取过了输入文件的末尾，该表达式返回 `true`；否则返回 `false`。由于我们想测试是否不在文件末尾，因此使用 `not`（`!`）来该成员函数。记得在 C++ 中，符号 `!` 用于表示“非”。可以使用以下循环将连接到输入流的文件全部内容写入屏幕：

```
inputStream.get(next);
while (!inputStream.eof())
{
    cout << next << endl;
    inputStream.get(next);
}
```

之前的循环使用成员函数从输入文件读取每个字符到 `char` 变量 `next`，并将其写入屏幕。程序通过文件末尾后，`instream.eof()` 的值从 `false` 变为 `true`。因此，

```
!inputStream.eof()
```

从 `true` 变为 `false`，循环结束。
注意，`inStream.eof()` 直到程序尝试读取文件末尾之外的一个字符之前，不会变为 `true`。例如，假设文件包含以下内容（在 `c` 之后没有换行符）：

```
ab
c
```

# 第 12 章 流与文件 I/O

这实际上是以下字符列表：

```
ab换行符 '\n'>c
```

循环将读取一个 'a' 并写入屏幕，读取一个 'b' 并写入屏幕，然后读取换行符 '\n' 并写入屏幕，然后读取一个 'c' 并写入屏幕。此时，循环已经拥有了文件中的所有字符。然而，`inStream.eof()` 的值仍为 `false`，直到程序尝试再读一个字符时才会变为 `true`。这就是为什么 `while` 循环以 `inStream.get(next)` 结束。循环需要多读一个字符来结束循环。

文件末尾有一个特殊的文件结束标记。在该文件结束标记改变之前，成员函数不会从 `false` 变为 `true`。这就是为什么 `while` 循环读取的字符比你认为的文件字符多一个。然而，这个文件结束标记不是普通字符，不应像普通字符那样进行处理。你可以读取这个文件结束标记，但不应将其写出。结果是不可预测的。系统会自动在每个文件的最后放置这个文件结束标记。

复杂的是，某些编译器上 `eof` 的实现会在没有文件结束标记的情况下返回 `true`，因此你可能需要检查编译器的文档或编写一个短程序来确定你编译器的行为。

检查文件结束的第二种方法是（并利用）使用提取运算符读取实际上返回一个布尔值。表达式

```
(inStream >> next)
```

如果循环成功，则返回 `true`；当你的代码尝试读取文件末尾之外时，返回 `false`。例如，以下代码将读取连接到输入流 `inStream` 的所有整数，并在变量 `sum` 中计算它们的和：

```
double sum = 0;
while (inStream >> next)
    sum = sum + next;
cout << "the sum is " << sum << endl;
```

之前的循环可能看起来很奇怪，因为 `inStream >> next` 从流中读取一个数字并返回一个布尔值。涉及提取运算符 `>>` 的表达式既是一个动作，又是一个布尔条件。如果有另一个数字要输入，则读取该数字并返回布尔值 `true`，因此循环体再执行一次。

> 从技术上讲，布尔条件的工作方式如下：`operator >>` 的返回值是一个输入流引用（`istream&`），如第 8 章所述。该流引用会自动转换为布尔值。如果流能够提取数据，则结果为 `true`，否则为 `false`。

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_559_png)

# I/O 流 531

如果没有更多数字可以读取，则没有输入并返回布尔值 `false`，循环结束。在这个示例中，输入 `next` 的类型是 `double`，但这种检查文件结束的方法对于其他数据类型（如 `int` 和 `char`）同样有效。

这种测试文件结束的第二方法被许多 C++ 程序员采用，似乎出于文化原因。它在 C 语言中很常用。取决于实现细节，这种方法可能更高效。无论如何，无论你需要它来理解其他程序员的代码，`eof` 成员函数的示例在显示 12.4 中。

# 显示 12.4 检查文件结束（部分 1/2）

```
// 从 story.txt 到 numstory.txt，
// 在每行开头添加一个数字。
// 假设 story.txt 不空。
#include <fstream>
#include <iostream>
#include <cstdlib>

using std::ifstream;
using std::ostream;
using std::cout;

int main() 
{
    ifstream fin;
    ostream fout;

    fin.open("story.txt");
    if (fin.fail()) {
        cout << "Input file opening failed.\n";
        exit(1);
    }

    fout.open("numstory.txt");
    if (fout.fail()) {
        cout << "Output file opening failed.\n"
        exit(1);
    }
n
```

