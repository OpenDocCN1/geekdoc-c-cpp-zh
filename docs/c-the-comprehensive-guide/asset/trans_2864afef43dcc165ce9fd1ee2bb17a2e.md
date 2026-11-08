
在这里，我定义了一个 lambda 作为操纵器，而不是函数。请注意，你必须用 `-> std::ostream&` 指定 lambda 的返回类型，以确保它返回的是引用而不是值。

输入流也是如此。

### 27.5.3 创建带参数的自定义操纵器

你也可以使用函数对象轻松地创建带参数的操纵器。

下面的清单是一个简单的示例，演示如何编写带参数的操纵器。

```cpp
// https://godbolt.org/z/KKE6nWT49
#include <iostream>
using std::cout; using std::endl;
class dendl { // Dots followed by newline
    int dendl_;
public:
    dendl(int n=1)
      : dendl_{n} {}
    std::ostream& operator()(std::ostream& os) const { // Functor
        for (int i=0; i<dendl_; ++i) os << '.';
        return os << '\n';
    }
};
std::ostream& operator<<(std::ostream& os, const dendl& elem) {
    return elem(os);
}
int main() {
    cout << "Text1" << dendl(4); // Output: Text1....
    cout << "Text2" << dendl(2); // Output: Text2..
    cout << "Text3" << dendl(); // Output: Text3.
}
```

**清单 27.11** 带参数的操纵器。

通过 dendl，你可以看到在 main 中定义所需函数对象的典型类定义。这个函数对象本身所做的只是输出 n 个点，然后换行。

正如你在 main 应用程序中所见，你会注意到单独使用函数对象还不行。与 `cout << dendl(4)` 等价的函数调用如下：

`operator<<(std::cout, dendl(4));`

然而，operator<< 还没有针对类型为 `dendl` 的第二个参数的重载。这个重载仍然需要提供——正如示例中那样。在重载中，只需要调用传入的函数对象。

针对输入流的带参数的操纵器的实现方式类似。

> **引用作为返回值**
> 
> 在这里，也同样建议返回引用，因为这可以确保后续操作可以与运算符进行链式调用。

### 27.5.4 直接更改格式标志

除了使用操纵器格式化流之外，你还可以使用方法来直接更改标志。虽然操纵器的使用通常更常见、也方便得多，但我们这里将简要讨论可用的方法。它们的区别也很容易解释。请看下面的清单，其中我们使用操纵器来格式化输出。

```cpp
// https://godbolt.org/z/csbPMYM19
#include <iostream>
#include <ios> // hex, dec
using std::cout; using std::endl;
int main() {
    int val = 255;
    cout << std::showbase << std::hex << val << endl;  // Output: 0xff
    cout << std::noshowbase << std::dec << val << endl; // Output: 255
}
```

**清单 27.12** 直接影响格式。

首先，我使用两个操纵器输出十六进制值（ff）以及进制前缀（0x）。然后我停用进制前缀的输出，并将进制切换回十进制。

这里使用的操纵器等价于以下指令，这些指令使用方法直接更改了标志。

```cpp
// https://godbolt.org/z/1xzzMdjdM
#include <iostream>
using std::cout; using std::endl;
int main() {
    int val = 255;
    cout.setf(std::ios_base::hex, std::ios_base::basefield);
    cout.setf(std::ios_base::showbase);
    cout << val << std::endl; // Output: 0xff
    cout.unsetf(std::ios_base::showbase);
    cout.setf(std::ios_base::dec, std::ios_base::basefield);
    cout << val << std::endl; // Output: 255
}
```

清单 27.13 使用 "setf" 和 "unsetf" 影响格式。

这里发生的事情与清单 27.12 相同，但首先是使用 hex 在 basefield 组中设置十六进制数字表示的位。为了确保进制前缀（0x）也被输出，我为 cout 流设置了这个标志。在下面我以相反的顺序做了同样的事情，在那里我再次清除 showbase 位。最后，我将 basefield 组中的标志重置回十进制整数输出（dec）。

我认为这个示例展示了操纵器比这里使用的 setf() 和 unsetf() 方法更清晰、更方便。使用操纵器，你不必处理诸如标志、位和位掩码之类的繁琐事物。而且最终，像 std::showbase 这样的操纵器在内部还是会调用 cout.setf(std::ios::showbase) 方法。

某些格式标志也可以分组使用，正如 dec 与 basefield 的示例所示。具体来说，有三个分组：adjustfield（包含标志 left、right、internal）、basefield（包含标志 dec、oct、hex）和 floatfield（包含标志 scientific 和 fixed）。

独立标志（如 showbase）可以单独使用（尽管需要使用 ios_base:: 或 ios:: 前缀）。表 27.7 概述了 ios_base 类中允许你直接更改格式标志的方法。

| 方法 | 含义 |
| :--- | :--- |
| setf(flags) | 将格式标志设置为 flags。 |
| setf(flags, group) | 将 group 组的格式标志设置为 flags。 |
| unsetf(flags) | 清除所有标志。 |
| flags() | 返回当前设置的格式标志。 |
| flags(flags) | 将格式标志设置为 flags。 |

表 27.7 访问格式标志的方法。

下一个清单与上一个示例相同，但现在所有内容都应仅使用 flags() 方法来实现。

## 27.6 用于文件输入和输出的流

你已经使用计算机一段时间了，并且一直在处理系统内存中的变量。你可能已经注意到，当你关闭程序时，所有这些变量都会消失。不过，别担心，因为在本节中，我将向你展示如何将这些变量永久保存到外部存储设备上，以便你随时需要时都可以访问它们。

在我们开始之前，我想快速介绍一下如何访问文件。要访问文件，你需要一些函数。这些函数由 C++ 标准库提供。在读写文件时，你不会逐字节访问它们。相反，你会以更大的块来访问它们以提高效率。对于这种数据传输，我们使用缓冲区作为 RAM 中的临时存储空间。你可以将文件或文件内容视为具有特定长度的字节数组。

就像你将数据写入文件一样，你也可以再次将其读出来。因此，你需要自己处理格式和结构。为了确保读写文件顺利进行，文件中有一个特殊的位置（从 0 开始）可供你使用。这被称为*文件位置*，它确保文件按正确的顺序进行处理。如果你从文件中读取 10 个字节，读取位置将位于第 10 个字节。写入也是如此。

### 27.6.1 “ifstream”、“ofstream”和“fstream”流

用于文件输入和输出的流已无缝集成到标准库的流概念中。如果你查看本章开头以及图 27.1 中的简化类层次结构，你会发现 ifstream、ofstream 和 fstream 文件流都以众所周知的类作为基类。这意味着你也可以将所有众所周知的输入/输出操作（例如 << 和 >> 运算符）用于文件。基本上，只有流对象发生了变化。现在使用的是与文件关联的其他流对象，而不是 cout 或 cin。以下是三个可用的文件流类的简要概述：

- `ifstream` 派生自 `istream`，用于读取文件。
- `ofstream` 派生自 `ostream`，用于写入文件。
- `fstream` 派生自 `iostream`，可用于读取和写入文件。

对于所有文件流，你必须在程序中包含 `<fstream>` 头文件。

### 27.6.2 连接到文件

要对文件进行任何操作，你必须首先实例化一个类型为 ifstream、ofstream 或 fstream 的适当流对象。此外，你必须打开文件。你既可以在实例化时直接使用适当的构造函数打开文件，也可以使用
