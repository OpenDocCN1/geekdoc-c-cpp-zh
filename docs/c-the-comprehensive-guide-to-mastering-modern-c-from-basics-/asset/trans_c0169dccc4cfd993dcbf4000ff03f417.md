

```cpp
ostream& flush();
```

立即刷新流缓冲区。缓冲区中所有尚未写入的字符现在必须被输出。

所有方法都返回 `ostream` 流。输出是否成功可以使用并且应该使用 `<ios>` 头文件中的函数（第 27.4 节）进行检查。

当使用方法读取原始数据进行非格式化输入时，与使用 `>>` 格式化读取不同，开头的空白字符不会被简单地跳过和忽略。对于非格式化输入`<iostream>` 头文件提供了几种方法，其中某些方法被重载了多次。

以下是 `<get(char& c):` 中非格式化输入方法的概述：

- istream& get(char& c); 从流中提取单个字符到 `c` 中。
- istream get(char* s, streamsize n); 从流中读取 `n-1` 个字符并将它们作为 C 字符串存储在 `s` 中。如果使用的字符少于 `n-1` 个，则继续读取直到遇到换行符 `'\n'`。换行符不会存储在 `s` 中。末尾会自动添加空终止符 `'\0'`。
- istream get(char* s, streamsize n, char del); 从流中读取 `n-1` 个字符并将它们作为 C 字符串存储在 `s` 中。如果使用的字符少于 `n-1` 个，则它读取到 `del` 中包含的第一个分隔符为止。`del` 字符不会存储在 `s` 中。末尾会自动附加终止字符 `'\0'`。
- istream&getline(char* s, streamsize n[], char del); 与相应的 `get()` 版本的主要区别在于如果读取了超过 `n-1` 个字符，则设置 `failbit` 错误标志。
- istream&read(char* s, streamsize n); 从流中提取 `n-1` 个字符并将它们存储在 C 字符串中。与 `get` 和 `getline` 版本不同，它返回流 `istream`。输入序列不以空字符 `'\0'` 终止——这是一个用于复制整个数据块的经典函数。

对于所有从流到 `char* s` 地址提取 `n-1` 个字符的版本，你必须确保 `s` 中有足够的内存空间。所有方法都返回输入，成功的与可以使用 `<ios>` 头文件中的机制（第 27.4 节）进行检查。在所有输入方法中，当读取到 EOF 时，从流提取字符的操作终止。

> 文件结束 (End of File)

EOF 通常定义为值 -1，用于指示数据流或文件的结束。在交互式 shell 中，你也可以通过组合键生成 EOF。在经典的 Unix shell 中，你可以通过 `Ctrl + D` 重现此。在 Windows 命令提示符中，使用 `Ctrl + Z` 生成 EOF。

下面的简单列表演示了非格式化输入的一些方法。

```cpp
// https://opbolt.org/z/MaEzcccTG
#include <iostream>
using std::cout; using std::cin; using std::endl;
int main() {
    const unsigned int MAX = 10;
    char buffer[MAX] = {0};
    cout << "Input getline : ";
    cin.getline(buffer, MAX);
    cout << std::cin.gcount() <<
    << " characters read\n";
    for(auto c : buffer) {
        if(c && c!='\0') cout.put(c);
    }
    cin.ignore(MAX, '\n');
    cout << "\nMake input (end with .) : ";
    char ch=0;
    while(cin.get(ch)) {
        if(ch == '.') break;
        cout.put(ch);
    }
    cout << "Input ended" << endl;
}
```

# 列表 27.2 来自流的非格式化输入。

首先，我从 `cin` 流中提取最多 `MAX` 个字符并将它们存储在 `buffer` 中。从流中实际提取的字符数量使用 `gcount()` 方法确定。`gcount()` 方法也可以用于所有其他非格式化输入方法。

然后我使用 `put()` 将单个字符输出到屏幕上。

在这个示例中，我使用 `ignore()` 方法跳过输入流中最多 `MAX` 个字符，直到遇到 `'\n'` 字符为止，并从缓冲区中移除 `'\n'`。这里也可以使用另一个字符代替 `'\n'`。在示例中，我用它将换行符从缓冲区中提取出来，这样它就不会在下一次读取操作中使用，从而可以被简单地跳过。

这个“技巧”并不处处都有效。在其他系统（如 Mac）上，你可以插入以下几行：

```cpp
cin.clear();
cin.ignore(cin.rdbuf()->in avail());
cin.get();
```

`while` 循环来自经典的 Unix 框架，它简单地从 `cin` 流中非格式化地读取所有字符并将它们输出到 `cout` 流。读取持续到输入句或到达 EOF。

程序在执行期间看起来如下：

```
Input getline: Hello getline
9 characters were read
Hello get
Make an input (end with .): Hello get
Hello get
Another line
Another line
We end with a period.
We end with a period
Input ended
```

```cpp
std::string and getline()
```

在 `<string>` 头文件中，你还会找到 `getline()` 方法，它可以从流中读取一行到 `std::string` 中。

# 27.4 错误处理和流状态

对于流，仅仅检查某操作是否工作（true）或不工作（false）通常是不够的。因为可能会发生各种类型的错误，I/O 流提供了检查状态的机制。常量定义在 `ios_base` 中作为公共成员，并可以直接访问（例如 `ios::goodbit`）。表 27.1。

| 常量 | 含义 |
| :--- | :--- |
| goodbit | 无问题。 |
| eofbit | 已到达流末尾。 |
| failbit | 输入/输出错误。 |
| badbit | 严重错误。 |

# 27.4.1 处理错误的方法

对于流，它提供了各种方法来检查状态。常量定义在 `ios_base` 中作为公共成员并可以访问：

- good() - 如果一切正常（设置了 goodbit）返回 true。
- eof() - 如果到达流末尾则返回 true。
- fail() - 如果发生 I/O 错误则返回 true。
- bad() - 如果发生严重错误则返回 true。
- clear() - 将状态重置为 goodbit。
- clear(ios_base f) - 使用 f 位重置状态。
- setstate(ios_base f) - 使用 f 设置状态。
- rstate() - 返回当前状态。
- ustate() - 返回区域的状态。
- xstate() - 返回流缓冲区的状态。
- bitset() - 返回位set的状态。
- flags() - 返回整数形式的状态。
- setbit(ios_base f) - 使用 f 设置位。
- unset(ios_base f) - 取消 f 位。
- test(ios_base f) - 测试 f 位是否设置。
- toggle(ios_base f) - 翻转 f 位。

在 `<string>` 头文件中，你还会找到 `getline()` 方法，它可以从流中读取一行到 `std::string` 中。

