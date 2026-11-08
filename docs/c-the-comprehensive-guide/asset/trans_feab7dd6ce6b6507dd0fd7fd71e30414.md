
对象。对于输入，`<istream>` 头文件包含 `cin` 流对象，它可用于典型的用户输入（例如来自键盘）。

### 27.2.1 流运算符 << 和 >>

基本上，数据流最初只不过是不可读的字节序列，通过特化 `operator<<` 将其格式化为输出，通过特化 `operator>>` 将其格式化为输入。

在 `<iostream>` 头文件中，你会发现 `operator<<` 针对所有内置类型进行了多次重载：

```cpp
ostream& operator<<(bool val);
ostream& operator<<(short val);
ostream& operator<<(unsigned short val);
ostream& operator<<(int val);
// ...
```

对于 `<istream>` 头文件中的 `operator>>` 也是如此：

```cpp
istream& operator>>(bool val);
istream& operator>>(short val);
istream& operator>>(unsigned short val);
istream& operator>>(int val);
// ...
```

通过让 `operator<<` 和 `operator>>` 运算符返回流的引用，就可以连续多次使用这些运算符，如下面的清单所示。

```cpp
// https://godbolt.org/z/WaEGdNWvq
#include <iostream> // cin, cout
int main() {
    int val1, val2;
    std::cout << "Please enter 2 int values: ";
    std::cin >> val1 >> val2;
    std::cout << val1 << " : " << val2 << std::endl;
}
```

**清单 27.1** 通过引用返回流允许链式调用。

> **使用自定义类型**
>
> 许多标准类（如 `string`）也实现了 `operator<<` 和 `operator>>` 运算符。对于自定义类，如果希望 `<<` 和/或 `>>` 能与流配合使用，你需要自行实现这些运算符。

标准输入/输出运算符支持 C++ 中几乎所有基本类型。例外是 `void` 和 `nullptr_t`。当然，输入和输出并非任意发生。还有几件事需要考虑：

- **数值类型**
  
  读取数值时，输入必须至少以一个数字开头。如果使用 `+` 或 `-` 指定符号，该符号只能出现在第一个数字之前。但是，符号与数字之间不能有空格。前导空白字符会被忽略。如果输入错误，数值会被设为 0，并设置 `std::failbit`。

- **`char*`**
  
  在 C 中，使用 `char*` 进行输入就已经非常危险。输入会一直读取到第一个空白字符或直到 *文件结束*（EOF；后文会详细说明）。前导空白会被跳过，这可以通过 `skipws` 操纵符更改。读取 `char*` 的问题在于它可能读到缓冲区之外（缓冲区溢出）——例如 `char cval[20]; std::cin >> cval`。如果你在这里读入超过 20 个字符，`cin` 会忠实地照做并写入未定义的内存区域。因此，对于旧的 C 字符串（如果你绝对必须使用它们），你必须始终确保不超过最大长度。为此，适合使用 `<iomanip>` 头文件中的 `setw` 操纵符——例如 `cin >> setw(20) >> cval`。

- **bool**
  
  `bool` 的输出会转换为：`false` 为 0，`true` 为 1。对于输入，最初适用与数值相同的规则。当输入除 0 以外的有效数值时，会转换为 1（`=true`）。当输入 0 时，则使用 0（表示 `false`）。如果输入错误，该值也会被设为 0，并设置 `std::failbit`。

## 27.3 流输入和输出的方法

除了流常用的 `operator<<` 和 `operator>>` 之外，你还可以使用 I/O 流库提供的方法。然而，与 << 和 >> 运算符不同，这些方法处理原始字节，因此是未格式化的。标准输入/输出方法使用 `<ios>` 中的 `streamsize` 类型，该类型通常是 `size_t`。这意味着，例如，在输入期间不会忽略前导空白。

### 27.3.1 未格式化输出的方法

对于原始和未格式化的输出，I/O 流库提供了来自 `<ostream>` 头文件的 `put()` 和 `write()` 方法。`put()` 方法输出单个字符，`write()` 输出指定数量的字符。以下代码片段简要演示了这些方法：

### 27.3.2 未格式化输入的方法

使用方法读取原始数据时，与使用 >> 进行格式化读取不同，前导空白字符不会被简单地跳过和忽略。对于未格式化输入，头文件 `<istream>` 提供了若干方法，其中一些被多次重载。

以下是 `<istream>` 中未格式化输入方法的概述：

- `istream& get(char& c);`
  
  从流中提取单个字符到 c。
- `istream& get(char* s, streamsize n);`
  
  这从流中读取 n-1 个字符，并将它们作为 C 字符串存储在 s 中。如果使用的字符少于 n-1 个，则继续读取直到第一个换行字符 '\n'。换行字符不会存储在 s 中。末尾会自动添加空终止符 '\0'。
- `istream& get(char* s, streamsize n, char delim);`
  
  这从流中读取 n-1 个字符，并将它们作为 C 字符串存储在 s 中。如果使用的字符少于 n-1 个，则读取到 delim 中包含的第一个分隔字符为止。分隔字符不会存储在 s 中。末尾会自动追加终止字符 '\0'。
- `istream& getline(char* s, streamsize n[, char delim]);`
  
  与相应的 get() 版本的主要区别在于，如果读取的字符超过 n-1 个，则会设置 failbit 错误标志。
- `istream& read(char* s, streamsize n);`
  
  这从流中提取 n（不是 n-1）个字符，并将它们存储在 C 字符串 s 中。与 get 和 getline 版本不同，读取的序列不会以空字符 '\0' 终止——这是用于复制整个数据块的经典函数。

对于所有从流中提取 n–1 个字符到 char* s 地址的版本，你必须确保 s 中有足够的内存空间可用。所有方法都返回 istream 流。输入是否成功可以/应该使用 `<ios>` 头文件中可用的机制来检查（第 27.4 节）。在所有输入方法中，当读到 EOF 时，从流中提取字符的过程都会终止。

> **文件结束**
>
> EOF 通常定义为值 –1，用于表示数据流或文件的结束。在交互式 shell 中，你也可以通过组合键生成 EOF。在经典 Unix shell 中，可以使用 [Ctrl]+[D] 来产生 EOF。在 Windows 命令提示符中，使用 [Ctrl]+[Z] 生成 EOF。

以下简单清单演示了一些未格式化输入的方法。

```cpp
// https://godbolt.org/z/MeAzcccTG
#include <iostream>
using std::cout; using std::cin; using std::endl;
int main() {
    const unsigned int MAX = 10;
    char buffer[MAX] = {0};
    cout << "Input getline : ";
    cin.getline(buffer, MAX);
    cout << std::cin.gcount()
         << " characters were read\n";
    for(auto c : buffer) {
        if(c && c!='\0') cout.put(c);
    }
    cin.ignore(MAX, '\n');
    cout << "\nMake input ( end with ): ";
    char ch=0;
    while(cin.get(ch)) {
        if(ch == '#') break;
        cout.put(ch);
    }
    cout << "Input ended" << endl;
}
```

**清单 27.2** 从流进行未格式化输入。

首先，我从 cin 流中提取最多 MAX 个字符，并将它们存储在 buffer 中。实际从流中提取的字符数通过 gcount() 方法确定。gcount() 方法也可以用于所有其他未格式化输入方法。

然后我使用 put() 将单个字符输出到屏幕。

在这个例子中，我使用 ignore() 方法从输入流中跳过最多 MAX 个字符，直到 '\n' 字符，并从缓冲区中移除 '\n'。这里也可以使用另一个字符代替 '\n'。在示例中，我使用这一行将换行字符从缓冲区中取出，以便它不会在下次读取操作中被使用，从而可以被简单地跳过。

这个“技巧”并非在所有地方都有效。在其他系统（例如 Mac）上，你可以插入以下行：

```cpp
cin.clear();
cin.ignore(cin.rdbuf()->in_avail());
cin.get();
```
